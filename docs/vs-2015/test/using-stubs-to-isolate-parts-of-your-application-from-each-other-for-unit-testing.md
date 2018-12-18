---
title: Uso de stubs para isolar partes do seu aplicativo para teste de unidade | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 73519dd9-f3d5-49b6-a634-38881b459ea4
caps.latest.revision: 19
ms.author: gewarren
manager: douge
ms.openlocfilehash: cc12f77a8f1c3443606537dd6f818e9ee6625327
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49853175"
---
# <a name="using-stubs-to-isolate-parts-of-your-application-from-each-other-for-unit-testing"></a>Usando stubs para isolar partes de seu aplicativo para teste de unidade
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Tipos de stub * são uma das duas tecnologias que o Microsoft Fakes framework fornece para permitir que você isole facilmente um componente que você está testando de outros componentes que ele chama. Um stub é um pequeno trecho de código que ocupa o lugar de outro componente durante o teste. A vantagem de usar um stub é que ele retorna resultados consistentes, tornando mais fácil escrever o teste. E você pode executar testes mesmo se os outros componentes não estiverem funcionando ainda.  
  
 Para obter uma visão geral e início rápido guia Fakes, confira [Isolamento de código em teste com Microsoft Fakes](../test/isolating-code-under-test-with-microsoft-fakes.md).  
  
 Para usar stubs, você precisa escrever seu componente de forma que ele use apenas interfaces, não classes, para referenciar outras partes do aplicativo. Essa é uma boa prática de design porque faz alterações em uma parte com menor probabilidade de exigir alterações em outra. Em testes, permite que você substitua um stub de um componente real.  
  
 No diagrama, o componente StockAnalyzer é aquele que desejamos testar. Ele geralmente usa outro componente, RealStockFeed. Mas RealStockFeed retorna resultados diferentes sempre que seus métodos são chamados, dificultando o teste do StockAnalyzer.  Durante o teste, nós o substituímos por uma classe diferente, StubStockFeed.  
  
 ![As classes de stub e real em conformidade com uma interface. ](../test/media/fakesinterfaces.png "FakesInterfaces")  
  
 Como os stubs dependem de sua capacidade de estruturar seu código dessa forma, normalmente você usará stubs para isolar uma parte do aplicativo de outra. Para isolá-lo de outros assemblies que não estão sob seu controle, como System.dll, você normalmente usaria shims. Confira o artigo [Uso de shims para isolar o seu aplicativo de outros assemblies para o teste de unidade](../test/using-shims-to-isolate-your-application-from-other-assemblies-for-unit-testing.md).  
  
 **Requisitos**  
  
-   Visual Studio Enterprise  
  
## <a name="in-this-topic"></a>Neste tópico  
  
-   [Como usar stubs](#how)  
  
    -   [Projeto para injeção de dependência](#Dependency)  
  
    -   [Como gerar stubs](#GeneratingStubs)  
  
    -   [Como escrever seu teste com stubs](#WriteTest)  
  
    -   [Verificação de valores de parâmetros](#mocks)  
  
-   [Stubs para tipos diferentes de membros de tipo](../test/using-stubs-to-isolate-parts-of-your-application-from-each-other-for-unit-testing.md#BKMK_Stub_basics)  
  
    -   [Métodos](../test/using-stubs-to-isolate-parts-of-your-application-from-each-other-for-unit-testing.md#BKMK_Methods)  
  
    -   [Propriedades](../test/using-stubs-to-isolate-parts-of-your-application-from-each-other-for-unit-testing.md#BKMK_Properties)  
  
    -   [Eventos](../test/using-stubs-to-isolate-parts-of-your-application-from-each-other-for-unit-testing.md#BKMK_Events)  
  
    -   [Métodos genéricos](../test/using-stubs-to-isolate-parts-of-your-application-from-each-other-for-unit-testing.md#BKMK_Generic_methods)  
  
    -   [Stubs de classes virtuais](../test/using-stubs-to-isolate-parts-of-your-application-from-each-other-for-unit-testing.md#BKMK_Partial_stubs)  
  
-   [Depuração de stubs](../test/using-stubs-to-isolate-parts-of-your-application-from-each-other-for-unit-testing.md#BKMK_Debugging_stubs)  
  
-   [Limitações de stub](../test/using-stubs-to-isolate-parts-of-your-application-from-each-other-for-unit-testing.md#BKMK_Stub_limitation)  
  
-   [Alteração do comportamento padrão de stubs](../test/using-stubs-to-isolate-parts-of-your-application-from-each-other-for-unit-testing.md#BKMK_Changing_the_default_behavior_of_stubs)  
  
##  <a name="How"></a> Como usar o stubs  
  
###  <a name="Dependency"></a> Projetado para injeção de dependência  
 Para usar stubs, seu aplicativo precisa ser criado de forma que os diferentes componentes não sejam dependentes um do outro, mas apenas dependentes das definições de interface. Em vez de ser acoplados no tempo de compilação, os componentes são conectados no tempo de execução. Esse padrão ajuda a criar um software robusto e fácil de atualizar, pois as alterações tendem a não ser propagadas além dos limites dos componentes. Recomendamos segui-lo mesmo que você não use stubs. Se você está escrevendo um código novo, siga o padrão [Injeção de dependência](http://en.wikipedia.org/wiki/Dependency_injection). Se você está escrevendo testes para um software existente, talvez seja necessário refatorá-lo. Caso isso seja impraticável, você pode considerar o uso de shims.  
  
 Vamos começar esta discussão com um exemplo motivador, aquele do diagrama. A classe StockAnalyzer lê preços de ações e gera alguns resultados interessantes. Ela tem alguns métodos públicos, que queremos testar. Para simplificar as coisas, vamos conferir apenas um desses métodos, um muito simples que informa o preço atual de uma ação específica. Queremos escrever um teste de unidade desse método. Este é o primeiro rascunho de um teste:  
  
```csharp  
[TestMethod]  
public void TestMethod1()  
{  
    // Arrange:  
    var analyzer = new StockAnalyzer();  
    // Act:  
    var result = analyzer.GetContosoPrice();  
    // Assert:  
    Assert.AreEqual(123, result); // Why 123?  
}  
```  
  
```vb  
<TestMethod()> Public Sub TestMethod1()  
    ' Arrange:  
    Dim analyzer = New StockAnalyzer()  
    ' Act:  
    Dim result = analyzer.GetContosoPrice()  
    ' Assert:  
    Assert.AreEqual(123, result) ' Why 123?  
End Sub  
```  
  
 Um problema com esse teste imediatamente é óbvio: os preços das ações variam e, portanto, a asserção normalmente falhará.  
  
 Outro problema pode ser que o componente StockFeed, que é usado pelo StockAnalyzer, ainda esteja em desenvolvimento. Este é o primeiro rascunho do código do método em teste:  
  
```csharp  
public int GetContosoPrice()  
{  
    var stockFeed = new StockFeed(); // NOT RECOMMENDED  
    return stockFeed.GetSharePrice("COOO");  
}  
```  
  
```vb  
Public Function GetContosoPrice()  
    Dim stockFeed = New StockFeed() ' NOT RECOMMENDED  
    Return stockFeed.GetSharePrice("COOO")  
End Function  
```  
  
 Assim, esse método pode não compilar ou pode gerar uma exceção porque o trabalho na classe StockFeed ainda não foi concluído.  
  
 A injeção de interface soluciona esses dois problemas.  
  
 A injeção de interface aplica a seguinte regra:  
  
- O código de qualquer componente de seu aplicativo nunca deve se referir explicitamente a uma classe de outro componente, em uma declaração ou em uma instrução `new`. Em vez disso, as variáveis e os parâmetros devem ser declarados com interfaces. As instâncias do componente devem ser criadas somente pelo contêiner do componente.  
  
   Nesse caso, “componente” significa uma classe ou um grupo de classes que você desenvolve e atualiza em conjunto. Normalmente, um componente é o código em um projeto do Visual Studio. É menos importante desacoplar classes em um componente, pois elas são atualizadas ao mesmo tempo.  
  
   Também não é tão importante desacoplar seus componentes das classes de uma plataforma relativamente estável, como System.dll. Escrever interfaces para todas essas classes obstruiria seu código.  
  
  O código StockAnalyzer pode, portanto, ser melhorado desacoplando-o do StockFeed usando uma interface como esta:  
  
```csharp  
public interface IStockFeed  
{  
    int GetSharePrice(string company);  
}  
  
public class StockAnalyzer  
{  
    private IStockFeed stockFeed;  
    public Analyzer(IStockFeed feed)  
    {  
        stockFeed = feed;  
    }  
    public int GetContosoPrice()  
    {  
        return stockFeed.GetSharePrice("COOO");  
    }  
}  
```  
  
```vb  
Public Interface IStockFeed  
    Function GetSharePrice(company As String) As Integer  
End Interface  
  
Public Class StockAnalyzer  
    ' StockAnalyzer can be connected to any IStockFeed:  
    Private stockFeed As IStockFeed  
    Public Sub New(feed As IStockFeed)  
        stockFeed = feed  
    End Sub    
    Public Function GetContosoPrice()  
        Return stockFeed.GetSharePrice("COOO")  
    End Function  
End Class  
  
```  
  
 Neste exemplo, StockAnalyzer é passado para uma implementação de um IStockFeed quando é construído. No aplicativo concluído, o código de inicialização faria a conexão:  
  
```  
analyzer = new StockAnalyzer(new StockFeed())  
```  
  
 Há maneiras mais flexíveis de fazer essa conexão. Por exemplo, StockAnalyzer poderia aceitar um objeto factory capaz de instanciar implementações diferentes de IStockFeed em condições diferentes.  
  
###  <a name="GeneratingStubs"></a> Como gerar stubs  
 Você desacoplou a classe que deseja testar dos outros componentes que ela usa. Além de tornar o aplicativo mais robusto e flexível, desacoplar permite conectar o componente em teste às implementações de stubs das interfaces para fins de teste.  
  
 Você poderia simplesmente escrever os stubs como classes da maneira usual. Mas o Microsoft Fakes fornece uma maneira mais dinâmica de criar o stub mais adequado para cada teste.  
  
 Para usar stubs, você deve primeiro gerar tipos de stub a partir das definições de interface.  
  
##### <a name="adding-a-fakes-assembly"></a>Adicionando um assembly do Fakes  
  
1.  No Gerenciador de Soluções, expanda as **Referências** de seu projeto de teste de unidade.  
  
    -   Se você estiver trabalhando no Visual Basic, selecione **Mostrar Todos os Arquivos** na barra de ferramentas do Gerenciador de Soluções para ver a lista Referências.  
  
2.  Selecione o assembly que contém as definições de interface para as quais você deseja criar stubs.  
  
3.  No menu de atalhos, escolha **Adicionar Assembly do Fakes**.  
  
###  <a name="WriteTest"></a> Como escrever seu teste com stubs  
  
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
  
 A parte especial da mágica aqui é a classe `StubIStockFeed`. Para cada tipo público no assembly referenciado, o mecanismo Microsoft Fakes gera uma classe de stub. O nome da classe stub é derivado do nome da interface, com "`Fakes.Stub`" como prefixo e os nomes dos tipos de parâmetro anexados.  
  
 Os stubs também são gerados para getters e setters de propriedades, para eventos e métodos genéricos.  
  
###  <a name="mocks"></a> Verifique os valores de parâmetros  
 Você pode verificar que, quando seu componente chama outro componente, ele passa os valores corretos. Você pode colocar uma asserção no stub ou armazenar o valor e verificá-lo no corpo principal do teste. Por exemplo:  
  
```csharp  
[TestClass]  
class TestMyComponent  
{  
  
    [TestMethod]  
    public void TestVariableContosoPrice()  
    {  
     // Arrange:  
        int priceToReturn;  
        string companyCodeUsed;  
        var componentUnderTest = new StockAnalyzer(new StubIStockFeed()  
            {  
               GetSharePriceString = (company) =>   
                  {   
                     // Store the parameter value:  
                     companyCodeUsed = company;  
                     // Return the value prescribed by this test:  
                     return priceToReturn;  
                  };  
            };  
        // Set the value that will be returned by the stub:  
        priceToReturn = 345;  
  
     // Act:  
        int actualResult = componentUnderTest.GetContosoPrice();  
  
     // Assert:  
        // Verify the correct result in the usual way:  
        Assert.AreEqual(priceToReturn, actualResult);  
  
        // Verify that the component made the correct call:  
        Assert.AreEqual("COOO", companyCodeUsed);  
    }  
...}  
  
```  
  
```vb  
<TestClass()> _  
Class TestMyComponent  
    <TestMethod()> _  
    Public Sub TestVariableContosoPrice()  
        ' Arrange:  
        Dim priceToReturn As Integer  
        Dim companyCodeUsed As String = ""  
        Dim stockFeed As New StockAnalysis.Fakes.StubIStockFeed()  
        With stockFeed  
            ' Implement the interface's method:  
            .GetSharePriceString = _  
                Function(company)  
                    ' Store the parameter value:  
                    companyCodeUsed = company  
                    ' Return a fixed result:  
                    Return priceToReturn  
                End Function  
        End With  
        ' Create an object to test:  
        Dim componentUnderTest As New StockAnalyzer(stockFeed)  
        ' Set the value that will be returned by the stub:  
        priceToReturn = 345  
  
        ' Act:  
        Dim actualResult As Integer = componentUnderTest.GetContosoPrice()  
  
        ' Assert:  
        ' Verify the correct result in the usual way:  
        Assert.AreEqual(priceToReturn, actualResult)  
        ' Verify that the component made the correct call:  
        Assert.AreEqual("COOO", companyCodeUsed)  
    End Sub  
...  
End Class  
```  
  
##  <a name="BKMK_Stub_basics"></a>Stubs para tipos diferentes de membros de tipo  
  
###  <a name="BKMK_Methods"></a> Métodos  
 Conforme descrito no exemplo, é possível fazer o stub dos métodos anexando um delegado a uma instância da classe stub. O nome do tipo de stub é derivado dos nomes do método e dos parâmetros. Por exemplo, dada a interface `IMyInterface` e o método `MyMethod` a seguir:  
  
```csharp  
// application under test  
interface IMyInterface   
{  
    int MyMethod(string value);  
}  
```  
  
 Anexamos um stub a `MyMethod` que sempre retorna 1:  
  
```csharp  
// unit test code  
  var stub = new StubIMyInterface ();  
  stub.MyMethodString = (value) => 1;  
  
```  
  
 Se você não fornecer um stub para uma função, o Fakes gerará uma função que retorna o valor padrão do tipo de retorno. Para números, o valor padrão é 0, e para tipos de classe é `null` (C#) ou `Nothing` (Visual Basic).  
  
###  <a name="BKMK_Properties"></a> Propriedades  
 Os getters e setters de propriedade são expostos como delegados separados e podem passar por stub separadamente. Por exemplo, considere a propriedade `Value` de `IMyInterface`:  
  
```csharp  
// code under test  
interface IMyInterface   
{  
    int Value { get; set; }  
}  
  
```  
  
 Anexamos delegados ao getter e ao setter de `Value` para simular uma autopropriedade:  
  
```csharp  
// unit test code  
int i = 5;  
var stub = new StubIMyInterface();  
stub.ValueGet = () => i;  
stub.ValueSet = (value) => i = value;  
  
```  
  
 Se você não fornecer métodos stub para o setter ou o getter de uma propriedade, o Fakes gerará um stub que armazena valores, para que a propriedade stub funcione como uma variável simples.  
  
###  <a name="BKMK_Events"></a> Eventos  
 Os eventos são expostos como campos delegados. Portanto, qualquer evento de stub pode ser gerado simplesmente invocando o campo de suporte do evento. Vamos considerar a seguinte interface para stub:  
  
```csharp  
// code under test  
interface IWithEvents   
{  
    event EventHandler Changed;  
}  
```  
  
 Para gerar o evento `Changed`, simplesmente invocamos o delegado de suporte:  
  
```csharp  
// unit test code  
  var withEvents = new StubIWithEvents();  
  // raising Changed  
  withEvents.ChangedEvent(withEvents, EventArgs.Empty);  
  
```  
  
###  <a name="BKMK_Generic_methods"></a> Métodos genéricos  
 É possível fazer o stub de métodos genéricos fornecendo um delegado para cada instanciação desejada do método. Por exemplo, dada a seguinte interface que contém um método genérico:  
  
```csharp  
// code under test  
interface IGenericMethod   
{  
    T GetValue<T>();  
}  
```  
  
 você poderia escrever um teste que faz o stub da instanciação de `GetValue<int>`:  
  
```csharp  
// unit test code  
[TestMethod]  
public void TestGetValue()   
{  
    var stub = new StubIGenericMethod();  
    stub.GetValueOf1<int>(() => 5);  
  
    IGenericMethod target = stub;  
    Assert.AreEqual(5, target.GetValue<int>());  
}  
```  
  
 Se o código fosse chamar `GetValue<T>` com qualquer outra instanciação, o stub simplesmente chamaria o comportamento.  
  
###  <a name="BKMK_Partial_stubs"></a> Stubs de classes virtuais  
 Nos exemplos anteriores, os stubs foram gerados a partir de interfaces. Você também pode gerar stubs a partir de uma classe que tenha membros virtuais ou abstratos. Por exemplo:  
  
```csharp  
// Base class in application under test  
    public abstract class MyClass  
    {  
        public abstract void DoAbstract(string x);  
        public virtual int DoVirtual(int n)  
        { return n + 42; }  
        public int DoConcrete()  
        { return 1; }  
    }  
```  
  
 No stub gerado a partir dessa classe, você pode definir métodos delegados para DoAbstract() e DoVirtual(), mas não DoConcrete().  
  
```csharp  
// unit test  
  var stub = new Fakes.MyClass();  
  stub.DoAbstractString = (x) => { Assert.IsTrue(x>0); };  
  stub.DoVirtualInt32 = (n) => 10 ;  
  
```  
  
 Se você não fornecer um delegado para um método virtual, o Fakes poderá fornecer o comportamento padrão ou chamar o método na classe base. Para ter o método base chamado, defina a propriedade `CallBase`:  
  
```csharp  
// unit test code  
var stub = new Fakes.MyClass();  
stub.CallBase = false;  
// No delegate set – default delegate:  
Assert.AreEqual(0, stub.DoVirtual(1));  
  
stub.CallBase = true;  
//No delegate set - calls the base:  
Assert.AreEqual(43,stub.DoVirtual(1));  
```  
  
##  <a name="BKMK_Debugging_stubs"></a> Depuração de stubs  
 Os tipos de stub são criados para oferecer uma experiência de depuração simples. Por padrão, o depurador é instruído a passar por cima de qualquer código gerado é ir diretamente para as implementações de membro personalizado que foram anexadas ao stub.  
  
##  <a name="BKMK_Stub_limitation"></a> Limitações de stub  
  
1.  Não há suporte para assinaturas de métodos com ponteiros.  
  
2.  Não é possível fazer o stub de classes fechadas ou métodos estáticos porque os tipos de stub dependem da distribuição virtual do método. Em casos como este, siga as instruções de [Uso de shims para isolar o aplicativo de outros assemblies para teste de unidade](../test/using-shims-to-isolate-your-application-from-other-assemblies-for-unit-testing.md) para usar os tipos de shim  
  
##  <a name="BKMK_Changing_the_default_behavior_of_stubs"></a> Alteração do comportamento padrão de stubs  
 Cada tipo de stub gerado contém uma instância da interface `IStubBehavior` (pela propriedade `IStub.InstanceBehavior`). O comportamento é chamado sempre que um cliente chama um membro sem delegado personalizado anexado. Se o comportamento não for definido, ele usará a instância retornada pela propriedade `StubsBehaviors.Current`. Por padrão, essa propriedade retorna um comportamento que gerou uma exceção `NotImplementedException`.  
  
 O comportamento pode ser alterado a qualquer momento definindo a propriedade `InstanceBehavior` em qualquer instância do stub. Por exemplo, o seguinte snippet altera um comportamento que não faz nada ou retorna o valor padrão do tipo de retorno: `default(T)`:  
  
```csharp  
// unit test code  
var stub = new StubIFileSystem();  
// return default(T) or do nothing  
stub.InstanceBehavior = StubsBehaviors.DefaultValue;  
```  
  
 O comportamento também pode ser modificado globalmente para todos os objetos stub para os quais o comportamento não foi definido na configuração da propriedade `StubsBehaviors.Current`:  
  
```csharp  
// unit test code  
//change default behavior for all stub instances  
//where the behavior has not been set  
StubBehaviors.Current =   
    BehavedBehaviors.DefaultValue;  
```  
  
## <a name="external-resources"></a>Recursos externos  
  
### <a name="guidance"></a>Diretrizes  
 [Testes de Entrega Contínua com o Visual Studio 2012 – Capítulo 2: Teste de Unidade: Testando o Interior](http://go.microsoft.com/fwlink/?LinkID=255188)  
  
## <a name="see-also"></a>Consulte também  
 [Isolando código em teste com Microsoft Fakes](../test/isolating-code-under-test-with-microsoft-fakes.md)



