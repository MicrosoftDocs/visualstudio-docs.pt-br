---
title: Executar testes de unidade em extensões UML | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 745d74ae-e48c-4fd9-a755-4354b81b9f8a
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 6ba485b40beb82db9ea8cfe573cb6d9e6742ecea
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51817315"
---
# <a name="run-unit-tests-on-uml-extensions"></a>Executar testes de unidade em extensões UML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para ajudar a manter o código estável ao longo de sucessivas alterações, recomendamos que você escreva testes de unidade e execute-os como parte de um processo de compilação regular. Para obter mais informações, consulte [Efetuar teste de unidade em seu código](../test/unit-test-your-code.md). Para configurar testes para extensões de modelagem do Visual Studio, você precisa de algumas informações importantes. Em resumo:  
  
- [Configurando um teste de unidade para extensões VSIX](#Host)  
  
   Execute testes com o adaptador host do IDE do VS. Prefixe cada método de teste com `[HostType("VS IDE")]`. Esse adaptador host inicia o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] quando você executa os testes.  
  
- [Acessando o DTE e ModelStore](#DTE)  
  
   Normalmente, você terá que abrir um modelo e seus diagramas e acessar o `IModelStore` na inicialização do teste.  
  
- [Abrindo um diagrama de modelo](#Opening)  
  
   Você pode converter `EnvDTE.ProjectItem` para e do `IDiagramContext`.  
  
- [Executando alterações no Thread da interface do usuário](#UiThread)  
  
   Os testes que fazem alterações no repositório de modelo devem ser executados no thread de interface do usuário. Você pode usar o `Microsoft.VSSDK.Tools.VsIdeTesting.UIThreadInvoker` para essa finalidade.  
  
- [Testando comandos, gestos e outros componentes do MEF](#MEF)  
  
   Para testar os componentes do MEF, você deve conectar explicitamente as propriedades deles importadas aos valores.  
  
  Esses pontos são elaborados nas seguintes seções.  
  
  Um exemplo de uma extensão UML testada de unidade pode ser encontrado na Galeria de exemplos de código em [UML – Rapid Entry by usando texto](http://code.msdn.microsoft.com/UML-Rapid-Entry-using-Text-0813ad8a).  
  
## <a name="requirements"></a>Requisitos  
 Ver [requisitos de](../modeling/extend-uml-models-and-diagrams.md#Requirements).  
  
 Para ver quais versões do Visual Studio dão suporte a esse recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
##  <a name="Host"></a> Configurando um teste de unidade para extensões VSIX  
 Os métodos em suas extensões de modelagem geralmente trabalham com um diagrama que já está aberto. Os métodos usam importações MEF como **IDiagramContext** e **ILinkedUndoContext**. O seu ambiente de teste deve configurar este contexto antes de executar os testes.  
  
#### <a name="to-set-up-a-unit-test-that-executes-in-includevsprvsincludesvsprvs-mdmd"></a>Para configurar um teste de unidade que execute em [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]  
  
1.  Crie o projeto de extensão UML e o projeto de teste de unidade.  
  
    1.  **Um projeto de extensão UML.** Normalmente você criá-lo usando o comando, gesto ou modelos de projeto de validação. Por exemplo, consulte [definir um comando de menu em um diagrama de modelagem](../modeling/define-a-menu-command-on-a-modeling-diagram.md).  
  
    2.  **Um projeto de teste de unidade.** Para obter mais informações, consulte [Efetuar teste de unidade em seu código](../test/unit-test-your-code.md).  
  
2.  Criar uma solução [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] que contém um projeto de modelagem UML. Você usará esta solução como o estado inicial de seus testes. Ela deve ser à parte da solução na qual você escreve a extensão UML e os testes de unidade dela. Para obter mais informações, consulte [diagramas e projetos de modelagem UML criar](../modeling/create-uml-modeling-projects-and-diagrams.md).  
  
3.  **No projeto de extensão UML**, edite o arquivo. csproj como texto e verifique se as linhas a seguir mostram `true`:  
  
    ```  
    <CopyBuildOutputToOutputDirectory>true</CopyBuildOutputToOutputDirectory>  
        <CopyOutputSymbolsToOutputDirectory>true</CopyOutputSymbolsToOutputDirectory>  
    ```  
  
     Para editar o arquivo. csproj como texto, escolha **descarregar projeto** no menu de atalho do projeto no Gerenciador de soluções. Em seguida, escolha **editar... csproj**. Depois de editar o texto, escolha **recarregar projeto**.  
  
4.  No seu projeto de extensão UML, adicione a seguinte linha ao **Properties\AssemblyInfo.cs**. Isso permite que os testes de unidade acessem os métodos que você quer testar:  
  
    ```csharp  
    [assembly:InternalsVisibleTo("MyUnitTests")] // Name of unit tests assembly.  
    ```  
  
5.  **No projeto de teste de unidade**, adicione as seguintes referências de assembly:  
  
    -   *Seu projeto de extensão UML*  
  
    -   **EnvDTE.dll**  
  
    -   **Microsoft.VisualStudio.ArchitectureTools.Extensibility.dll**  
  
    -   **Microsoft.VisualStudio.ComponentModelHost.dll**  
  
    -   **UnitTestFramework**  
  
    -   **VisualStudio**  
  
    -   **Microsoft.VSSDK.TestHostFramework.dll**  
  
6.  Prefixe o atributo `[HostType("VS IDE")]` para cada método de teste, incluindo os métodos de inicialização.  
  
     Isso garantirá que o teste será executado em uma instância experimental do Visual Studio.  
  
##  <a name="DTE"></a> Acessando o DTE e ModelStore  
 Escreva um método para abrir um projeto de modelagem no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Normalmente, você deseja abrir uma solução apenas uma vez em cada teste. Para executar o método apenas uma vez, prefixe o método com o atributo `[AssemblyInitialize]`. Lembre-se de que você também precisa do atributo [HostType("VS IDE")] em cada método de teste.  Por exemplo:  
  
```csharp  
using EnvDTE;  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility;  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;  
using Microsoft.VisualStudio.TestTools.UnitTesting;  
using Microsoft.VSSDK.Tools.VsIdeTesting;  
  
namespace UnitTests  
{  
  [TestClass]  
  public static class TestSetup  
  {  
  
    // Location of a VS Solution that defines an initial state for your tests:  
    private const string testSolutionFilePath = @"C:\MyTestFolder\TestModelSln\TestModel.sln";  
    // Name of a modeling project within the test solution:  
    private const string testModelingProjectName = "MyTestModel";  
  
    // Make Solution and IModelStore available to test methods:  
    public static Solution ModelSolution = null;  
    public static IModelingProject ModelingProject = null;  
    public static IModelStore ModelStore = null;  
  
    // This method will be performed once to initialize tests for this assembly:  
    [AssemblyInitialize]   
    [HostType("VS IDE")]  
    public static void OpenTestModelingProject(TestContext testContext)  
    {  
      // To make sure that we always start the tests in the same state,  
      // copy the test solution from a read-only directory:  
      // TODO: copy test solution folder.  
  
      // Open a solution that is the initial state for your tests:  
      ModelSolution = VsIdeTestHostContext.Dte.Solution;  
      ModelSolution.Open(testSolutionFilePath);  
  
      // Find the ModelingProject and IModelStore:  
      foreach (Project project in ModelSolution.Projects)  
      {  
        // http://msdn.microsoft.com/library/ee791691.aspx  
        ModelingProject = project as IModelingProject;  
        if (ModelingProject != null)  
        {  
          // This is a modeling project.  
          ModelStore = ModelingProject.Store;  
          break;  
        }  
        // else this is another kind of project.  
      }  
  
      Assert.IsNotNull(ModelSolution, "VS solution not found");  
      Assert.IsNotNull(ModelStore, "Modeling store not found");  
    }  
    [AssemblyCleanup]  
    public static void RemoveTestSolution ()  
    {  
      // TODO: Remove copied test solution directory.  
    }  
  }  
}  
  
```  
  
 Se uma instância de <xref:EnvDTE.Project?displayProperty=fullName> representa um projeto de modelagem, você pode convertê-la para e do <xref:Microsoft.VisualStudio.ArchitectureTools.Extensibility.IModelingProject>.  
  
##  <a name="Opening"></a> Abrindo um diagrama de modelo  
 Para cada teste ou classe de testes, normalmente você trabalha com um diagrama aberto. O exemplo a seguir usa o atributo `[ClassInitialize]`, que executa esse método antes de outros métodos nessa classe de teste. Lembre-se de que você também precisa do atributo [HostType("VS IDE")] em cada método de teste:  
  
```csharp  
//   
private IDiagram diagram;  
// This class contains unit tests:  
[TestClass]  
public class MyTestClass  
{  
  // Map filenames to open diagram files:  
  private static Dictionary<string, IDiagram> diagrams = new Dictionary<string, IDiagram>();  
  
  // This method will be called once for this test class:  
  [ClassInitialize]  
  [HostType("VS IDE")]  
  public static void TestClassInitialize(TestContext testContext)  
  {  
    // Open all the diagrams in the model:  
    foreach (ProjectItem item in (TestSetup.ModelingProject as Project).ProjectItems)  
    {  
      // Get the filename of the principal file (not the .layout subsidiary):  
      string fileName = item.FileNames[0];  
      // If this is a model diagram file, it can be cast to IDiagramContext:  
      IDiagramContext modelingItem = item as IDiagramContext;  
      if (modelingItem != null)  
      {  
        IDiagram diagram = modelingItem.CurrentDiagram;  
        if (diagram == null)  
        {  
          // Diagram is closed. Open it:  
          item.Open().Activate();  
          diagram = modelingItem.CurrentDiagram;  
        }  
        diagrams[fileName] = diagram;  
      }  
      // else item is not a model diagram.  
    }  
    Assert.IsTrue(diagrams.Count>0, "UML diagram not found");  
  }  
// Insert test methods here ...  
}  
  
```  
  
##  <a name="UiThread"></a> Executar alterações no Thread da interface do usuário  
 Se os testes ou os métodos em teste alterarem o modelo do repositório, execute-os no thread da interface do usuário. Caso contrário, você poderá ver uma `AccessViolationException`. Inclua o código do método de teste em uma chamada para invocar:  
  
```  
using System.Windows.Forms;  
using Microsoft.VSSDK.Tools.VsIdeTesting;  
 ...  
    [TestMethod]  
    [HostType("VS IDE")]  
    public void MyTest1()  
    {  
      // Store operations must run in the UI thread:  
      UIThreadInvoker.Invoke((System.Action)delegate()  
      {  
        SetupTestState(TestSetup.ModelStore, diagram);  
        ExecuteMethodUnderTest(TestSetup.ModelStore, diagram);  
      });  
    }  
```  
  
##  <a name="MEF"></a> Testando comandos, gestos e outros componentes do MEF  
 Os componentes MEF usam declarações de propriedades que têm o atributo `[Import]` e cujos valores são definidos por seus hosts. Normalmente, essas propriedades incluem IDiagramContext, SVsServiceProvider e ILinkedUndoContext. Quando você testar um método que usa qualquer uma dessas propriedades, você precisa definir os valores delas antes de executar o método em teste. Por exemplo, se você escreveu uma extensão de comando parecida com este código:  
  
```  
  
  [Export(typeof(ICommandExtension))]  
  [ClassDesignerExtension]  
  class MyCommand : ICommandExtension  
  {  
    [Import] IDiagramContext context { get; set; }  
    [Import]   
Microsoft.VisualStudio.Shell.SVsServiceProvider  
serviceProvider {get;set;}  
    [Import] ILinkedUndoContext linkedUndoContext { get; set; }  
    public void Execute(IMenuCommand command)  
    {  
      DoCommand();  
    }  
    private void DoCommand()  
    {  
      IDiagram diagram = context.CurrentDiagram;  
      using (ILinkedUndoTransaction t = linkedUndoContext.BeginTransaction("go"))  
      { ... }}}  
  
```  
  
 Em seguida, você pode definir as propriedades importadas da seguinte forma:  
  
```  
  
using System.ComponentModel.Composition;  
using Microsoft.VisualStudio.ComponentModelHost;   
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;  
using Microsoft.VisualStudio.TestTools.UnitTesting;  
using Microsoft.VSSDK.Tools.VsIdeTesting;  
...  
    [TestMethod]   
    [HostType("VS IDE")]  
    public void Test1()  
    {  
      // Create an instance of the class under test:  
      MyCommand myCommand = new MyCommand();  
      // Get the components service:  
      IComponentModel components = VsIdeTestHostContext.ServiceProvider  
        .GetService(typeof(SComponentModel)) as IComponentModel;  
      // Set the imported properties of the instance under test:  
      // Extension requires "using System.ComponentModel.Composition;" :  
      components.DefaultCompositionService.SatisfyImportsOnce(myCommand);  
      // Call method(s) under test:  
      UIThreadInvoker.Invoke((System.Action)delegate()  
      {  
        myCommand.DoCommand();  
      });  
...}  
```  
  
 Se quiser testar um método que usa uma propriedade importada como um parâmetro, você pode importar a propriedade em sua classe de teste e aplicar `SatisfyImportsOnce` à instância de teste. Por exemplo:  
  
```  
  
using System.ComponentModel.Composition;  
...  
  [TestClass]  
  public class MyTestClass  
  {  
    [Import] ILinkedUndoContext linkedUndoContext { get; set; }  
  
    // Called before each test method:  
    [TestInitialize, HostType("VS IDE")]   
    public void TestInitializer()  
    {  
      IComponentModel components = VsIdeTestHostContext.ServiceProvider  
            .GetService(typeof(SComponentModel)) as IComponentModel;  
      // Extension requires "using System.ComponentModel.Composition;" :  
      components.DefaultCompositionService.SatisfyImportsOnce(this);  
    }  
    [TestMethod, HostType("VS IDE")]  
    public void Test2()  
    {   
     UIThreadInvoker.Invoke((System.Action)delegate()  
      {  
      // Pass context items to class under test:  
      Class1 item1 = new Class1(this.linkedUndoContext);  
      item1.Method1(); // Can use linkedUndoContext  
     });  
   }  
}  
  
```  
  
 Neste exemplo, os dois atributos de cada método de teste são combinados por conveniência em uma linha.  
  
## <a name="access-from-tests-to-private-methods-and-variables"></a>Acesso a partir de testes a métodos e variáveis particulares  
 Às vezes, você precisa testar um método particular ou verificar o estado de um campo particular, antes e depois de executar um método em teste. Isso representa uma dificuldade porque os testes estão em um assembly separado das classes em teste. Há várias táticas que você pode considerar, incluindo as seguintes:  
  
 Testar apenas usando itens públicos e internos  
 Escrever seus testes para que eles usem apenas classes e membros públicos (ou internos). Essa é a melhor abordagem. Os testes continuarão a funcionar mesmo se você refatorar a implementação interna do assembly em teste. Aplicando os mesmos testes antes e após as alterações, você pode ter certeza de que suas alterações não alteraram o comportamento do assembly.  
  
 Para tornar isso possível, talvez você tenha que reestruturar seu código. Por exemplo, você pode precisar separar alguns métodos em outra classe.  
  
 Ao considerar essa abordagem, normalmente você perceberá que o código ficou mais fácil de ler e de alterar, e menos propenso a erros quando houver necessidade de fazer alterações.  
  
 Você pode permitir que o assembly de teste acesse itens internos, adicionando um atributo em **Properties\AssemblyInfo.cs** no projeto a ser testado:  
  
```csharp  
[assembly:InternalsVisibleTo("MyUnitTests")] // Name of unit tests assembly.  
```  
  
 Definir uma interface de teste  
 Defina uma interface que inclua os membros públicos de uma classe a ser testada e propriedades e métodos adicionais para os membros particulares que você deseja que os testes usem. Adicione esta interface ao projeto a ser testado. Por exemplo:  
  
```csharp  
internal interface MyClassTestInterface {  
  void PublicMethod1();  
  string PublicProperty1 { get; }  
  string privateField1_Accessor { get; }  
  int privateMethod1_Accessor (string p1);   
 }  
```  
  
 Adicione métodos à classe a ser testada, para implementar os métodos de acesso explicitamente. Mantenha esses métodos adicionais separados da classe principal, escrevendo-os em uma definição de classe parcial em um arquivo separado. Por exemplo:  
  
```csharp  
partial public class MyClass  
{  
  string MyClassTestInterface.privateField1_Accessor  
  { get { return privateField1; } }  
  int MyClassTestInterface.privateMethod1_Accessor (string p1)  
  { return privateMethod1(p1); }  
}  
  
```  
  
 Permita que o assembly de teste use as interfaces de teste, adicionando esse atributo ao assembly que você está testando:  
  
```csharp  
[assembly:InternalsVisibleTo("MyUnitTests")] // Name of unit tests assembly.  
```  
  
 Nos métodos de teste de unidade, use a interface de teste. Por exemplo:  
  
```csharp  
MyClassTestInterface testInstance = new MyClass();  
testInstance.PublicMethod1();  
Assert.AreEqual("hello", testInstance.privateField1_Accessor);  
```  
  
 Definir acessadores usando reflexão  
 Essa é a maneira menos recomendada. As versões mais antigas do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] forneciam um utilitário que criava automaticamente um método de acesso para cada método particular. Embora seja conveniente, a nossa experiência indica que eles tendem a resultar em testes de unidade que são muito acoplados à estrutura interna do aplicativo que estão testando. Isso acarreta trabalho adicional quando os requisitos ou a arquitetura mudam, pois você precisa alterar os testes com a implementação. Além disso, todas as suposições incorretas no projeto de implementação também são compiladas nos testes, para que os testes não encontrem erros.  
  
## <a name="see-also"></a>Consulte também  
 [Anatomia de um teste de unidade](http://msdn.microsoft.com/en-us/a03d1ee7-9999-4e7c-85df-7d9073976144)   
 [Definir um comando de menu em um diagrama de modelagem](../modeling/define-a-menu-command-on-a-modeling-diagram.md)   
 [UML – Rapid Entry by usando texto](http://code.msdn.microsoft.com/UML-Rapid-Entry-using-Text-0813ad8a)



