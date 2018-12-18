---
title: Avisos e erros | Ferramenta de teste do desenvolvedor do Microsoft IntelliTest
ms.date: 05/02/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: reference
helpviewer_keywords:
- IntelliTest, Warnings and errors
ms.author: gewarren
manager: douge
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: efb82a7419ba58c27ccab864d2360538075a1089
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51000608"
---
# <a name="warnings-and-errors"></a>Avisos e erros

## <a name="warnings-and-errors-by-category"></a>Avisos e erros por categoria

* **Limites**
  * [MaxBranches excedido](#maxbranches-exceeded)
  * [MaxConstraintSolverTime excedido](#maxconstraintsolvertime-exceeded)
  * [MaxConditions excedido](#maxconditions-exceeded)
  * [MaxCalls excedido](#maxcalls-exceeded)
  * [MaxStack excedido](#maxstack-exceeded)
  * [MaxRuns excedido](#maxruns-exceeded)
  * [MaxRunsWithoutNewTests excedido](#maxrunswithoutnewtests-exceeded)<p />

* **Solução de restrição**
  * [Não é Possível Concretizar a Solução](#cannot-concretize-solution)<p />

* **Domínios**
  * [Precisa de Ajuda para Construir o Objeto](#help-construct)
  * [Precisa de Ajuda para Encontrar Tipos](#help-types)
  * [Tipo Utilizável Estimado](#usable-type-guessed)<p />

* **Execução**
  * [Falha Inesperada Durante a Exploração](#unexpected-exploration)
  * [TargetInvocationException](#targetinvocationexception)<p />

* **Instrumentação**
  * [Método Não Instrumentado Chamado](#uninstrumented-method-called)
  * [Método Externo Chamado](#external-method-called)
  * [Método Não Instrumentável Chamado](#uninstrumentable-method-called)
  * [Problema de Capacidade de Teste](#testability-issue)
  * [Limitação](#limitation)<p />

* **Interpretador**
  * [Incompatibilidade de Chamada Observada](#observed-call-mismatch)
  * [Valor Armazenado no Campo Estático](#value-static-field)

<a name="maxbranches-exceeded"></a>
## <a name="maxbranches-exceeded"></a>MaxBranches excedido

O IntelliTest limita o comprimento de qualquer caminho de execução que ele explora durante a [geração de entrada](input-generation.md). Esse recurso impede que o IntelliTest deixe de responder quando o programa entrar em um loop infinito.

Cada branch condicional e incondicional do código executado e monitorado é contada até esse limite, inclusive branches que não dependem das entradas do [teste de unidade parametrizado](test-generation.md#parameterized-unit-testing).

Por exemplo, o código a seguir consome branches na ordem de 100:

```csharp
for (int i=0; i<100; i++) { }
```

Você pode editar a opção **MaxBranches** de um atributo derivado de **PexSettingsAttributeBase**, como [PexClass](attribute-glossary.md#pexclass) ou [PexMethod](attribute-glossary.md#pexmethod). O exemplo a seguir remove efetivamente este limite:

```csharp
[PexMethod(MaxBranches=int.MaxValue)]
public void MyTest(...) {
    // ....
}
```

Você também pode definir a opção **TestExcludePathBoundsExceeded** para informar o IntelliTest como lidar com esses problemas de forma geral.

No código de teste, você pode usar [PexSymbolicValue](static-helper-classes.md#pexsymbolicvalue) para ignorar restrições geradas pela condição de loop:

```csharp
for (int i=0;
    PexSymbolicValue.Ignore(i<100); // IntelliTest will 'forget' about this path condition
    i++)
{ }
```

<a name="maxconstraintsolvertime-exceeded"></a>
## <a name="maxconstraintsolvertime-exceeded"></a>MaxConstraintSolverTime excedido

O IntelliTest usa um [solver de restrição](input-generation.md#constraint-solver) para calcular novas entradas de teste. A solução de restrição pode ser um processo muito demorado, portanto, o IntelliTest permite que você configure os limites, em especial, **MaxConstraintSolverTime**.

Para muitos aplicativos, aumentar significativamente o tempo limite não resultará em uma cobertura melhor. A razão para isso é que a maioria dos tempos limite é causada por sistemas de restrição que não tem soluções. No entanto, o IntelliTest pode não conseguir determinar que isso é inconsistente sem testar todas as soluções possíveis, o que resultará em um tempo limite.

<a name="maxconditions-exceeded"></a>
## <a name="maxconditions-exceeded"></a>MaxConditions excedido

O IntelliTest limita o comprimento de qualquer caminho de execução que ele explora durante a [geração de entrada](input-generation.md). Esse recurso impede que o IntelliTest deixe de responder quando o programa entrar em um loop infinito.

Cada branch condicional que depende das entradas do [teste de unidade parametrizado](test-generation.md#parameterized-unit-testing) é contada até esse limite.

Por exemplo, cada caminho no código a seguir consome **n+1** condições:

```csharp
[PexMethod]
void ParameterizedTest(int n) {
    // conditions are "0<n", "1<n", ..., "!(n<n)"
    for (int i=0; i<n; i++)
    { ... }

    // irrelevant for MaxConditions, since conditions do not depend on input
    for (int i=0; i<100; i++)
    { ... }
}
```

Você pode editar a opção **MaxConditions** de um atributo derivado de **PexSettingsAttributeBase**, como [PexClass](attribute-glossary.md#pexclass) ou [PexMethod](attribute-glossary.md#pexmethod). Por exemplo:

```csharp
[PexMethod(MaxConditions=10000)]
void ParameterizedTest(int n) {
    // ...
}
```

Você também pode definir a opção **TestExcludePathBoundsExceeded** para informar o IntelliTest como lidar com esses problemas de forma geral.

Você pode usar [PexSymbolicValue](static-helper-classes.md#pexsymbolicvalue) para ignorar restrições geradas pela condição de loop:

```csharp
[PexMethod]
void ParameterizedTest(int n) {
    int nshadow = PexSymbolicValue.Ignore(n); // IntelliTest looses track of 'n'

    // irrevelant for MaxConditions, since nshadow is not related to input
    for (int i=0; i<nshadow; i++)
    {...}
}
```

<a name="maxcalls-exceeded"></a>
## <a name="maxcalls-exceeded"></a>MaxCalls excedido

O IntelliTest limita o comprimento de qualquer caminho de execução que ele explora durante a [geração de entrada](input-generation.md). Esse recurso impede que o IntelliTest deixe de responder quando o programa entrar em um loop infinito.

Cada chamada (direta, indireta, virtual ou pulo) do código executado e monitorado é contada até esse limite.

Você pode editar a opção **MaxCalls** de um atributo derivado de **PexSettingsAttributeBase**, como [PexClass](attribute-glossary.md#pexclass) ou [PexMethod](attribute-glossary.md#pexmethod). O exemplo a seguir remove efetivamente este limite:

```csharp
[PexMethod(MaxCalls=int.MaxValue)]
public void MyTest(...) {
    // ....
}
```

Você também pode definir a opção **TestExcludePathBoundsExceeded** para informar o IntelliTest como lidar com esses problemas de forma geral.

<a name="maxstack-exceeded"></a>
## <a name="maxstack-exceeded"></a>MaxStack excedido

O IntelliTest limita o tamanho da pilha de chamadas de qualquer caminho de execução que ele explora durante a [geração de entrada](input-generation.md). Esse recurso impede que o IntelliTest seja encerrado quando ocorrer um excedente de pilha.

Você pode editar a opção **MaxStack** de um atributo derivado de **PexSettingsAttributeBase**, como [PexClass](attribute-glossary.md#pexclass) ou [PexMethod](attribute-glossary.md#pexmethod). O exemplo a seguir remove efetivamente este limite (não recomendado):

```csharp
[PexMethod(MaxStack=int.MaxValue)]
public void MyTest(...) {
    // ....
}
```

Você também pode definir a opção **TestExcludePathBoundsExceeded** para informar o IntelliTest como lidar com esses problemas de forma geral.

<a name="maxruns-exceeded"></a>
## <a name="maxruns-exceeded"></a>MaxRuns excedido

O IntelliTest limita o número de caminhos de execução que ele explora durante a [geração de entrada](input-generation.md). Esse recurso garante que o IntelliTest seja encerrado quando o programa tem loops ou recursão.

Pode não ser o caso que, sempre que o IntelliTest executa o teste parametrizado com entradas específicas, ele emite um novo caso de teste. Consulte [TestEmissionFilter](exploration-bounds.md#testemissionfilter) para obter mais informações.

Você pode editar a opção **MaxRuns** de um atributo derivado de **PexSettingsAttributeBase**, como [PexClass](attribute-glossary.md#pexclass) ou [PexMethod](attribute-glossary.md#pexmethod). O exemplo a seguir remove efetivamente este limite (não recomendado):

```csharp
[PexMethod(MaxRuns=2000)]
public void MyTest(...) {
    // ....
}
```

<a name="maxrunswithoutnewtests-exceeded"></a>
## <a name="maxrunswithoutnewtests-exceeded"></a>MaxRunsWithoutNewTests excedido

O IntelliTest limita o número de caminhos de execução que ele explora durante a [geração de entrada](input-generation.md). Esse recurso garante que o IntelliTest seja encerrado quando o programa tem loops ou recursão.

Pode não ser o caso que, sempre que o IntelliTest executa o teste parametrizado com entradas específicas, ele emite um novo caso de teste. Consulte [TestEmissionFilter](exploration-bounds.md#testemissionfilter) para obter mais informações.

Enquanto o IntelliTest geralmente encontra muitas entradas de teste interessantes inicialmente, ele pode não emitir mais nenhum teste após um tempo. Essa opção determina quanto tempo o IntelliTest pode continuar tentando encontrar outra entrada de teste relevante.

Você pode editar a opção **MaxRunsWithoutNewTests** de um atributo derivado de **PexSettingsAttributeBase**, como [PexClass](attribute-glossary.md#pexclass) ou [PexMethod](attribute-glossary.md#pexmethod). O exemplo a seguir remove efetivamente este limite (não recomendado):

```csharp
[PexMethod(MaxRunsWithoutNewTests=2000)]
public void MyTest(...) {
    // ....
}
```

<a name="cannot-concretize-solution"></a>
## <a name="cannot-concretize-solution"></a>Não é possível concretizar a solução

Esse erro geralmente é a consequência de um erro anterior. O IntelliTest usa um [solver de restrição](input-generation.md#constraint-solver) para determinar novas entradas de teste. Às vezes, as entradas de teste propostas pelo [solver de restrição](input-generation.md#constraint-solver) são inválidas. Isso pode ocorrer quando:

* determinadas restrições não são conhecidas
* se os valores forem criados de forma definida pelo usuário, causando erros no código do usuário
* alguns dos tipos envolvidos têm a lógica de inicialização não controlada pelo IntelliTest (por exemplo, classes COM)

<a name="help-construct"></a>
## <a name="need-help-to-construct-object"></a>Precisa de ajuda para construir o objeto

O IntelliTest [gera as entradas do teste](input-generation.md) e algumas das entradas podem ser objetos com campos.
Aqui, o IntelliTest tenta gerar uma instância de uma classe que tem um campo particular e ele pressupõe que um comportamento do programa interessantes ocorrerá quando esse campo particular tiver um valor específico.

No entanto, embora isso seja possível com o Reflection, o IntelliTest não produz objetos com valores de campo arbitrários.
Em vez disso, nesses casos, ele se baseia no usuário para fornecer dicas sobre como usar os métodos públicos de uma classe para criar um objeto e colocá-lo em um estado em que seu campo particular tenha o valor desejado.

Leia [Criando instâncias de classes existentes](input-generation.md#existing-classes) para saber como você pode ajudar o IntelliTest a construir objetos interessantes.

<a name="help-types"></a>
## <a name="need-help-to-find-types"></a>Precisa de ajuda para encontrar tipos

O IntelliTest [gera as entradas de teste](input-generation.md) para qualquer tipo de .NET. Aqui, o IntelliTest tenta criar uma instância que deriva de uma classe abstrata ou implementa uma interface abstrata e o IntelliTest não sabe de nenhum tipo que satisfaça as restrições.

Você pode ajudar o IntelliTest apontando para um ou mais tipos que correspondam às restrições. Normalmente, um dos seguintes atributos ajudará:

* **PexUseTypeAttribute**, que aponta para um tipo específico.

  Por exemplo, se o IntelliTest relata que ele "não conhece nenhum dos tipos atribuíveis ao **System.Collections.IDictionary**", você pode ajudá-lo anexando o seguinte **PexUseTypeAttribute** a seguir ao teste (ou a classe de acessório):

  ```csharp
  [PexMethod]
  [PexUseType(typeof(System.Collections.Hashtable))]
  public void MyTest(IDictionary[] dictionaries) { ... }
  ```

* **Um atributo de nível de assembly**

  ```csharp
  [assembly: PexUseType(typeof(System.Collections.Hashtable))]
  ```

<a name="usable-type-guessed"></a>
## <a name="usable-type-guessed"></a>Tipo utilizável estimado

O IntelliTest [gera as entradas de teste](input-generation.md) para qualquer tipo de .NET. Quando um tipo é abstrato ou uma interface, o IntelliTest deve escolher uma implementação específica desse tipo. Para fazer essa escolha, é necessário saber quais são os tipos existentes.

Quando este aviso é exibido, ele indica que o IntelliTest procurava algum dos assemblies referenciados e encontrou um tipo de implementação, mas não tem certeza de se ele deve usar esse tipo ou se já tipos mais adequados disponíveis em outro lugar. IntelliTest simplesmente escolhe um tipo que pareceu promissor.

Para evitar este aviso, você pode aceitar a escolha de tipo do IntelliTest ou ajudar o IntelliTest no uso de outros tios adicionando um [PexUseType](attribute-glossary.md#pexusetype) correspondente.

<a name="unexpected-exploration"></a>
## <a name="unexpected-failure-during-exploration"></a>Falha inesperada durante a exploração

Foi detectada uma exceção inesperada ao explorar um teste.

[Relatar isso como um bug](#report-bug).

<a name="targetinvocationexception"></a>
## <a name="targetinvocationexception"></a>TargetInvocationException

Ocorreu uma exceção no código do usuário. Inspecione o rastreamento de pilha e remova o bug em seu código.

<a name="uninstrumented-method-called"></a>
## <a name="uninstrumented-method-called"></a>Método não instrumentado chamado

O IntelliTest [gera entradas de teste](input-generation.md) monitorando a execução do programa. É essencial que o código relevante seja corretamente instrumentado para que o IntelliTest possa monitorar seu comportamento.

Esse aviso é exibido quando o código instrumentado chama métodos em outro assembly não instrumentado.
Se quiser que o IntelliTest explore a interação de ambos, você também deverá instrumentar o outro assembly (ou partes dele).

<a name="external-method-called"></a>
## <a name="external-method-called"></a>Método externo chamado

O IntelliTest [gera entradas de teste](input-generation.md) monitorando a execução dos aplicativos .NET.
O IntelliTest não pode gerar entradas de teste significativas para o código que não é escrito em uma linguagem .NET.

Esse aviso é exibido quando o código instrumentado chama um método nativo não gerenciado que o IntelliTest não pode analisar. Se você quiser que o IntelliTest explore a interação de ambos, você deverá simular o método não gerenciado.

<a name="uninstrumentable-method-called"></a>
## <a name="uninstrumentable-method-called"></a>Método não instrumentável chamado

O IntelliTest [gera entradas de teste](input-generation.md) monitorando a execução dos aplicativos .NET. No entanto, há alguns métodos que, por motivos técnicos, o IntelliTest não pode monitorar. Por exemplo, o IntelliTest não pode monitorar um construtor estático.

Esse aviso é exibido quando o código instrumentado chama um método que o IntelliTest não pode monitorar.

<a name="testability-issue"></a>
## <a name="testability-issue"></a>Problema de capacidade de teste

O IntelliTest [gera entradas de teste](input-generation.md) monitorando a execução do programa. Ele só pode gerar entradas de teste relevantes quando o programa é determinístico e quando o comportamento relevante é controlado pelas entradas de teste.

Esse aviso aparece porque, durante a execução do seu caso de teste, foi chamado um método que se comporta de forma não determinística ou interage com o ambiente. Os exemplos são métodos de **System.Random** e **System.IO.File**. Se quiser que o IntelliTest crie entradas de teste significativas, você deverá simular os métodos que o IntelliTest sinaliza como problemas de capacidade de teste.

<a name="limitation"></a>
## <a name="limitation"></a>Limitação

O IntelliTest [gera as entradas de teste](input-generation.md) usando um [solver de restrição](input-generation.md#constraint-solver).
No entanto, existem algumas operações que estão além do escopo do [solver de restrição](input-generation.md#constraint-solver).
Atualmente isso inclui:

* a maioria das operações de ponto flutuante (apenas um pouco de aritmética linear tem suporte em números de ponto flutuante)
* conversões entre os números de ponto flutuante e inteiros
* todas as operações do tipo **System.Decimal**

Esse aviso aparece quando o código executado realiza uma operação ou chama um método que o IntelliTest não pode interpretar.

<a name="observed-call-mismatch"></a>
## <a name="observed-call-mismatch"></a>Incompatibilidade de chamada observada

O IntelliTest [gera entradas de teste](input-generation.md) monitorando a execução do programa. No entanto, o IntelliTest pode não ser capaz de monitorar todas as instruções. Por exemplo, ele não pode monitorar o código nativo e não pode monitorar o código que não está instrumentado.

Quando o IntelliTest não pode monitorar o código, ele não pode gerar entradas de teste relevantes para o código.
Geralmente, o IntelliTest não está ciente do fato de que ele não pode monitorar um método até que uma chamada para esse método retorne. No entanto, a causa esse aviso é:

* O IntelliTest monitorou um pouco de código, o que iniciou uma chamada para um método não instrumentado
* O método não instrumentado chamou um método instrumentado
* O IntelliTest monitora o método instrumentado que foi chamado

O IntelliTest não sabe o que o método intermediário não instrumentado fez, portanto, ele pode não ser capaz de gerar entradas de teste relevantes para a chamada instrumentada aninhada.

<a name="value-static-field"></a>
## <a name="value-stored-in-static-field"></a>Valor armazenado no campo estático

O IntelliTest pode determinar sistematicamente as [entradas de teste relevantes](input-generation.md) apenas quando o teste de unidade é determinístico, em outras palavras, ele se comporta da mesma forma para as mesmas entradas de teste. Em particular, isso significa que o teste deve deixar o sistema em um estado que permite executar esse teste novamente.
Em condições ideais, o teste de unidade não deve alterar nenhum estado global, mas todas as interações com globais devem ser simuladas.

Esse aviso indica que um campo estático foi alterado, isso pode fazer com que o teste se comporte de forma não determinística.

Em algumas situações, a alteração de um campo estático é aceitável:

* quando as entradas de teste fazem com que a configuração ou o código de limpeza desfaça a alteração
* quando o campo é iniciado apenas uma vez e o valor não muda posteriormente

<a name="report-bug"></a>

## <a name="got-feedback"></a>Recebeu comentários?

Poste suas ideias e solicitações de recursos na [Comunidade de Desenvolvedores](https://developercommunity.visualstudio.com/content/idea/post.html?space=8).