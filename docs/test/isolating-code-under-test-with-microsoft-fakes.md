---
title: Isolando código em teste com falsificação da Microsoft
description: Saiba como as falsificações da Microsoft ajudam a isolar o código que você está testando, substituindo outras partes do aplicativo por stubs ou shims.
ms.custom: SEO-VS-2020
ms.date: 06/03/2020
ms.topic: how-to
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
author: mikejo5000
dev_langs:
- VB
- CSharp
ms.openlocfilehash: 8800116393df30df59b9fbe9544c1bbd0ee1bc18
ms.sourcegitcommit: 6d88913a8b5a9e5eda01d3f95205b4d138f440f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/13/2021
ms.locfileid: "107295644"
---
# <a name="isolate-code-under-test-with-microsoft-fakes"></a>Isolar o código em teste com elementos fictícios da Microsoft

O Microsoft Fakes ajuda a isolar o código em teste substituindo outras partes do aplicativo por *stubs* ou *shims*. Esses são pequenos trechos de código sob o controle de seus testes. Ao isolar seu código para teste, você sabe que se o teste falhar, a causa está lá e não em outro lugar. Stubs e shims também permitem que você teste seu código mesmo que outras partes do aplicativo ainda não estejam funcionando.

O Fakes vem em duas versões:

- Um [stub](#get-started-with-stubs) substitui uma classe por um pequeno substituto que implementa a mesma interface.  Para usar stubs, você precisa criar seu aplicativo de modo que cada componente dependa apenas das interfaces, e não de outros componentes. (Por “componente”, queremos dizer uma classe ou um grupo de classes que são criadas e atualizadas em conjunto e normalmente estão contidas em um assembly.)

- Um [shim](#get-started-with-shims) modifica o código compilado do aplicativo no tempo de execução para que, em vez de fazer uma chamada de método específica, ele execute o código shim que fornecido pelo teste. Os shims podem ser usados para substituir chamadas para assemblies que você não pode modificar, como assemblies do .NET.

![As falsificações substituem outros componentes](../test/media/fakes-2.png)

**Requirements**

- Visual Studio Enterprise
- Um projeto do .NET Framework
::: moniker range=">=vs-2019"
- O .NET Core, o .NET 5,0 e o projeto em estilo SDK oferecem suporte à visualização no Visual Studio 2019 atualização 6 e são habilitados por padrão na atualização 8. Para obter mais informações, consulte [falsificações da Microsoft para projetos do estilo SDK e do .NET Core](/visualstudio/releases/2019/release-notes#microsoft-fakes-for-net-core-and-sdk-style-projects).
::: moniker-end

> [!NOTE]
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

   1. Em **Gerenciador de soluções**, 
       - Para um projeto de .NET Framework mais antigo (estilo não SDK), expanda o nó **referências** do seu projeto de teste de unidade.
       ::: moniker range=">=vs-2019"
       - Para um projeto no estilo SDK direcionado a .NET Framework, .NET Core ou .NET 5,0, expanda o nó **dependências** para localizar o assembly que você gostaria de falsificar em **assemblies**, **projetos** ou **pacotes**.
       ::: moniker-end
       - Se você estiver trabalhando em Visual Basic, selecione **Mostrar todos os arquivos** na barra de ferramentas **Gerenciador de soluções** para ver o nó **referências** .
   2. Selecione o assembly que contém as definições de classe para as quais você deseja criar shims. Por exemplo, se você quiser corrigir **DateTime**, selecione **System.dll**.

   3. No menu de atalhos, escolha **Adicionar Assembly do Fakes**.

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

    A parte especial da mágica aqui é a classe `StubIStockFeed`. Para cada interface no assembly referenciado, o mecanismo Microsoft Fakes gera uma classe de stub. O nome da classe de stub é derivado do nome da interface, com " `Fakes.Stub` " como um prefixo e os nomes de tipo de parâmetro anexados.

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

## <a name="using-microsoft-fakes-in-the-ci"></a>Usando falsificações da Microsoft no CI

### <a name="microsoft-fakes-assembly-generation"></a>Geração de assembly de falsificações da Microsoft
Como as falsificações da Microsoft exigem Visual Studio Enterprise, a geração de assemblies de falsificações exige que você crie seu projeto usando a [tarefa de compilação do Visual Studio](/azure/devops/pipelines/tasks/build/visual-studio-build?view=azure-devops&preserve-view=true).

::: moniker range=">=vs-2019"
> [!NOTE]
> Uma alternativa para isso é verificar os assemblies de falsificações no CI e usar a [tarefa MSBuild](../msbuild/msbuild-task.md?view=vs-2019&preserve-view=true). Ao fazer isso, você precisa garantir que você tenha uma referência de assembly para o assembly de falsificações gerado em seu projeto de teste, semelhante ao seguinte trecho de código:

```xml
<Project Sdk="Microsoft.NET.Sdk">
    <ItemGroup>
        <Reference Include="FakesAssemblies\System.Fakes.dll"/>
    </ItemGroup>
</Project>
```

Essa referência é necessária para ser adicionada em projetos de estilo de SDK especificamente específicos (.NET Core, .NET 5,0 e .NET Framework) porque mudamos para adicionar implicitamente referências de assembly ao seu projeto de teste. Se você seguir esse método, precisará garantir que o assembly de falsificações seja atualizado quando o assembly pai for alterado.
::: moniker-end

### <a name="running-microsoft-fakes-tests"></a>Executando testes de falsificações da Microsoft
Desde que os assemblies de falsificações da Microsoft estejam presentes no `FakesAssemblies` diretório configurado (o padrão está sendo `$(ProjectDir)FakesAssemblies` ), você pode executar testes usando a [tarefa VSTest](/azure/devops/pipelines/tasks/test/vstest?view=azure-devops&preserve-view=true).

::: moniker range=">=vs-2019"
Os testes distribuídos com os projetos .NET Core e .NET 5,0 da [tarefa VSTest](/azure/devops/pipelines/tasks/test/vstest?view=azure-devops&preserve-view=true) usando falsificações da Microsoft exigem o Visual Studio 2019 atualização 9 Preview `20201020-06` e superior.
::: moniker-end

::: moniker range=">=vs-2019"
## <a name="transitioning-your-net-framework-test-projects-that-use-microsoft-fakes-to-sdk-style-net-framework-net-core-or-net-50-projects"></a>Transição de seus projetos de teste de .NET Framework que usam falsificações da Microsoft para projetos do estilo SDK .NET Framework, .NET Core ou .NET 5,0
Você precisará de alterações mínimas em seu .NET Framework configurado para que os falsificadores da Microsoft façam a transição para o .NET Core ou o .NET 5,0. Os casos que você teria que considerar são:
- Se você estiver usando um modelo de projeto personalizado, precisará garantir que ele seja o estilo do SDK e seja compilado para uma estrutura de destino compatível.
- Alguns tipos existem em assemblies diferentes no .NET Framework e no .NET Core/. NET 5,0 (por exemplo, `System.DateTime` existe no `System` / `mscorlib` .NET Framework e no `System.Runtime` .NET Core e no .NET 5,0), e nesses cenários você precisa alterar o assembly que está sendo falsificado.
- Se você tiver uma referência de assembly para um assembly de falsificações e o projeto de teste, você poderá ver um aviso de compilação sobre uma referência ausente semelhante a:
  ```
  (ResolveAssemblyReferences target) ->
  warning MSB3245: Could not resolve this reference. Could not locate the assembly "AssemblyName.Fakes". Check to make sure the assembly exists on disk.
  If this reference is required by your code, you may get compilation errors.
  ```
  Esse aviso se deve às alterações necessárias feitas na geração de falsificações que podem ser ignoradas. Ele pode ser evitado com a remoção da referência de assembly do arquivo de projeto, pois agora as adicionamos implicitamente durante a compilação.
::: moniker-end

## <a name="microsoft-fakes-support"></a>Suporte a falsificações da Microsoft 
### <a name="microsoft-fakes-in-older-projects-targeting-net-framework-non-sdk-style"></a>Falsificações da Microsoft em projetos mais antigos direcionados a .NET Framework (estilo não-SDK).
- A geração de assembly de falsificações da Microsoft tem suporte no Visual Studio Enterprise 2015 e superior.
- Os testes de falsificações da Microsoft podem ser executados com todos os pacotes NuGet Microsoft. TestPlatform disponíveis.
- A cobertura de código tem suporte para projetos de teste que usam falsificações da Microsoft no Visual Studio Enterprise 2015 e superior.

### <a name="microsoft-fakes-in-sdk-style-net-framework-net-core-and-net-50-projects"></a>Microsoft falsificações nos projetos .NET Framework, .NET Core e .NET 5,0 no estilo SDK
- A geração de assembly de falsificações da Microsoft visualizada no Visual Studio Enterprise 2019 atualização 6 e é habilitada por padrão na atualização 8.
- Os testes de falsificações da Microsoft para projetos direcionados .NET Framework podem ser executados com todos os pacotes NuGet Microsoft. TestPlatform disponíveis.
- Os testes de falsificações da Microsoft para projetos direcionados para .NET Core e .NET 5,0 podem ser executados com pacotes NuGet Microsoft. TestPlatform com versões [16.9.0-Preview-20210106-01](https://www.nuget.org/packages/Microsoft.TestPlatform/16.9.0-preview-20210106-01) e superiores.
- A cobertura de código tem suporte para projetos de teste destinados a .NET Framework usando falsificações da Microsoft no Visual Studio Enterprise versão 2015 e superior.
- O suporte à cobertura de código para projetos de teste destinados ao .NET Core e ao .NET 5,0 usando falsificações da Microsoft está disponível no Visual Studio 2019 atualização 9 e superior.


## <a name="in-this-section"></a>Nesta seção
[Usar stubs para isolar partes do aplicativo para teste de unidade](../test/using-stubs-to-isolate-parts-of-your-application-from-each-other-for-unit-testing.md)

[Usar shims para isolar seu aplicativo de outros assemblies para teste de unidade](../test/using-shims-to-isolate-your-application-from-other-assemblies-for-unit-testing.md)

[Geração de código, compilação e convenções de nomenclatura no Microsoft Fakes](../test/code-generation-compilation-and-naming-conventions-in-microsoft-fakes.md)
