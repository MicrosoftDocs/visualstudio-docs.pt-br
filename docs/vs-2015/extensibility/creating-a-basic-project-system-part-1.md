---
title: Criar um sistema de projeto básico, parte 1 | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- writing a project system
- project system
- tutorial
ms.assetid: 882a10fa-bb1c-4b01-943a-7a3c155286dd
caps.latest.revision: 48
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 9bc0be22f0a5f975f616bfcce942d59399a36ad6
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51792548"
---
# <a name="creating-a-basic-project-system-part-1"></a>Criando um sistema de projeto básico, Parte 1
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No Visual Studio, os projetos são contêineres que os desenvolvedores usam para organizar os arquivos de código-fonte e outros ativos. Projetos aparecem como filhos de soluções na **Gerenciador de soluções**. Projetos permitem que você organize, compilar, depurar e implantar o código-fonte e criar referências para os serviços da Web, bancos de dados e outros recursos.  
  
 Projetos são definidos em arquivos de projeto, por exemplo, um arquivo. csproj para um projeto do Visual c#. Você pode criar seu próprio tipo de projeto que tem sua própria extensão de nome de arquivo de projeto. Para obter mais informações sobre tipos de projeto, consulte [tipos de projeto](../extensibility/internals/project-types.md).  
  
> [!NOTE]
>  Se você precisar estender o Visual Studio com um tipo de projeto personalizado, é altamente recomendável aproveitar a [sistema de projeto do Visual Studio](https://github.com/Microsoft/VSProjectSystem) que tem uma série de vantagens sobre a criação de um sistema de projeto a partir do zero:  
> 
> - Integração mais fácil.  Até mesmo um sistema de projeto básico exige dezenas de milhares de linhas de código.  Aproveitar o CPS reduz o custo de integração para alguns cliques, antes que você está pronto para personalizá-lo às suas necessidades.  
>   -   Facilidade de manutenção.  Aproveitando o CPS, você precisa apenas manter seus próprios cenários.  Podemos lidar com a manutenção de toda a infraestrutura do sistema de projeto.  
> 
>   Se você precisar direcionar às versões do Visual Studio mais antigo que o Visual Studio 2013, você não poderá aproveitar o CPS em uma extensão do Visual Studio.  Se esse for o caso, este passo a passo é um bom lugar para começar a usar.  
  
 Este passo a passo mostra como criar um tipo de projeto que tem o .myproj de extensão de nome de arquivo de projeto. Este passo a passo emprestada do sistema de projeto Visual c# existente.  
  
> [!NOTE]
>  Para um exemplo de ponta a ponta de um sistema de projeto de linguagem completa, consulte o exemplo de IronPython Deep Dive na [exemplos de VSSDK](../misc/vssdk-samples.md).  
  
 Este passo a passo ensina como realizar essas tarefas:  
  
-   Crie um tipo de projeto básico.  
  
-   Crie um modelo de projeto básico.  
  
-   Registre o modelo de projeto no Visual Studio.  
  
-   Criar uma instância de projeto, abra o **novo projeto** caixa de diálogo e, em seguida, usando seu modelo.  
  
-   Crie uma fábrica de projeto para o seu sistema de projeto.  
  
-   Crie um nó do projeto para o seu sistema de projeto.  
  
-   Adicione ícones personalizados para o sistema de projeto.  
  
-   Implemente a substituição de parâmetro do modelo básico.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
 Você também deve baixar o código-fonte para o [estrutura de pacote gerenciado para projetos](http://mpfproj12.codeplex.com/). Extraia o arquivo para um local acessível para a solução que você pretende criar.  
  
## <a name="creating-a-basic-project-type"></a>Criando um tipo de projeto básico  
 Crie um projeto de VSIX em C# chamado **SimpleProject**. (**Arquivo, novo, projeto** e, em seguida **pacote do Visual Studio c#, extensibilidade,**). Adicionar um modelo de item de projeto do Visual Studio Package (no Gerenciador de soluções, clique com botão direito no nó do projeto e selecione **Adicionar / Novo Item**, em seguida, vá para **extensibilidade / pacote do Visual Studio**). Nomeie o arquivo **SimpleProjectPackage**.  
  
## <a name="creating-a-basic-project-template"></a>Criando um modelo de projeto básico  
 Agora, você pode modificar este VSPackage básicas para implementar o novo tipo de projeto .myproj. Para criar um projeto com base no tipo de projeto .myproj, Visual Studio precisa saber quais arquivos, recursos e referências a serem adicionadas ao novo projeto. Para fornecer essas informações, colocar os arquivos de projeto em uma pasta de modelo de projeto. Quando um usuário usa o projeto .myproj para criar um projeto, os arquivos são copiados para o novo projeto.  
  
#### <a name="to-create-a-basic-project-template"></a>Para criar um modelo de projeto básico  
  
1. Adicionar três pastas para o projeto, um sob o outro: **Templates\Projects\SimpleProject**. (No **Gerenciador de soluções**, clique com botão direito do **SimpleProject** nó do projeto, aponte para **adicionar**e, em seguida, clique em **nova pasta**. Nomeie a pasta `Templates`. No **modelos** pasta, adicione uma pasta chamada `Projects`. Além de **projetos** pasta, adicione uma pasta chamada `SimpleProject`.)  
  
2. No **Projects\SimpleProject** pasta adicionar um arquivo de ícone denominado `SimpleProject.ico`. Quando você clica em **adicionar**, abre o editor de ícone.  
  
3. Para exibir o ícone diferenciada. Esse ícone aparecerá na **novo projeto** caixa de diálogo posteriormente no passo a passo.  
  
    ![Ícone de projeto simples](../extensibility/media/simpleprojicon.png "SimpleProjIcon")  
  
4. O ícone Salvar e fechar o editor de ícone.  
  
5. No **Projects\SimpleProject** pasta, adicione um **classe** item nomeado `Program.cs`.  
  
6. Substitua o código existente com as seguintes linhas.  
  
   ```csharp  
   using System;  
   using System.Collections.Generic;  
   using System.Text;  
  
   namespace $nameSpace$  
   {  
       public class $className$  
       {  
           static void Main(string[] args)  
           {  
               Console.WriteLine("Hello VSX!!!");  
               Console.ReadKey();  
           }  
       }  
   }  
   ```  
  
   > [!IMPORTANT]
   >  Isso não é a forma final do código Program.cs; os parâmetros de substituição serão abordados em uma etapa posterior. Você poderá ver erros de compilação, mas desde que o arquivo **BuildAction** é **conteúdo**, você deve ser capaz de compilar e executar o projeto como de costume.  
  
7. Salve o arquivo.  
  
8. Copie o arquivo AssemblyInfo.cs dos **propriedades** pasta para o **Projects\SimpleProject** pasta.  
  
9. No **Projects\SimpleProject** pasta adicionar um arquivo XML denominado `SimpleProject.myproj`.  
  
   > [!NOTE]
   >  A extensão de nome de arquivo para todos os projetos desse tipo é .myproj. Se você quiser alterá-lo, altere-lo em qualquer lugar, que ele é mencionado no passo a passo.  
  
10. Substitua o conteúdo existente com as seguintes linhas.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <Project DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
      <PropertyGroup>  
        <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>  
        <SchemaVersion>2.0</SchemaVersion>  
        <ProjectGuid></ProjectGuid>  
        <OutputType>Exe</OutputType>  
        <RootNamespace>MyRootNamespace</RootNamespace>  
        <AssemblyName>MyAssemblyName</AssemblyName>  
        <EnableUnmanagedDebugging>false</EnableUnmanagedDebugging>  
      </PropertyGroup>  
      <PropertyGroup Condition=" '$(Configuration)' == 'Debug' ">  
        <DebugSymbols>true</DebugSymbols>  
        <OutputPath>bin\Debug\</OutputPath>  
      </PropertyGroup>  
      <PropertyGroup Condition=" '$(Configuration)' == 'Release' ">  
        <DebugSymbols>false</DebugSymbols>  
        <OutputPath>bin\Release\</OutputPath>  
      </PropertyGroup>  
      <ItemGroup>  
        <Reference Include="mscorlib" />  
        <Reference Include="System" />  
        <Reference Include="System.Data" />  
        <Reference Include="System.Xml" />  
      </ItemGroup>  
      <ItemGroup>  
        <Compile Include="AssemblyInfo.cs">  
          <SubType>Code</SubType>  
        </Compile>  
        <Compile Include="Program.cs">  
          <SubType>Code</SubType>  
        </Compile>  
      </ItemGroup>  
      <Import Project="$(MSBuildBinPath)\Microsoft.CSharp.targets" />  
    </Project>  
    ```  
  
11. Salve o arquivo.  
  
12. No **propriedades** janela, defina as **Build Action** de AssemblyInfo.cs, Program.cs, SimpleProject.ico e SimpleProject.myproj para **conteúdo**e defina seus  **Incluir no VSIX** propriedades a serem **verdadeiro**.  
  
    Este modelo de projeto descreve um projeto Visual c# básico que tenha uma configuração de depuração e uma configuração de versão. O projeto inclui dois arquivos de origem, AssemblyInfo.cs e Program.cs e assembly várias referências. Quando um projeto é criado a partir do modelo, o valor de ProjectGuid automaticamente é substituído por um novo GUID.  
  
    Na **Gerenciador de soluções**, o expandido **modelos** pasta deve aparecer da seguinte maneira:  
  
    Modelos  
  
    Projetos  
  
    SimpleProject  
  
    AssemblyInfo.cs  
  
    Module.vb  
  
    SimpleProject.ico  
  
    SimpleProject.myproj  
  
## <a name="creating-a-basic-project-factory"></a>Criação de uma fábrica de projeto básico  
 Você deve informar o local da pasta do modelo de projeto do Visual Studio. Para fazer isso, adicione um atributo à classe VSPackage que implementa a fábrica de projeto para que o local do modelo é gravado no registro do sistema quando o VSPackage é compilado. Comece criando uma fábrica de projeto básico que é identificada por um GUID de fábrica do projeto. Use o <xref:Microsoft.VisualStudio.Shell.ProvideProjectFactoryAttribute> atributo para conectar-se a fábrica de projeto para a classe SimpleProjectPackage.  
  
#### <a name="to-create-a-basic-project-factory"></a>Para criar uma fábrica de projeto básico  
  
1. Abra SimpleProjectPackageGuids.cs no editor de códigos.  
  
2. Criar GUIDs para sua fábrica de projeto (sobre o **ferramentas** menu, clique em **criar GUID**), ou use no exemplo a seguir. Adicione os GUIDs para a classe SimpleProjectPackageGuids. Os GUIDs devem estar no formato GUID e o formulário de cadeia de caracteres. O código resultante deve se parecer com o exemplo a seguir.  
  
   ```  
   static class SimpleProjectPackageGuids  
   {  
       public const string guidSimpleProjectPkgString =   
           "96bf4c26-d94e-43bf-a56a-f8500b52bfad";  
       public const string guidSimpleProjectCmdSetString =   
           "72c23e1d-f389-410a-b5f1-c938303f1391";  
       public const string guidSimpleProjectFactoryString =   
           "471EC4BB-E47E-4229-A789-D1F5F83B52D4";  
  
       public static readonly Guid guidSimpleProjectCmdSet =   
           new Guid(guidSimpleProjectCmdSetString);  
       public static readonly Guid guidSimpleProjectFactory =   
           new Guid(guidSimpleProjectFactoryString);  
   }  
   ```  
  
3. Adicione uma classe na parte superior **SimpleProject** pasta chamada `SimpleProjectFactory.cs`.  
  
4. Adicione as seguintes instruções using:  
  
   ```  
   using System.Runtime.InteropServices;  
   using Microsoft.VisualStudio.Shell;  
   ```  
  
5. Adicione um atributo de Guid para a classe SimpleProjectFactory. O valor do atributo é o novo GUID de fábrica de projeto.  
  
   ```  
   [Guid(SimpleProjectGuids.guidSimpleProjectFactoryString)]  
   class SimpleProjectFactory  
   {  
   }  
   ```  
  
   Agora você pode registrar seu modelo de projeto.  
  
#### <a name="to-register-the-project-template"></a>Para registrar o modelo de projeto  
  
1. No SimpleProjectPackage.cs, adicione um <xref:Microsoft.VisualStudio.Shell.ProvideProjectFactoryAttribute> atributo à classe SimpleProjectPackage, da seguinte maneira.  
  
   ```  
   [ProvideProjectFactory(    typeof(SimpleProjectFactory),     "Simple Project",   
       "Simple Project Files (*.myproj);*.myproj", "myproj", "myproj",   
       @"Templates\Projects\SimpleProject",     LanguageVsTemplate = "SimpleProject")]  
   [Guid(SimpleProjectGuids.guidSimpleProjectPkgString)]  
   public sealed class SimpleProjectPackage : Package  
   ```  
  
2. Recompile a solução e verificar se ele é compilado sem erros.  
  
    Recriando registra o modelo de projeto.  
  
   Os parâmetros `defaultProjectExtension` e `possibleProjectExtensions` são definidos para a extensão de nome de arquivo de projeto (.myproj). O `projectTemplatesDirectory` parâmetro for definido como o caminho relativo da pasta de modelos. Durante a compilação, esse caminho será convertido em uma compilação completa e adicionado ao registro para registrar o sistema de projeto.  
  
## <a name="testing-the-template-registration"></a>Teste o registro de modelo  
 Registro de modelo informa ao Visual Studio o local da pasta do modelo de projeto para que o Visual Studio pode exibir o nome do modelo e o ícone na **novo projeto** caixa de diálogo.  
  
#### <a name="to-test-the-template-registration"></a>Para testar o registro de modelo  
  
1. Pressione F5 para iniciar a depuração de uma instância experimental do Visual Studio.  
  
2. Na instância experimental, crie um novo projeto do seu tipo de projeto recém-criado. No **novo projeto** caixa de diálogo, você deverá ver **SimpleProject** sob **modelos instalados**.  
  
   Agora você tem uma fábrica de projeto que está registrada. No entanto, ele ainda não é possível criar um projeto. O pacote do projeto e a fábrica de projeto trabalham juntos para criar e inicializar um projeto.  
  
## <a name="add-the-managed-package-framework-code"></a>Adicione o código de estrutura de pacote gerenciado  
 Implemente a conexão entre o pacote do projeto e a fábrica de projeto.  
  
-   Importe os arquivos de código-fonte para a estrutura de pacote gerenciado.  
  
    1.  Descarregue o projeto SimpleProject (no **Gerenciador de soluções**, selecione o nó do projeto e no menu de contexto, clique em **descarregar projeto**.) e abra o arquivo de projeto no editor de XML.  
  
    2.  Adicione os seguintes blocos para o arquivo de projeto (imediatamente acima do \<importação > blocos). Defina ProjectBasePath para o local do arquivo ProjectBase.files no código de estrutura de pacote gerenciado que você acabou de baixar. Você talvez precise adicionar uma barra invertida para o nome do caminho. Se você não fizer isso, o projeto pode não conseguir encontrar o código de estrutura de pacote gerenciado.  
  
        ```  
        <PropertyGroup>  
             <ProjectBasePath>your path here\</ProjectBasePath>  
             <RegisterWithCodebase>true</RegisterWithCodebase>  
          </PropertyGroup>  
          <Import Project="$(ProjectBasePath)\ProjectBase.Files" />  
        ```  
  
        > [!IMPORTANT]
        >  Não se esqueça de barra invertida no final do caminho.  
  
    3.  Recarrega o projeto.  
  
    4.  Adicione referências aos assemblies a seguir:  
  
        -   Microsoft.VisualStudio.Designer.Interfaces (em \<install VSSDK > \VisualStudioIntegration\Common\Assemblies\v2.0)  
  
        -   WindowsBase  
  
        -   Microsoft.Build.Tasks.v4.0  
  
#### <a name="to-initialize-the-project-factory"></a>Para inicializar a fábrica de projeto  
  
1.  No arquivo SimpleProjectPackage.cs, adicione o seguinte `using` instrução.  
  
    ```  
    using Microsoft.VisualStudio.Project;  
    ```  
  
2.  Derivar de `SimpleProjectPackage` classe `Microsoft.VisualStudio.Package.ProjectPackage`.  
  
    ```  
    public sealed class SimpleProjectPackage : ProjectPackage  
    ```  
  
3.  Registre-se a fábrica de projeto. Adicione a seguinte linha para o `SimpleProjectPackage.Initialize` método, logo após `base.Initialize`.  
  
    ```  
    base.Initialize();  
    this.RegisterProjectFactory(new SimpleProjectFactory(this));  
    ```  
  
4.  Implementa a propriedade abstrata `ProductUserContext`:  
  
    ```csharp  
    public override string ProductUserContext  
        {  
            get { return ""; }  
    }  
    ```  
  
5.  No SimpleProjectFactory.cs, adicione o seguinte `using` instrução depois do `using` instruções.  
  
    ```  
    using Microsoft.VisualStudio.Project;  
    ```  
  
6.  Derivar de `SimpleProjectFactory` classe `ProjectFactory`.  
  
    ```  
    class SimpleProjectFactory : ProjectFactory  
    ```  
  
7.  Adicione o seguinte método fictício para o `SimpleProjectFactory` classe. Você implementará este método em uma seção posterior.  
  
    ```  
    protected override ProjectNode CreateProject()  
    {  
        return null;  
    }  
    ```  
  
8.  Adicione o seguinte campo e o construtor para o `SimpleProjectFactory` classe. Isso `SimpleProjectPackage` referência é armazenado em cache em um campo particular para que ele pode ser usado na configuração de um site do provedor de serviço.  
  
    ```  
    private SimpleProjectPackage package;  
  
    public SimpleProjectFactory(SimpleProjectPackage package)  
        : base(package)  
    {  
        this.package = package;  
    }  
    ```  
  
9. Recompile a solução e verificar se ele é compilado sem erros.  
  
## <a name="testing-the-project-factory-implementation"></a>Testando a implementação de fábrica de projeto  
 Teste se o construtor para sua implementação de fábrica de projeto é chamado.  
  
#### <a name="to-test-the-project-factory-implementation"></a>Para testar a implementação de fábrica de projeto  
  
1.  No arquivo SimpleProjectFactory.cs, defina um ponto de interrupção na linha a seguir no `SimpleProjectFactory` construtor.  
  
    ```  
    this.package = package;  
    ```  
  
2.  Pressione F5 para iniciar uma instância experimental do Visual Studio.  
  
3.  Na instância experimental, comece a criar um novo projeto. No **novo projeto** caixa de diálogo, selecione o SimpleProject tipo de projeto e, em seguida, clique em **Okey**. Interrompe a execução no ponto de interrupção.  
  
4.  Limpe o ponto de interrupção e parar a depuração. Como não criamos um nó do projeto ainda, o código de criação do projeto ainda lança exceções.  
  
## <a name="extending-the-project-node-class"></a>Estendendo a classe de nó do projeto  
 Agora, você pode implementar o `SimpleProjectNode` classe, que deriva de `ProjectNode` classe. O `ProjectNode` classe base lida com as seguintes tarefas de criação do projeto:  
  
- Copia o arquivo de modelo de projeto, SimpleProject.myproj, para a nova pasta de projeto. A cópia é renomeada de acordo com o nome inserido na **novo projeto** caixa de diálogo. O `ProjectGuid` valor da propriedade é substituído por um novo GUID.  
  
- Percorre os elementos do MSBuild do arquivo de modelo de projeto, SimpleProject.myproj e procura `Compile` elementos. Para cada `Compile` arquivo de destino, copia o arquivo para a nova pasta de projeto.  
  
  A derivada `SimpleProjectNode` classe lida com essas tarefas:  
  
- Permite que os ícones para nós de projeto e arquivo no **Gerenciador de soluções** a ser criada ou selecionada.  
  
- Habilita as substituições de parâmetro de modelo de projeto adicionais sejam especificados.  
  
#### <a name="to-extend-the-project-node-class"></a>Estender a classe de nó do projeto  
  
1. 
  
2. Adicione uma classe chamada `SimpleProjectNode.cs`.  
  
3. Substitua o código existente pelo código a seguir.  
  
   ```  
   using System;  
   using System.Collections.Generic;  
   using Microsoft.VisualStudio.Project;  
  
   namespace SimpleProject  
   {  
       public class SimpleProjectNode : ProjectNode  
       {  
           private SimpleProjectPackage package;  
  
           public SimpleProjectNode(SimpleProjectPackage package)  
           {  
               this.package = package;  
           }  
           public override Guid ProjectGuid  
           {  
               get { return SimpleProjectGuids.guidSimpleProjectFactory; }  
           }  
           public override string ProjectType  
           {  
               get { return "SimpleProjectType"; }  
           }  
  
           public override void AddFileFromTemplate(  
               string source, string target)  
           {  
               this.FileTemplateProcessor.UntokenFile(source, target);  
               this.FileTemplateProcessor.Reset();  
           }  
       }  
   }  
   ```  
  
   Isso `SimpleProjectNode` implementação da classe tem esses métodos substituídos:  
  
- `ProjectGuid`, que retorna o GUID de fábrica do projeto.  
  
- `ProjectType`, que retorna o nome localizado do tipo de projeto.  
  
- `AddFileFromTemplate`, que copia arquivos selecionados da pasta de modelo para o projeto de destino. Além disso, esse método é implementado em uma seção posterior.  
  
  O `SimpleProjectNode` construtor, como o `SimpleProjectFactory` construtor, armazena em cache um `SimpleProjectPackage` referência em um campo particular para uso posterior.  
  
  Para conectar-se a `SimpleProjectFactory` de classe para o `SimpleProjectNode` classe, você deve criar um novo `SimpleProjectNode` no `SimpleProjectFactory.CreateProject` método e armazena em cache em um campo particular para uso posterior.  
  
#### <a name="to-connect-the-project-factory-class-and-the-node-class"></a>Para conectar-se a classe de fábrica do projeto e a classe de nó  
  
1.  No arquivo SimpleProjectFactory.cs, adicione o seguinte `using` instrução:  
  
    ```  
    using IOleServiceProvider =    Microsoft.VisualStudio.OLE.Interop.IServiceProvider;  
    ```  
  
2.  Substitua o `SimpleProjectFactory.CreateProject` método usando o código a seguir.  
  
    ```  
    protected override ProjectNode CreateProject()  
    {  
        SimpleProjectNode project = new SimpleProjectNode(this.package);  
  
        project.SetSite((IOleServiceProvider)        ((IServiceProvider)this.package).GetService(            typeof(IOleServiceProvider)));  
        return project;  
    }  
    ```  
  
3.  Recompile a solução e verificar se ele é compilado sem erros.  
  
## <a name="testing-the-project-node-class"></a>Testando a classe de nó do projeto  
 Teste sua fábrica de projeto para ver se ele cria uma hierarquia do projeto.  
  
#### <a name="to-test-the-project-node-class"></a>Para testar a classe de nó do projeto  
  
1.  Pressione F5 para iniciar a depuração. Na instância experimental, crie um novo SimpleProject.  
  
2.  Visual Studio deve chamar sua fábrica de projeto para criar um projeto.  
  
3.  Feche a instância experimental do Visual Studio.  
  
## <a name="adding-a-custom-project-node-icon"></a>Adicionando um ícone de nó de projeto personalizado  
 O ícone do nó do projeto na seção anterior é um ícone padrão. Você pode alterar para um ícone personalizado.  
  
#### <a name="to-add-a-custom-project-node-icon"></a>Para adicionar um ícone de nó de projeto personalizado  
  
1. No **recursos** pasta, adicione um arquivo de bitmap chamado SimpleProjectNode.bmp.  
  
2. No **propriedades** windows, reduza o bitmap para 16 por 16 pixels. Verifique o bitmap diferenciada.  
  
    ![Comando de projeto simples](../extensibility/media/simpleprojprojectcomm.png "SimpleProjProjectComm")  
  
3. No **propriedades** janela, altere o **ação de Build** do bitmap a ser **Embedded Resource**.  
  
4. No SimpleProjectNode.cs, adicione o seguinte `using` instruções:  
  
   ```  
   using System.Drawing;  
   using System.Windows.Forms;  
   ```  
  
5. Adicione o seguinte campo estático e o construtor para o `SimpleProjectNode` classe.  
  
   ```  
   private static ImageList imageList;  
  
   static SimpleProjectNode()  
   {  
       imageList =        Utilities.GetImageList(            typeof(SimpleProjectNode).Assembly.GetManifestResourceStream(                "SimpleProject.Resources.SimpleProjectNode.bmp"));  
   }  
   ```  
  
6. Adicione a seguinte propriedade para o início do `SimpleProjectNode` classe.  
  
   ```  
   internal static int imageIndex;  
      public override int ImageIndex  
      {  
          get { return imageIndex; }  
      }  
   ```  
  
7. Substitua o construtor de instância com o código a seguir.  
  
   ```  
   public SimpleProjectNode(SimpleProjectPackage package)  
   {  
       this.package = package;  
  
       imageIndex = this.ImageHandler.ImageList.Images.Count;  
  
       foreach (Image img in imageList.Images)  
       {  
           this.ImageHandler.AddImage(img);  
       }  
   }  
   ```  
  
   Durante a construção estática, `SimpleProjectNode` recupera o bitmap de nó do projeto de recursos de manifesto do assembly e armazena em cache em um campo particular para uso posterior. Observe a sintaxe do <xref:System.Reflection.Assembly.GetManifestResourceStream%2A> caminho da imagem. Para ver os nomes dos recursos de manifesto inseridos em um assembly, use o <xref:System.Reflection.Assembly.GetManifestResourceNames%2A> método. Quando esse método é aplicado ao `SimpleProject` assembly, os resultados devem ser da seguinte maneira:  
  
- SimpleProject.Resources.resources  
  
- VisualStudio.Project.resources  
  
- SimpleProject.VSPackage.resources  
  
- Resources.imagelis.bmp  
  
- Microsoft.VisualStudio.Project.DontShowAgainDialog.resources  
  
- Microsoft.VisualStudio.Project.SecurityWarningDialog.resources  
  
- SimpleProject.Resources.SimpleProjectNode.bmp  
  
  Durante a construção de instância, o `ProjectNode` Resources.imagelis.bmp, no qual são bitmaps de 16 x 16 comumente usados incorporado de Resources\imagelis.bmp classe base é carregado. Esta lista de bitmap é disponibilizada para `SimpleProjectNode` como ImageHandler.ImageList. `SimpleProjectNode` acrescenta o bitmap de nó do projeto à lista. O deslocamento do bitmap de nó do projeto na lista de imagens é armazenado em cache para uso posterior como o valor do público `ImageIndex` propriedade. Visual Studio usa essa propriedade para determinar quais bitmap a ser exibido como o ícone de nó do projeto.  
  
## <a name="testing-the-custom-project-node-icon"></a>Testando o ícone do nó de projeto personalizado  
 Teste sua fábrica de projeto para ver se ele cria uma hierarquia de projeto que tem o ícone do nó de projeto personalizado.  
  
#### <a name="to-test-the-custom-project-node-icon"></a>Para testar o ícone do nó de projeto personalizado  
  
1.  Iniciar a depuração e na instância experimental, crie um novo SimpleProject.  
  
2.  No projeto recém-criado, observe que SimpleProjectNode.bmp é usado como o ícone de nó do projeto.  
  
     ![Projeto simples novo nó do projeto](../extensibility/media/simpleprojnewprojectnode.png "SimpleProjNewProjectNode")  
  
3.  Abra Program.cs no editor de códigos. Você deve ver o código-fonte que se parece com o código a seguir.  
  
    ```  
    using System;  
    using System.Collections.Generic;  
    using System.Text;  
  
    namespace $nameSpace$  
    {  
        public class $className$  
        {  
            static void Main(string[] args)  
            {  
                Console.WriteLine("Hello VSX!!!");  
                Console.ReadKey();  
            }  
        }  
    }  
    ```  
  
     Observe que os parâmetros de modelo $nameSpace$ e $ $className$ não tem novos valores. Você aprenderá a implementar a substituição de parâmetro de modelo na próxima seção.  
  
## <a name="substituting-template-parameters"></a>Substituindo parâmetros de modelo  
 Em uma seção anterior, você registrou o modelo de projeto com o Visual Studio usando o `ProvideProjectFactory` atributo. Registrar o caminho de uma pasta de modelos dessa maneira permite que você habilitar a substituição de parâmetro do modelo básico, substituindo e expandindo o `ProjectNode.AddFileFromTemplate` classe. Para obter mais informações, consulte [nova geração de projeto: Under the Hood, parte dois](../extensibility/internals/new-project-generation-under-the-hood-part-two.md).  
  
 Agora, adicione o código de substituição para o `AddFileFromTemplate` classe.  
  
#### <a name="to-substitute-template-parameters"></a>Substituir parâmetros de modelo  
  
1. No arquivo SimpleProjectNode.cs, adicione o seguinte `using` instrução.  
  
   ```  
   using System.IO;  
   ```  
  
2. Substitua o `AddFileFromTemplate` método usando o código a seguir.  
  
   ```  
   public override void AddFileFromTemplate(  
       string source, string target)  
   {  
       string nameSpace =   
           this.FileTemplateProcessor.GetFileNamespace(target, this);  
       string className = Path.GetFileNameWithoutExtension(target);  
  
       this.FileTemplateProcessor.AddReplace("$nameSpace$", nameSpace);  
       this.FileTemplateProcessor.AddReplace("$className$", className);  
  
       this.FileTemplateProcessor.UntokenFile(source, target);  
       this.FileTemplateProcessor.Reset();  
   }  
   ```  
  
3. Defina um ponto de interrupção no método, logo após o `className` instrução de atribuição.  
  
   As instruções de atribuição determinam valores razoáveis para um namespace e um novo nome de classe. Os dois `ProjectNode.FileTemplateProcessor.AddReplace` chamadas de método substitua os valores de parâmetro de modelo correspondente usando esses novos valores.  
  
## <a name="testing-the-template-parameter-substitution"></a>Testando a substituição de parâmetro de modelo  
 Agora você pode testar a substituição de parâmetro de modelo.  
  
#### <a name="to-test-the-template-parameter-substitution"></a>Para testar a substituição de parâmetro de modelo  
  
1. Iniciar a depuração e na instância experimental, crie um novo SimpleProject.  
  
2. Execução é interrompida no ponto de interrupção no `AddFileFromTemplate` método.  
  
3. Examine os valores para o `nameSpace` e `className` parâmetros.  
  
   -   `nameSpace` recebe o valor da \<RootNamespace > elemento no arquivo de modelo de projeto \Templates\Projects\SimpleProject\SimpleProject.myproj. Nesse caso, o valor é "MyRootNamespace".  
  
   -   `className` recebe o valor do nome de arquivo de origem de classe, sem a extensão de nome de arquivo. Nesse caso, o primeiro arquivo a ser copiado para a pasta de destino é AssemblyInfo.cs; Portanto, o valor do nome da classe é "AssemblyInfo".  
  
4. Remova o ponto de interrupção e pressione F5 para continuar a execução.  
  
    Visual Studio deverá terminar a criação de um projeto.  
  
5. Abra Program.cs no editor de códigos. Você deve ver o código-fonte que se parece com o código a seguir.  
  
   ```  
   using System;  
   using System.Collections.Generic;  
   using System.Linq;  
   using System.Text;  
  
   namespace MyRootNamespace  
   {  
       public class Program  
       {  
           static void Main(string[] args)  
           {  
               Console.WriteLine("Hello VSX!!!");  
               Console.ReadKey();  
           }  
       }  
   }  
   ```  
  
    Observe que o namespace agora é "MyRootNamespace" e o nome de classe agora é "Programa".  
  
6. Inicie a depuração do projeto. O novo projeto deve compilar, executar e exibir "Hello VSX"!!! na janela do console.  
  
    ![Comando de projeto simples](../extensibility/media/simpleprojcommand.png "SimpleProjCommand")  
  
   Parabéns! Você implementou um sistema básico de projeto gerenciado.

