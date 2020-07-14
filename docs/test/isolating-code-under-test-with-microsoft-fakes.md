---
title: Isolando código em teste com falsificação da Microsoft
ms.date: 06/03/2020
ms.topic: how-to
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
dev_langs:
- VB
- CSharp
ms.openlocfilehash: 49330132321c389fc5b6a4842972769896c72637
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85286954"
---
# <a name="isolate-code-under-test-with-microsoft-fakes"></a>Isolar o código em teste com elementos fictícios da Microsoft

O Microsoft Fakes ajuda a isolar o código em teste substituindo outras partes do aplicativo por *stubs* ou *shims*. Esses são pequenos trechos de código sob o controle de seus testes. Ao isolar seu código para teste, você sabe que se o teste falhar, a causa está lá e não em outro lugar. Stubs e shims também permitem que você teste seu código mesmo que outras partes do aplicativo ainda não estejam funcionando.

O Fakes vem em duas versões:

- Um [stub](#get-started-with-stubs) substitui uma classe por um pequeno substituto que implementa a mesma interface.  Para usar stubs, você precisa criar seu aplicativo de modo que cada componente dependa apenas das interfaces, e não de outros componentes. (Por “componente”, queremos dizer uma classe ou um grupo de classes que são criadas e atualizadas em conjunto e normalmente estão contidas em um assembly.)

- Um [shim](#get-started-with-shims) modifica o código compilado do aplicativo no tempo de execução para que, em vez de fazer uma chamada de método específica, ele execute o código shim que fornecido pelo teste. Os shims podem ser usados para substituir chamadas para assemblies que você não pode modificar, como assemblies do .NET.

![As falsificações substituem outros componentes](../test/media/fakes-2.png)

**Requisitos**

- Visual Studio Enterprise
- Um projeto do .NET Framework
- O suporte ao projeto de estilo SDK e .NET Core está atualmente em versão prévia. [Leia mais](https://docs.microsoft.com/visualstudio/releases/2019/release-notes#microsoft-fakes-for-net-core-and-sdk-style-projects)

> [!NOTE]
> - Projetos do .NET Standard não têm suporte.
> - A criação de perfil com o Visual Studio não está disponível para testes que usam o Microsoft Fakes.

## <a name="choose-between-stub-and-shim-types"></a>Escolher entre os tipos de stub e shim
Normalmente, você consideraria um projeto do Visual Studio para ser um componente, pois desenvolve e atualiza as classes ao mesmo tempo. Você poderia considerar o uso de stubs e shims para chamadas feitas pelo projeto para outros projetos em sua solução ou para outros assemblies que o projeto referencia.

Como guia geral, use stubs para chamadas em sua solução do Visual Studio, e shims para chamadas a outros assemblies referenciados. Isso é porque em sua própria solução é uma boa prática desacoplar os componentes definindo interfaces da maneira exigida pelo stub. Mas assemblies externos, como *System.dll* normalmente não são fornecidos com definições de interface separadas, portanto, você deve usar shims em vez disso.

Outras considerações são:

**Desempenho.** Os shims têm execução mais lenta porque reescrevem seu código no tempo de execução. Os stubs não têm essa sobrecarga de desempenho e são tão rápidos quanto os métodos virtuais.

**Métodos estáticos, tipos lacrados.** É possível usar stubs somente para implementar interfaces. Portanto, os tipos de stub não podem ser usados para métodos estáticos, métodos não virtuais, métodos virtuais lacrados, métodos em tipos lacrados e assim por diante.

**Tipos internos.** Os stubs e shims podem ser usados com tipos internos que são acessíveis com o atributo de assembly <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>.

**Métodos privados.** Os shims poderão substituir chamadas para métodos particulares se todos os tipos na assinatura do método estiverem visíveis. Os stubs só podem substituir métodos visíveis.

**Interfaces e métodos abstratos.** Os stubs oferecem implementações de interfaces e métodos abstratos que podem ser usados em testes. Os shims não podem instrumentar interfaces e métodos abstratos, porque eles não têm corpos de método.

Em geral, recomendamos que você use tipos de stub para isolar das dependências dentro de sua base de código. É possível fazer isso ocultando os componentes atrás das interfaces. Os tipos de shims podem ser usados para isolar de componentes de terceiros que não oferecem uma API testável.

## <a name="get-started-with-stubs"></a>Introdução aos stubs
Para obter uma descrição mais detalhada, confira [Usar stubs para isolar partes do aplicativo para teste de unidade](../test/using-stubs-to-isolate-parts-of-your-application-from-each-other-for-unit-testing.md).

1. **Injetar interfaces**

     Para usar stubs, você precisa escrever o código que deseja testar de forma que ele não mencione explicitamente as classes em outro componente de seu aplicativo. Por “componente”, queremos dizer uma classe ou um grupo de classes que são criadas e atualizadas em conjunto e normalmente estão contidas em um projeto do Visual Studio. As variáveis e os parâmetros devem ser declarados usando interfaces e instâncias de outros componentes que devem ser passados ou criados usando uma fábrica. Por exemplo, se StockFeed é uma classe em outro componente do aplicativo, ele é considerado incorreto:

     `return (new StockFeed()).GetSharePrice("COOO"); // Bad`

     Em vez disso, defina uma interface que possa ser implementada pelo outro componente, e que também possa ser implementada por um stub para fins de teste:

    ```csharp
    public int GetContosoPrice(IStockFeed feed) => feed.GetSharePrice("COOO");
    ```

    ```vb
    Public Function GetContosoPrice(feed As IStockFeed) As Integer
     Return feed.GetSharePrice("COOO")
    End Function

    ```

2. **Adicionar Assembly do Fakes**

    1. Em **Gerenciador de soluções**, expanda a lista de referência do projeto de teste. Se estiver trabalhando no Visual Basic, escolha **Mostrar Todos os Arquivos** para ver a lista de referências.

    2. Selecione a referência ao assembly em que a interface (por exemplo, IStockFeed) é definida. No menu de atalho dessa referência, escolha **Adicionar Assembly do Fakes**.

    3. Recriar a solução.

3. Em seus testes, construa instâncias do stub e forneça o código para seus métodos:

    ```csharp
    [TestClass]
    class TestStockAnalyzer
    {
        [TestMethod]
        public void TestContosoStockPrice()
        {
          // Arrange:

            // Create the fake stockFeed:
            IStockFeed stockFeed =
                 new StockAnalysis.Fakes.StubIStockFeed() // Generated by Fakes.
                     {
                         // Define each method:
                         // Name is original name + parameter types:
                         GetSharePriceString = (company) => { return 1234; }
                     };

            // In the completed application, stockFeed would be a real one:
            var componentUnderTest = new StockAnalyzer(stockFeed);

          // Act:
            int actualValue = componentUnderTest.GetContosoPrice();

          // Assert:
            Assert.AreEqual(1234, actualValue);
        }
        ...
    }
    ```

    ```vb
    <TestClass()> _
    Class TestStockAnalyzer

        <TestMethod()> _
        Public Sub TestContosoStockPrice()
            ' Arrange:
            ' Create the fake stockFeed:
            Dim stockFeed As New StockAnalysis.Fakes.StubIStockFeed
            With stockFeed
                .GetSharePriceString = Function(company)
                                           Return 1234
                                       End Function
            End With
            ' In the completed application, stockFeed would be a real one:
            Dim componentUnderTest As New StockAnalyzer(stockFeed)
            ' Act:
            Dim actualValue As Integer = componentUnderTest.GetContosoPrice
            ' Assert:
            Assert.AreEqual(1234, actualValue)
        End Sub
    End Class

    ```

    A parte especial da mágica aqui é a classe `StubIStockFeed`. Para cada interface no assembly referenciado, o mecanismo Microsoft Fakes gera uma classe de stub. O nome da classe stub é derivado do nome da interface, com "`Fakes.Stub`" como prefixo e os nomes dos tipos de parâmetro anexados.

    Os stubs também são gerados para getters e setters de propriedades, para eventos e métodos genéricos. Para obter mais informações, confira [Usar stubs para isolar partes do aplicativo para teste de unidade](../test/using-stubs-to-isolate-parts-of-your-application-from-each-other-for-unit-testing.md).

## <a name="get-started-with-shims"></a>Introdução aos shims
(Para obter uma descrição mais detalhada, confira [Usar shims para isolar o aplicativo de outros assemblies para o teste de unidade](../test/using-shims-to-isolate-your-application-from-other-assemblies-for-unit-testing.md).)

Suponhamos que seu componente contenha chamadas para `DateTime.Now`:

```csharp
// Code under test:
    public int GetTheCurrentYear()
    {
       return DateTime.Now.Year;
    }
```

Durante os testes, você gostaria de corrigir a propriedade `Now`, porque a versão real retorna inconvenientemente um valor diferente em cada chamada.

Para usar shims, você não precisa modificar o código do aplicativo ou escrevê-lo de uma maneira específica.

1. **Adicionar Assembly do Fakes**

     Em **Gerenciador de soluções**, abra as referências do projeto de teste de unidade e selecione a referência ao assembly que contém o método que você deseja falsificar. Nesse exemplo, a classe `DateTime` está em *System.dll*.  Para ver as referências em um projeto do Visual Basic, escolha **Mostrar Todos os Arquivos**.

     Escolha **Adicionar Assembly do Fakes**.

2. **Inserir um shim em um ShimsContext**

    ```csharp
    [TestClass]
    public class TestClass1
    {
            [TestMethod]
            public void TestCurrentYear()
            {
                int fixedYear = 2000;

                // Shims can be used only in a ShimsContext:
                using (ShimsContext.Create())
                {
                  // Arrange:
                    // Shim DateTime.Now to return a fixed date:
                    System.Fakes.ShimDateTime.NowGet =
                    () =>
                    { return new DateTime(fixedYear, 1, 1); };

                    // Instantiate the component under test:
                    var componentUnderTest = new MyComponent();

                  // Act:
                    int year = componentUnderTest.GetTheCurrentYear();

                  // Assert:
                    // This will always be true if the component is working:
                    Assert.AreEqual(fixedYear, year);
                }
            }
    }
    ```

    ```vb
    <TestClass()> _
    Public Class TestClass1
        <TestMethod()> _
        Public Sub TestCurrentYear()
            Using s = Microsoft.QualityTools.Testing.Fakes.ShimsContext.Create()
                Dim fixedYear As Integer = 2000
                ' Arrange:
                ' Detour DateTime.Now to return a fixed date:
                System.Fakes.ShimDateTime.NowGet = _
                    Function() As DateTime
                        Return New DateTime(fixedYear, 1, 1)
                    End Function

                ' Instantiate the component under test:
                Dim componentUnderTest = New MyComponent()
                ' Act:
                Dim year As Integer = componentUnderTest.GetTheCurrentYear
                ' Assert:
                ' This will always be true if the component is working:
                Assert.AreEqual(fixedYear, year)
            End Using
        End Sub
    End Class
    ```

    Os nomes das classes de shims são compostos pelo prefixo `Fakes.Shim` adicionado ao nome do tipo original. Os nomes dos parâmetros são acrescentados ao nome do método. (Você não precisa adicionar nenhuma referência ao assembly ao System.Fakes.)

O exemplo anterior usa um shim para um método estático. Para usar um shim para um método de instância, digite `AllInstances` entre o nome do tipo e o nome do método:

```vb
System.IO.Fakes.ShimFile.AllInstances.ReadToEnd = ...
```

(Não há nenhum assembly de 'System.IO.Fakes' para referência. O namespace é gerado pelo processo de criação de shim. Mas você pode usar 'using' ou 'Import' como de costume.)

Você também pode criar shims para instâncias específicas, para construtores e propriedades. Para obter mais informações, confira [Usar shims para isolar o aplicativo de outros assemblies para teste de unidade](../test/using-shims-to-isolate-your-application-from-other-assemblies-for-unit-testing.md).

## <a name="in-this-section"></a>Nesta seção
[Usar stubs para isolar partes do aplicativo para teste de unidade](../test/using-stubs-to-isolate-parts-of-your-application-from-each-other-for-unit-testing.md)

[Usar shims para isolar seu aplicativo de outros assemblies para teste de unidade](../test/using-shims-to-isolate-your-application-from-other-assemblies-for-unit-testing.md)

[Geração de código, compilação e convenções de nomenclatura no Microsoft Fakes](../test/code-generation-compilation-and-naming-conventions-in-microsoft-fakes.md)
