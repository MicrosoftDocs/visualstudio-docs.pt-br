---
title: Limites de exploração | Ferramenta de teste para desenvolvedores do Microsoft IntelliTest
ms.date: 05/02/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: reference
helpviewer_keywords:
- IntelliTest, Exploration bounds
ms.author: gewarren
manager: douge
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: 9d1ac08a2314119c924417191ca509a4bcd18021
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51000640"
---
# <a name="exploration-bounds"></a>Limites de exploração

**PexSettingsAttributeBase** é a classe base abstrata para definir limites como atributos. Consulte [Cascata de configurações](settings-waterfall.md) para obter uma visão geral das configurações no IntelliTest.

Você pode modificar as configurações usando propriedades nomeadas deles e seus atributos derivados:

```csharp
[PexClass(MaxRuns = 10)]
public partial class FooTest {...}
```

* **Limites de resolução de restrição**
  * [MaxConstraintSolverTime](#maxconstraintsolvertime) – o número de segundos que o [solver de restrição](input-generation.md#constraint-solver) tem para descobrir entradas que farão com que um caminho de execução novo e diferente seja seguido.
  * [MaxConstraintSolverMemory](#maxconstraintsolvermemory) – o tamanho em megabytes que o [solver de restrição](input-generation.md#constraint-solver) pode usar para descobrir as entradas.<p />
* **Limites de caminho de exploração**
  * [MaxBranches](#maxbranches) – o número máximo de branches que podem ser seguidos ao longo de um único caminho de execução.
  * [MaxCalls](#maxcalls) – o número máximo de chamadas que podem ser feitas durante um único caminho de execução.
  * [MaxStack](#maxstack) – o tamanho máximo da pilha a qualquer momento durante um único caminho de execução, medido como o número de quadros de chamada ativa.
  * [MaxConditions](#maxconditions) – o número máximo de condições sobre as entradas que podem ser verificadas durante um único caminho de execução.<p />
* **Limites de Exploração**
  * [MaxRuns](#maxruns) – o número máximo de execuções que serão tentadas durante uma exploração.
  * [MaxRunsWithoutNewTests](#maxrunswithoutnewtests) – o número máximo de execuções consecutivas sem um novo teste ser emitido.
  * [MaxRunsWithUniquePaths](#maxrunswithuniquepaths) – o número máximo de execuções com caminhos de execução exclusivos que serão tentadas durante uma exploração.
  * [MaxExceptions](#maxexceptions) – o número máximo de exceções que podem ser encontradas para uma combinação de todos os caminhos de execução descobertos.<p />
* **Configurações de geração de código de conjunto de testes**
  * [TestExcludePathBoundsExceeded](#testexcludepathboundsexceeded) – quando true, os caminhos de execução que excederem qualquer um dos limites de caminho ([MaxCalls](#maxcalls), [MaxBranches](#maxbranches), [MaxStack](#maxstack), [MaxConditions](#maxconditions)) serão ignorados.
  * [TestEmissionFilter](#testemissionfilter) – indica sob quais circunstâncias o IntelliTest deverá emitir testes.
  * [TestEmissionBranchHits](#testemissionbranchhits) – controla quantos testes o IntelliTest emite.

<a name="maxconstraintsolvertime"></a>
## <a name="maxconstraintsolvertime"></a>MaxConstraintSolverTime

O número de segundos que o [solver de restrição](input-generation.md#constraint-solver) tem para calcular entradas que farão com que um caminho de execução novo e diferente seja seguido. Essa é uma opção do **PexSettingsAttributeBase** e seus tipos derivados.

Quanto mais o IntelliTest explora os caminhos de execução de um programa, mais complexos se tornam os sistemas de restrições que o IntelliTest cria do fluxo de controle e do fluxo de dados do programa. Dependendo de seu limite de tempo, você pode definir esse valor para permitir que o IntelliTest leve mais ou menos tempo descobrindo novos caminhos de execução.

Normalmente, o motivo para um tempo limite é que o IntelliTest está tentando encontrar uma solução para um sistema de restrição que não tem uma solução, mas não está ciente desse fato. Como esse é o caso mais comum para um tempo limite, talvez não faça sentido aumentar o limite.

<a name="maxconstraintsolvermemory"></a>
## <a name="maxconstraintsolvermemory"></a>MaxConstraintSolverMemory

O número de megabytes que o [solver de restrição](input-generation.md#constraint-solver) tem para calcular entradas que farão com que um caminho de execução novo e diferente seja seguido. Essa é uma opção do *PexSettingsAttributeBase** e de seus tipos derivados.

Quanto mais o IntelliTest explora os caminhos de execução de um programa, mais complexos se tornam os sistemas de restrições que o IntelliTest cria do fluxo de controle e do fluxo de dados do programa. Dependendo da memória disponível do computador, você pode definir esse valor para permitir que o IntelliTest lide com sistemas de restrição mais complexos.

Normalmente, o motivo para um tempo limite é que o IntelliTest está tentando encontrar uma solução para um sistema de restrição que não tem uma solução, mas não está ciente desse fato. Como essa é a causa mais comum de uma situação de falta de memória, talvez não faça sentido aumentar o limite.

<a name="maxbranches"></a>
## <a name="maxbranches"></a>MaxBranches

O número máximo de branches que podem ser seguidos ao longo de um único caminho de execução.

A motivação por trás desse limite de exploração é limitar o comprimento de qualquer caminho de execução que o IntelliTest explore durante a [geração de entrada](input-generation.md). Em particular, ela impede que o IntelliTest deixe de responder se o programa entrar em um loop infinito.

Cada branch condicional e incondicional do código executado e monitorado é contada até esse limite, inclusive branches que não dependem das entradas do teste parametrizado.

Por exemplo, o código a seguir consome branches na ordem de 100:

```csharp
for (int i=0; i<100; i++) { }
```

<a name="maxcalls"></a>
## <a name="maxcalls"></a>MaxCalls

O número máximo de chamadas que podem ser feitas durante um único caminho de execução.

A motivação por trás desse limite de exploração é limitar o comprimento de qualquer caminho de execução que o IntelliTest explore durante a [geração de entrada](input-generation.md). Em particular, ela impedirá que o IntelliTest deixar de responder se o programa chamar um método recursivamente um número infinito de vezes, o que poderia causar um excedente de pilha do qual o IntelliTest não pode se recuperar.

Cada chamada (direta, indireta, virtual, pulo) do código executado e monitorado é contada até esse limite.

<a name="maxstack"></a>
## <a name="maxstack"></a>MaxStack

O tamanho máximo da pilha a qualquer momento durante um único caminho de execução, medido pelo número de quadros de chamada ativa.

A motivação por trás desse limite de exploração é limitar o tamanho da pilha de qualquer caminho de execução que o IntelliTest explore durante a [geração de entrada](input-generation.md). Em particular, ela impedirá que o IntelliTest use todo o espaço de pilha disponível, o que causaria um excedente de pilha do qual o IntelliTest não pode se recuperar.

<a name="maxconditions"></a>
## <a name="maxconditions"></a>MaxConditions

O número máximo de condições sobre as entradas que podem ser verificadas durante um único caminho de execução.

A motivação por trás desse limite de exploração é limitar a complexidade de qualquer caminho de execução que o IntelliTest explore durante a [geração de entrada](input-generation.md). Cada branch condicional que depende das entradas do teste parametrizado é contada até esse limite.

Por exemplo, cada caminho no código a seguir consome n+1 condições:

```csharp
[PexMethod]
void ParameterizedTest(int n) 
{
     for (int i=0; i<n; i++) { // conditions are "0<n", "1<n", ..., "!(n<n)"
          ...
     }
     for (int i=0; i<100; i++) { // irrelevant for MaxConditions, since conditions do not depend on input
          ...
     }
}
```

<a name="maxruns"></a>
## <a name="maxruns"></a>MaxRuns

O número máximo de execuções que o IntelliTest tentará durante a exploração de um teste.

A motivação por trás desse limite de exploração é que qualquer código que contenha loops ou recursão pode ter um número infinito de caminhos de execução e, portanto, o IntelliTest precisa ser limitado durante a [geração de entrada](input-generation.md).

As duas configurações **MaxRuns** e **MaxRunsWithUniquePaths** são relacionadas da seguinte maneira:

* O IntelliTest chamará um método de teste parametrizado até **MaxRuns** vezes com diferentes entradas de teste.
* Se o código executado for determinístico, o IntelliTest seguirá um caminho de execução diferente cada vez. No entanto, em algumas condições o código executado pode seguir um caminho de execução que já usado antes, com entradas diferentes.
* O IntelliTest conta quantos caminhos de execução exclusivos ele encontra, esse número é limitado pela opção **MaxRunsWithUniquePaths**.

<a name="maxrunswithoutnewtests"></a>
## <a name="maxrunswithoutnewtests"></a>MaxRunsWithoutNewTests

O número máximo de execuções consecutivas sem um novo teste ser emitido.

Embora o IntelliTest possa localizar muitas entradas de teste interessantes em um curto período, após alguns instantes ele não localizará mais nenhuma nova entrada de teste e não emitirá mais testes de unidade. Essa opção de configuração coloca um limite no número de tentativas consecutivas que o IntelliTest pode executar sem emitir um novo teste. Quando atingido, ele interromperá a exploração.

<a name="maxrunswithuniquepaths"></a>
## <a name="maxrunswithuniquepaths"></a>MaxRunsWithUniquePaths

O número máximo de caminhos exclusivos que o IntelliTest considerará durante uma exploração.

A motivação por trás desse limite de exploração é que qualquer código que contenha loops ou recursão pode ter um número infinito de caminhos de execução e, portanto, o IntelliTest deve ser limitado durante a [geração de entrada](input-generation.md).

As duas configurações **MaxRuns** e **MaxRunsWithUniquePaths** são relacionadas da seguinte maneira: 

* O IntelliTest chamará um método de teste parametrizado até **MaxRuns** vezes com diferentes entradas de teste.
* Se o código executado for determinístico, o IntelliTest seguirá um caminho de execução diferente cada vez. No entanto, em algumas condições o código executado pode seguir um caminho de execução que já usado antes, com entradas diferentes. 
* O IntelliTest conta quantos caminhos de execução exclusivos ele encontra, esse número é limitado pela opção **MaxRunsWithUniquePaths**.

<a name="maxexceptions"></a>
## <a name="maxexceptions"></a>MaxExceptions

O número máximo de exceções que podem ser encontradas antes de a exploração ser interrompida.

A motivação por trás desse limite de exploração é parar a exploração do código que contém muitos bugs. Se o IntelliTest encontra muitos erros no código, exploração é interrompida.

<a name="testexcludepathboundsexceeded"></a>
## <a name="testexcludepathboundsexceeded"></a>TestExcludePathBoundsExceeded

Os caminhos de execução que excederam os limites de caminho configurados [MaxCalls](#maxcalls), [MaxBranches](#maxbranches), [MaxStack](#maxstack) e [MaxConditions](#maxconditions) são ignorados.

A motivação por trás desse limite da exploração é lidar com testes (provavelmente) sem finalização. Quando o IntelliTest atinge um limite de exploração como [MaxCalls](#maxcalls), [MaxBranches](#maxbranches), [MaxStack](#maxstack) ou [MaxConditions](#maxconditions), ele assume que o teste não será um processo sem finalização e não causará um excedente de pilha posteriormente. Esses casos de teste podem causar problemas para outras estruturas de teste e esse atributo fornece uma maneira de impedir que o IntelliTest emita casos de teste para processos potencialmente sem finalização ou casos de teste que causarão um excedente de pilha.

<a name="testemissionfilter"></a>
## <a name="testemissionfilter"></a>TestEmissionFilter

Indica os tipos de testes que o IntelliTest deve emitir. Os valores possíveis são:

* **All** – emitir testes para tudo, inclusive violações de suposição.
* **FailuresAndIncreasedBranchHits** (padrão) – emitir testes para todas as falhas exclusivas e sempre que um caso de teste aumentar a cobertura conforme controlado por [TestEmissionBranchHits](#testemissionbranchhits).
* **FailuresAndUniquePaths** – emitir testes para todas as falhas que IntelliTest encontrar e também para cada entrada de teste que produz um caminho de execução exclusivo.
* **Failures** – Emitir testes apenas para falhas.

<a name="testemissionbranchhits"></a>
## <a name="testemissionbranchhits"></a>TestEmissionBranchHits

Dependendo da configuração [TestEmissionFilter](#testemissionfilter) atual, o IntelliTest emite novos casos de teste ao abranger um branch no programa que não foi abrangido antes.

A configuração **TestEmissionBranchHits** determina se o IntelliTest deve apenas considerar se um branch foi abrangido em absoluto (**TestEmissionBranchHits=1**), se um teste o abrangeu uma ou duas vezes (**TestEmissionBranchHits=2**) e assim por diante.

**TestEmissionBranchHits = 1** produzirá um conjunto de testes muito pequeno que abrangerá todos os branches que o IntelliTest puder atingir. Em particular, esse conjunto de testes também abrangerá todos os blocos básicos e instruções que ele atingiu.

O padrão para essa opção é **TestEmissionBranchHits = 2**, que gera um conjunto de testes mais expressivo que também é mais adequado para detectar erros de regressão futuros.

## <a name="got-feedback"></a>Recebeu comentários?

Poste suas ideias e solicitações de recursos na [Comunidade de Desenvolvedores](https://developercommunity.visualstudio.com/content/idea/post.html?space=8).
