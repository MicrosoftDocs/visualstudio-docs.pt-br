---
title: Geração de teste | Ferramenta de teste para desenvolvedores do Microsoft IntelliTest
ms.date: 05/02/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- IntelliTest, Test generation
ms.author: gewarren
manager: douge
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: 20bacca2343cb2689ed52096c1a9b0d9c3d74703
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51295859"
---
# <a name="test-generation"></a>Geração de teste

Nos testes de unidade tradicionais, um teste de consiste em várias coisas:

* Uma [sequência de chamadas de método](test-generation.md#test-generators)
* Os argumentos com os quais os métodos são chamados. Os argumentos são as [entradas de teste](input-generation.md)
* Validação do comportamento pretendido do aplicativo testado informando um conjunto de [declarações](#assumptions-and-assertions)

A seguir está um exemplo de estrutura de teste:

```csharp
[Test]
void MyTest() {
    // data
    ArrayList a = new ArrayList();

    // method sequence
    a.Add(5);

    // assertions
    Assert.IsTrue(a.Count==1);
    Assert.AreEqual(a[0], 5);
}
```

O IntelliTest geralmente pode determinar valores de argumento relevantes para [Testes de Unidade Parametrizados](#parameterized-unit-testing) mais gerais, o que fornece a sequência das chamadas de método e declarações.

<a name="test-generators"></a>
## <a name="test-generators"></a>Geradores de teste

O IntelliTest gera casos de teste selecionando uma sequência de métodos de implementação em teste para executar e, em seguida, gerando entradas para os métodos durante a verificação de declarações sobre os dados derivados.

Um [teste de unidade parametrizado](#parameterized-unit-testing) determina diretamente uma sequência de chamadas de método em seu corpo.

Quando o IntelliTest precisa construir objetos, chamadas para construtores e métodos de fábrica serão adicionados automaticamente à sequência de conforme necessário.

<a name="parameterized-unit-testing"></a>
## <a name="parameterized-unit-testing"></a>Teste de unidade parametrizado

*PUTs* (Testes de Unidade Parametrizados) são testes que usam parâmetros. Ao contrário de testes de unidade tradicionais, que geralmente são métodos fechados, os PUTs utilizam qualquer conjunto de parâmetros. É simples assim? Sim, a partir daí, o IntelliTest tentará [gerar o conjunto de entradas (mínimo)](input-generation.md) que [abrange totalmente](input-generation.md#dynamic-code-coverage) o código acessível do teste.

Os PUTs são definidos usando o atributo personalizado [PexMethod](attribute-glossary.md#pexmethod) de forma semelhante ao MSTest (ou NUnit, xUnit). Os PUTs são métodos de instância agrupados logicamente em classes marcadas com [PexClass](attribute-glossary.md#pexclass). O exemplo a seguir mostra um PUT simples armazenado na classe **MyPexTest**:

```csharp
[PexMethod]
void ReplaceFirstChar(string target, char c) {

    string result = StringHelper.ReplaceFirstChar(target, c);

    Assert.AreEqual(result[0], c);
}
```

em que **ReplaceFirstChar** é um método que substitui o primeiro caractere de uma cadeia de caracteres:

```csharp
class StringHelper {
    static string ReplaceFirstChar(string target, char c) {
        if (target == null) throw new ArgumentNullException();
        if (target.Length == 0) throw new ArgumentOutOfRangeException();
        return c + target.Substring(1);
    }
}
```

Deste teste, o IntelliTest pode [gerar entradas](input-generation.md) automaticamente para um PUT que abrange muitos caminhos de execução do código testado. Cada entrada que abrange um caminho de execução diferente é “serializada” como um teste de unidade:

```csharp
[TestMethod, ExpectedException(typeof(ArgumentNullException))]
void ReplaceFirstChar0() {
    this.ReplaceFirstChar(null, 0);
}
...
[TestMethod]
void ReplaceFirstChar10() {
    this.ReplaceFirstChar("a", 'c');
}
```

<a name="generic-parameterized"></a>
## <a name="generic-parameterized-unit-testing"></a>Teste de unidade parametrizado genérico

Os testes de unidade parametrizados podem ser métodos genéricos. Nesse caso, o usuário deve especificar os tipos usados para criar a instância do método usando [PexGenericArguments](attribute-glossary.md#pexgenericarguments).

```csharp
[PexClass]
public partial class ListTest {
    [PexMethod]
    [PexGenericArguments(typeof(int))]
    [PexGenericArguments(typeof(object))]
    public void AddItem<T>(List<T> list, T value)
    { ... }
}
```

<a name="allowing-exceptions"></a>
## <a name="allowing-exceptions"></a>Permissão de exceções

O IntelliTest fornece vários atributos de validação para ajudar na triagem de exceções em exceções esperadas e exceções inesperadas.

As exceções esperadas geram casos de teste negativos com a anotação apropriada, como **ExpectedException(typeof(*xxx*))**, enquanto exceções inesperadas geram casos de teste com falha.

```csharp
[PexMethod, PexAllowedException(typeof(ArgumentNullException))]
void SomeTest() {...}
```

Os validadores são:

* [PexAllowedException](attribute-glossary.md#pexallowedexception): permite um determinado tipo de exceção de qualquer lugar
* [PexAllowedExceptionFromAssembly](attribute-glossary.md#pexallowedexceptionfromassembly): permite um determinado tipo de exceção de um assembly específico
* [PexAllowedExceptionFromType](attribute-glossary.md#pexallowedexceptionfromtype): permite um determinado tipo de exceção de um tipo específico
* [PexAllowedExceptionFromTypeUnderTest](attribute-glossary.md#pexallowedexceptionfromtypeundertest): permite um determinado tipo de exceção do tipo em teste

<a name="internal-types"></a>
## <a name="testing-internal-types"></a>Teste de tipos internos

O IntelliTest pode "testar" tipos internos, desde que ele pode vê-los. Para o IntelliTest ver os tipos, o seguinte atributo é adicionado ao seu projeto de teste ou produto pelos assistentes do IntelliTest do Visual Studio:

```csharp
[assembly: InternalsVisibleTo("Microsoft.Pex, PublicKey=002400000480000094000000060200000024000052534131000400000100010007d1fa57c4aed9f0a32e84aa0faefd0de9e8fd6aec8f87fb03766c834c99921eb23be79ad9d5dcc1dd9ad236132102900b723cf980957fc4e177108fc607774f29e8320e92ea05ece4e821c0a5efe8f1645c4c0c93c1ab99285d622caa652c1dfad63d745d6f2de5f17e5eaf0fc4963d261c8a12436518206dc093344d5ad293
```

<a name="assumptions-and-assertions"></a>
## <a name="assumptions-and-assertions"></a>Suposições e declarações

Os usuários podem usar suposições e declarações para expressar [pré-condições](#precondition) (suposições) e [pós-condições](#postcondition) (declarações) sobre seus testes. Quando o IntelliTest gera um conjunto de valores de parâmetro e “explora” o código, ele pode violar uma suposição do teste. Quando isso acontece, ele não gera um teste para esse caminho, mas silenciosamente o ignora.

As declarações são um conceito conhecido em estruturas de teste de unidade regulares, portanto o IntelliTest já "compreende" as classes **Assert** internas fornecidas por cada estrutura de teste com suporte. No entanto, a maioria das estruturas não fornece uma classe **Assume**. Nesse caso, o IntelliTest fornece a classe [PexAssume](static-helper-classes.md#pexassume). Se você não quiser usar uma estrutura de teste existente, o IntelliTest também terá a classe [PexAssert](static-helper-classes.md#pexassert).

```csharp
[PexMethod]
public void Test1(object o) {
    // precondition: o should not be null
    PexAssume.IsNotNull(o);

    ...
}
```

Em particular, a suposição não nula pode ser codificada como um atributo personalizado:

```csharp
[PexMethod]
public void Test2([PexAssumeNotNull] object o)
// precondition: o should not be null
{
   ...
}
```

<a name="precondition"></a>
## <a name="precondition"></a>Pré-condição

Uma pré-condição de um método expressa as condições sob as quais o método terá êxito.

Normalmente, a pré-condição é imposta verificando os parâmetros e o estado do objeto e lançando um **ArgumentException** ou **InvalidOperationException** se ela for violada.

No IntelliTest, uma pré-condição de um [teste de unidade parametrizado](#parameterized-unit-testing) é expresso com [PexAssume](static-helper-classes.md#pexassume).

<a name="postcondition"></a>
## <a name="postcondition"></a>Pós-condição

Uma pós-condição de um método expressa as condições que devem ser mantidas durante e após a execução do método, assumindo que suas pré-condições eram válidas inicialmente.

Normalmente, a pós-condição é imposta por chamadas para métodos **Assert**.

Com o IntelliTest uma pós-condição de um [teste de unidade parametrizado](#parameterized-unit-testing) é expressa com [PexAssert](static-helper-classes.md#pexassert).

<a name="test-failures"></a>
## <a name="test-failures"></a>Falhas de teste
Quando um caso de teste gerado falha?

1. Se ele não terminou dentro dos [limites de caminho configurados](exploration-bounds.md), ele é considerado como com falha a menos que a opção [TestExcludePathBoundsExceeded](exploration-bounds.md#testexcludepathboundsexceeded) esteja definida

1. Se o teste lança uma **PexAssumeFailedException**, ele é bem-sucedido. No entanto, isso geralmente é filtrado, a menos que [TestEmissionFilter](exploration-bounds.md#testemissionfilter) esteja definido como **All**

1. Se o teste viola uma [declaração](#assumptions-and-assertions), por exemplo, lançando uma exceção de violação de declaração de uma estrutura de teste de unidade, ele falha

Se nenhum deles produzir uma decisão, um teste terá êxito apenas se não lançar uma exceção. As violações de declaração são tratadas da mesma forma que as exceções.

<a name="setup-teardown"></a>
## <a name="setup-and-tear-down"></a>Configuração e desmontagem

Como parte da integração com estruturas de teste, o IntelliTest dá suporte à detecção e execução da configuração e montagem de métodos.

**Exemplo**

```csharp
using Microsoft.Pex.Framework;
using NUnit.Framework;

namespace MyTests
{
    [PexClass]
    [TestFixture]
    public partial class MyTestClass
    {
        [SetUp]
        public void Init()
        {
            // monitored
        }

        [PexMethod]
        public void MyTest(int i)
        {
        }

        [TearDown]
        public void Dispose()
        {
            // monitored
        }
    }
}
```

<a name="further-reading"></a>
## <a name="further-reading"></a>Leitura adicional

* [Test to code binding](https://blogs.msdn.microsoft.com/devops/2015/04/18/smart-unit-tests-test-to-code-binding-test-case-management/) (Teste para a associação de código)
* [One Test to rule them all](https://blogs.msdn.microsoft.com/devops/2015/07/05/intellitest-one-test-to-rule-them-all/) (Um teste para controlar todos)

## <a name="got-feedback"></a>Recebeu comentários?

Poste suas ideias e solicitações de recursos na [Comunidade de Desenvolvedores](https://developercommunity.visualstudio.com/content/idea/post.html?space=8).