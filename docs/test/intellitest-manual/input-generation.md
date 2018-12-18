---
title: Execução simbólica dinâmica | Ferramenta de teste do desenvolvedor do Microsoft IntelliTest
ms.date: 05/02/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- IntelliTest, Dynamic symbolic execution
ms.author: gewarren
manager: douge
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: 33bd31c59de85f70d653d2de912b8c9bc5bb0e30
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51295885"
---
# <a name="input-generation-using-dynamic-symbolic-execution"></a>Geração de entrada usando a execução simbólica dinâmica

O IntelliTest gera entradas para [testes de unidade parametrizados](test-generation.md#parameterized-unit-testing) analisando as condições de branch no programa. As entradas do teste são escolhidas com base em se elas podem disparar novos comportamentos de ramificação do programa. A análise é um processo incremental. Ela refina um predicado **q: I -> {true, false}** nos parâmetros de entrada de teste formal **I**. **q** representa o conjunto de comportamentos que o IntelliTest já observou. Inicialmente, **p: = false**, uma vez que ainda não foi observado nada.

As etapas do loop são:

1. O IntelliTest determina entradas **i** de forma que **q(i)=false** usando um [solver de restrição](#constraint-solver). 
   Pela construção, a entrada **i** utilizará um caminho de execução não visto antes. Inicialmente, isso significa que **i** pode ser qualquer entrada, porque nenhum caminho de execução foi descoberto ainda.

1. O IntelliTest executa o teste com a entrada de escolhida **i** e monitora a execução de teste e do programa em teste.

1. Durante a execução, o programa usa um caminho específico que é determinado por todos os branches condicionais do programa. O conjunto de todas as condições que determinam a execução é chamado de *condição de caminho*, escrito como o predicado **p: I -> {true, false}** sobre os parâmetros de entrada formais. O IntelliTest computa uma representação desse predicado.

1. O IntelliTest define **q := (q ou p)**. Em outras palavras, ele registra o fato de que viu o caminho representado pelo **p**.

1. Vá para a etapa 1.

O [solver de restrição](#constraint-solver) do IntelliTest pode lidar com valores de todos os tipos que podem aparecer em programas .NET:

* [Inteiros](#integers-and-floats) e [Floats](#integers-and-floats)
* [Objetos](#objects)
* [Estruturas](#structs)
* [Matrizes](#arrays-and-strings) e [Cadeias de Caracteres](#arrays-and-strings)

O IntelliTest filtra entradas que violam as suposições indicadas.

Além das entradas imediatas (argumentos para [testes de unidade parametrizados](test-generation.md#parameterized-unit-testing)), um teste pode obter valores adicionais da classe estática [PexChoose](static-helper-classes.md#pexchoose). As opções também determinam o comportamento das [simulações parametrizadas](#parameterized-mocks).

<a name="constraint-solver"></a>
## <a name="constraint-solver"></a>Solver de restrição

O IntelliTest usa um solver de restrição para determinar os valores de entrada relevantes de um teste e o programa em teste.

O IntelliTest usa o solver de restrição [Z3](https://github.com/Z3Prover/z3/wiki).

<a name="dynamic-code-coverage"></a>
## <a name="dynamic-code-coverage"></a>Cobertura de código dinâmica

Como um efeito colateral do monitoramento do tempo de execução, o IntelliTest coleta dados de cobertura de código dinâmica. Ela é chamada de *dinâmica* porque o IntelliTest sabe apenas sobre o código que foi executado, portanto ele não pode fornecer valores absolutos para a cobertura da mesma maneira que outra ferramenta de cobertura normalmente faz. 

Por exemplo, quando o IntelliTest informa a cobertura dinâmica como blocos básicos de 5/10, isso significa que cinco blocos de dez foram abrangidos, em que o número total de blocos em todos os métodos que foram alcançados até agora pela análise (em vez de todos os métodos que existem no assembly em teste) é de dez.
Posteriormente na análise, conforme mais métodos acessíveis forem descobertos, o numerador (5 nesse exemplo) e o denominador (10) podem aumentar.

<a name="integers-and-floats"></a>
## <a name="integers-and-floats"></a>Inteiros e floats

O [solver de restrição](#constraint-solver) do IntelliTest determina os valores de entrada de teste de tipos primitivos como **byte**, **int**, **float** e outros para disparar diferentes caminhos de execução diferentes para o teste e o programa em teste.

<a name="objects"></a>
## <a name="objects"></a>Objetos

O IntelliTest pode [criar instâncias de classes do .NET existentes](#existing-classes) ou você pode usar o IntelliTest para automaticamente [criar objetos fictícios](#parameterized-mocks) que implementam uma interface específica e se comportam de maneiras diferentes dependendo do uso.

<a name="existing-classes"></a>
## <a name="instantiate-existing-classes"></a>Criar instâncias de classes existentes

**Qual é o problema?**

O IntelliTest monitora as instruções executadas quando ele executa um teste e o programa em teste. Em particular, ele monitora todo o acesso aos campos. Em seguida, ele usa um [solver de restrição](#constraint-solver) para determinar as novas entradas de teste, incluindo objetos e seus valores de campo, por exemplo, de modo que o teste e o programa em teste se comportarão de outras maneiras interessantes.

Isso significa que o IntelliTest deve criar objetos de certos tipos e definir seus valores de campo. Se a classe for [visível](#visibility) e tiver um construtor [visível](#visibility) padrão, o IntelliTest poderá criar uma instância da classe.
Se todos os campos da classe forem [visível](#visibility), o IntelliTest poderá definir os campos automaticamente.

Se o tipo não for visível ou os campos não forem [visíveis](#visibility), o IntelliTest precisará de ajuda para criar objetos e colocá-los em estados interessantes para alcançar a cobertura de código máxima. O IntelliTest poderia usar reflexão para criar e inicializar instâncias de maneiras arbitrárias, mas isso geralmente não é  
desejável porque pode trazer o objeto para um estado que nunca pode ocorrer durante a execução normal do programa. Em vez disso, o IntelliTest depende de dicas do usuário.

<a name="visibility"></a>
## <a name="visibility"></a>Visibilidade

O .NET Framework tem um modelo de visibilidade elaborado: tipos, métodos, campos e outros membros podem ser **privados**, **públicos**, **internos** e muito mais.

Quando o IntelliTest gera testes, ele tenta executar somente ações (por exemplo, chamar construtores, métodos e definir campos) que são válidas em relação às regras de visibilidade do .NET de dentro do contexto dos testes gerados.

As regras são as seguintes:

* **Visibilidade de membros internos**
  * O IntelliTest pressupõe que os testes gerados terão acesso a membros internos que eram visíveis para a delimitação [PexClass](attribute-glossary.md#pexclass).
  O .NET tem o **InternalsVisibleToAttribute** para estender a visibilidade de membros internos para outros assemblies.<p />

* **Visibilidade de membros privados e de família (protegidos no C#) do [PexClass](attribute-glossary.md#pexclass)**
  * O IntelliTest sempre coloca os testes gerados diretamente no [PexClass](attribute-glossary.md#pexclass) ou em uma subclasse. Portanto, o IntelliTest pressupõe que ele pode usar todos os membros de família visíveis (**protegidos** no C#).
  * Se os testes gerados forem colocados diretamente no [PexClass](attribute-glossary.md#pexclass) (geralmente usando classes parciais), o IntelliTest pressuporá que ele também pode usar todos os membros privados do [PexClass](attribute-glossary.md#pexclass).<p />

* **Visibilidade de membros públicos**
  * O IntelliTest pressupõe que ele pode usar todos os membros exportados visíveis no contexto do [PexClass](attribute-glossary.md#pexclass).

<a name="parameterized-mocks"></a>
## <a name="parameterized-mocks"></a>Simulações parametrizadas

Como testar um método que tem um parâmetro de um tipo de interface? Ou de uma classe não selada? O IntelliTest não sabe quais implementações serão usadas posteriormente quando este método for chamado. E talvez não exista nem mesmo uma implementação real disponível no momento do teste.

A resposta convencional é usar *objetos fictícios* com comportamento explícito. 

Um objeto fictício implementa uma interface (ou estende uma classe não selada). Ele não representa uma implementação real, mas apenas um atalho que permite a execução de testes usando o objeto fictício. Seu comportamento é definido manualmente como parte de cada caso de teste em que ele é usado. Existem muitas ferramentas que facilitam a definição de objetos fictícios e seu comportamento esperado, mas esse comportamento ainda deve ser definido manualmente.

Em vez de valores embutidos em código em objetos fictícios, o IntelliTest pode gerar os valores. Assim como ele permite [teste de unidade parametrizado](test-generation.md#parameterized-unit-testing), o IntelliTest também permite simulações parametrizadas.

As simulações parametrizadas têm dois modos de execução diferentes:

* **escolha**: ao explorar o código, simulações com parâmetros são uma fonte de entradas de teste adicionais e o IntelliTest tentará escolher valores interessantes
* **reprodução**: ao executar um teste gerado anteriormente, as simulações parametrizadas se comportam como stubs com comportamento (em outras palavras, comportamento predefinido).

Use [PexChoose](static-helper-classes.md#pexchoose) para obter valores para as simulações parametrizadas.

<a name="structs"></a>
## <a name="structs"></a>Structs

O raciocínio do IntelliTest sobre os valores **struct** é semelhante à maneira que ele lida com [objetos](#objects).

<a name="arrays-and-strings"></a>
## <a name="arrays-and-strings"></a>Matrizes e cadeias de caracteres

O IntelliTest monitora as instruções executadas conforme ele executa um teste e o programa em teste. Em particular, ele observa quando o programa depende do tamanho de uma cadeia de caracteres ou uma matriz (e os limites inferiores e comprimentos de uma matriz multidimensional). Ele também observa como o programa usa os diferentes elementos de uma cadeia de caracteres ou matriz. Ele usa um [solver de restrição](#constraint-solver) para determinar quais valores de elemento e comprimentos podem fazer o teste e o programa em teste se comportarem de maneiras interessantes.

O IntelliTest tenta minimizar o tamanho das matrizes e cadeias de caracteres necessárias para disparar comportamentos de programa interessantes.

<a name="additional-inputs"></a>
## <a name="obtain-additional-inputs"></a>Obter entradas adicionais

A classe estática [PexChoose](static-helper-classes.md#pexchoose) pode ser usada para obter entradas adicionais para um teste e pode ser usada para implementar [simulações parametrizadas](#parameterized-mocks).

<a name="further-reading"></a>
## <a name="further-reading"></a>Leitura adicional

* [Como funciona?](https://blogs.msdn.microsoft.com/devops/2014/12/11/smart-unit-tests-a-mental-model/)

## <a name="got-feedback"></a>Recebeu comentários?

Poste suas ideias e solicitações de recursos na [Comunidade de Desenvolvedores](https://developercommunity.visualstudio.com/content/idea/post.html?space=8).