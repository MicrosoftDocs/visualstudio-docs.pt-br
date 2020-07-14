---
title: Criando um sistema de projeto básico, parte 1 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- writing a project system
- project system
- tutorial
ms.assetid: 882a10fa-bb1c-4b01-943a-7a3c155286dd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e95f760712f46632120540091b9f8f408aad9da4
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903429"
---
# <a name="create-a-basic-project-system-part-1"></a>Criar um sistema de projeto básico, parte 1
No Visual Studio, os projetos são os contêineres que os desenvolvedores usam para organizar arquivos de código-fonte e outros ativos. Os projetos aparecem como filhos de soluções no **Gerenciador de soluções**. Os projetos permitem organizar, compilar, depurar e implantar código-fonte e criar referências a serviços Web, bancos de dados e outros recursos.

 Os projetos são definidos em arquivos de projeto, por exemplo, um arquivo *. csproj* para um projeto do Visual C#. Você pode criar seu próprio tipo de projeto que tenha sua própria extensão de nome de arquivo de projeto. Para obter mais informações sobre tipos de projeto, consulte [Project Types](../extensibility/internals/project-types.md).

> [!NOTE]
> Se você precisar estender o Visual Studio com um tipo de projeto personalizado, é altamente recomendável aproveitar o [sistema de projeto do Visual Studio](https://github.com/Microsoft/VSProjectSystem) (VSPs), que tem várias vantagens em relação à criação de um sistema de projeto do zero:
>
> - Integração mais fácil.  Mesmo um sistema de projeto básico requer dezenas de milhares de linhas de código.  Aproveitar o VSPS reduz o custo de integração a alguns cliques antes que você esteja pronto para personalizá-lo às suas necessidades.
> - Manutenção mais fácil.  Ao aproveitar o VSPS, você só precisa manter seus próprios cenários.  Tratamos da manutenção de toda a infraestrutura do sistema do projeto.
>
>   Se você precisar direcionar versões do Visual Studio com mais de Visual Studio 2013, não será possível aproveitar o VSPS em uma extensão do Visual Studio.  Se esse for o caso, este passo a passos é um bom lugar para começar.

 Este tutorial mostra como criar um tipo de projeto que tem a extensão de nome de arquivo de projeto *. MyProj*. Este tutorial se empresta do sistema de projeto existente do Visual C#.

> [!NOTE]
> Para obter mais exemplos de projetos de extensão, consulte [exemplos de VSSDK](https://github.com/Microsoft/VSSDK-Extensibility-Samples).

 Este tutorial ensina como realizar essas tarefas:

- Crie um tipo de projeto básico.

- Crie um modelo de projeto básico.

- Registre o modelo de projeto com o Visual Studio.

- Crie uma instância de projeto abrindo a caixa de diálogo **novo projeto** e, em seguida, usando o modelo.

- Crie uma fábrica de projetos para o sistema de projeto.

- Crie um nó de projeto para o sistema de projeto.

- Adicione ícones personalizados para o sistema de projeto.

- Implemente a substituição de parâmetro de modelo básico.

## <a name="prerequisites"></a>Pré-requisitos
 A partir do Visual Studio 2015, você não instala o SDK do Visual Studio a partir do centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

 Você também deve baixar o código-fonte da [estrutura de pacote gerenciado para projetos](https://github.com/tunnelvisionlabs/MPFProj10). Extraia o arquivo para um local que possa ser acessado pela solução que você vai criar.

## <a name="create-a-basic-project-type"></a>Criar um tipo de projeto básico
 Crie um projeto VSIX em C# chamado **SimpleProject**. (**Arquivo**  >  **Novo**  >  **Projeto** e, em seguida, projeto VSIX de extensibilidade do **Visual C#**  >  **Extensibility**  >  **VSIX Project**). Adicione um modelo de item de projeto de pacote do Visual Studio (na **Gerenciador de soluções**, clique com o botão direito do mouse no nó do projeto e selecione **Adicionar**  >  **novo item**e vá para **extensibilidade**do  >  **pacote do Visual Studio**). Nomeie o arquivo *SimpleProjectPackage*.

## <a name="creating-a-basic-project-template"></a>Criando um modelo de projeto básico
 Agora, você pode modificar esse VSPackage básico para implementar o novo tipo de projeto *. MyProj* . Para criar um projeto baseado no tipo de projeto *. MyProj* , o Visual Studio precisa saber quais arquivos, recursos e referências adicionar ao novo projeto. Para fornecer essas informações, coloque os arquivos de projeto em uma pasta de modelo de projeto. Quando um usuário usa o projeto *. MyProj* para criar um projeto, os arquivos são copiados para o novo projeto.

### <a name="to-create-a-basic-project-template"></a>Para criar um modelo de projeto básico

1. Adicione três pastas ao projeto, uma na outra: *Templates\Projects\SimpleProject*. (Em **Gerenciador de soluções**, clique com o botão direito do mouse no nó do projeto **SimpleProject** , aponte para **Adicionar**e clique em **nova pasta**. Nomeie a pasta *modelos*. Na pasta *modelos* , adicione uma pasta chamada *projetos*. Na pasta *projetos* , adicione uma pasta chamada *SimpleProject*.)

2. Na pasta *Templates\Projects\SimpleProject* , adicione um arquivo de imagem de bitmap para usar como o ícone chamado *SimpleProject. ico*. Quando você clica em **Adicionar**, o editor de ícone é aberto.

3. Torne o ícone distintivo. Esse ícone aparecerá na caixa de diálogo **novo projeto** posteriormente no passo a passos.

    ![Ícone de projeto simples](../extensibility/media/simpleprojicon.png "SimpleProjIcon")

4. Salve o ícone e feche o editor de ícone.

5. Na pasta *Templates\Projects\SimpleProject* , adicione um item de **classe** chamado *Program.cs*.

6. Substitua o código existente pelas linhas a seguir.

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
   > Essa não é a forma final do código *Program.cs* ; os parâmetros de substituição serão tratados em uma etapa posterior. Você pode ver erros de compilação, mas, desde que o **BuildAction** do arquivo seja **conteúdo**, você deve ser capaz de compilar e executar o projeto como de costume.

7. Salve o arquivo.

8. Copie o arquivo *AssemblyInfo.cs* da pasta *Propriedades* para a pasta *Projects\SimpleProject* .

9. Na pasta *Projects\SimpleProject* , adicione um arquivo XML chamado *SimpleProject. MyProj*.

   > [!NOTE]
   > A extensão de nome de arquivo para todos os projetos desse tipo é *. MyProj*. Se você quiser alterá-lo, deverá alterá-lo em qualquer lugar em que ele for mencionado no Walkthrough.

10. Substitua o conteúdo existente pelas linhas a seguir.

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

12. Na janela **Propriedades** , defina a **ação de compilação** de *AssemblyInfo.cs*, *Program.cs*, *SimpleProject. ico*e *SimpleProject. MyProj* para **conteúdo**e defina sua **inclusão nas propriedades do VSIX** como **true**.

    Este modelo de projeto descreve um projeto básico do Visual C# que tem uma configuração de depuração e uma configuração de versão. O projeto inclui dois arquivos de origem, *AssemblyInfo.cs* e *Program.cs*, e várias referências de assembly. Quando um projeto é criado a partir do modelo, o valor de ProjectGuid é substituído automaticamente por um novo GUID.

    No **Gerenciador de soluções**, a pasta **modelos** expandidos deve aparecer da seguinte maneira:

```
Templates
   Projects
      SimpleProject
         AssemblyInfo.cs
         Program.cs
         SimpleProject.ico
         SimpleProject.myproj
```

## <a name="create-a-basic-project-factory"></a>Criar uma fábrica de projetos básica
 Você deve informar ao Visual Studio o local da pasta de modelo do projeto. Para fazer isso, adicione um atributo à classe VSPackage que implementa a fábrica de projetos para que o local do modelo seja gravado no registro do sistema quando o VSPackage for criado. Comece criando uma fábrica de projeto básica que é identificada por um GUID de fábrica do projeto. Use o <xref:Microsoft.VisualStudio.Shell.ProvideProjectFactoryAttribute> atributo para conectar a fábrica do projeto à `SimpleProjectPackage` classe.

### <a name="to-create-a-basic-project-factory"></a>Para criar uma fábrica de projetos básica

1. Crie GUIDs para o seu projeto Factory (no menu **ferramentas** , clique em **Criar GUID**) ou use um no exemplo a seguir. Adicione os GUIDs à `SimpleProjectPackage` classe próxima à seção com o já definido `PackageGuidString` . Os GUIDs devem estar no formato de GUID e no formulário de cadeia de caracteres. O código resultante deve ser semelhante ao exemplo a seguir.

   ```csharp
       public sealed class SimpleProjectPackage : Package
       {
           ...
           public const string SimpleProjectPkgString = "96bf4c26-d94e-43bf-a56a-f8500b52bfad";
           public const string SimpleProjectFactoryString = "471EC4BB-E47E-4229-A789-D1F5F83B52D4";

           public static readonly Guid guidSimpleProjectFactory = new Guid(SimpleProjectFactoryString);
       }
   ```

2. Adicione uma classe à pasta *SimpleProject* superior chamada *SimpleProjectFactory.cs*.

3. Adicione o seguinte usando as orientações:

   ```csharp
   using System.Runtime.InteropServices;
   using Microsoft.VisualStudio.Shell;
   ```

4. Adicione um atributo GUID à `SimpleProjectFactory` classe. O valor do atributo é o novo GUID de fábrica do projeto.

   ```csharp
   [Guid(SimpleProjectPackage.SimpleProjectFactoryString)]
   class SimpleProjectFactory
   {
   }
   ```

   Agora você pode registrar seu modelo de projeto.

### <a name="to-register-the-project-template"></a>Para registrar o modelo de projeto

1. No *SimpleProjectPackage.cs*, adicione um <xref:Microsoft.VisualStudio.Shell.ProvideProjectFactoryAttribute> atributo à `SimpleProjectPackage` classe, da seguinte maneira.

   ```csharp
   [ProvideProjectFactory(    typeof(SimpleProjectFactory),     "Simple Project",
       "Simple Project Files (*.myproj);*.myproj", "myproj", "myproj",
       @"Templates\Projects\SimpleProject",     LanguageVsTemplate = "SimpleProject")]
   [Guid(SimpleProjectPackage.PackageGuidString)]
   public sealed class SimpleProjectPackage : Package
   ```

2. Recompile a solução e verifique se ela é compilada sem erros.

    A recriação registra o modelo de projeto.

   Os parâmetros `defaultProjectExtension` e `possibleProjectExtensions` são definidos como a extensão de nome de arquivo do projeto (*. MyProj*). O `projectTemplatesDirectory` parâmetro é definido como o caminho relativo da pasta *modelos* . Durante a compilação, esse caminho será convertido em uma compilação completa e adicionado ao registro para registrar o sistema de projeto.

## <a name="test-the-template-registration"></a>Testar o registro do modelo
 Registro de modelo informa ao Visual Studio o local da pasta de modelo do projeto para que o Visual Studio possa exibir o nome do modelo e o ícone na caixa de diálogo **novo projeto** .

### <a name="to-test-the-template-registration"></a>Para testar o registro do modelo

1. Pressione **F5** para iniciar a depuração de uma instância experimental do Visual Studio.

2. Na instância experimental, crie um novo projeto de seu tipo de projeto criado recentemente. Na caixa de diálogo **novo projeto** , você deve ver **SimpleProject** em **modelos instalados**.

   Agora você tem uma fábrica de projetos registrada. No entanto, ele ainda não pode criar um projeto. O pacote de projeto e o Project Factory trabalham juntos para criar e inicializar um projeto.

## <a name="add-the-managed-package-framework-code"></a>Adicionar o código de estrutura de pacote gerenciado
 Implemente a conexão entre o pacote do projeto e a fábrica do projeto.

- Importe os arquivos de código-fonte para a estrutura de pacote gerenciado.

    1. Descarregue o projeto SimpleProject (em **Gerenciador de soluções**, selecione o nó do projeto e, no menu de contexto, clique em **descarregar projeto**.) e abra o arquivo de projeto no editor de XML.

    2. Adicione os seguintes blocos ao arquivo de projeto (logo acima dos \<Import> blocos). Defina `ProjectBasePath` como o local do arquivo *ProjectBase. files* no código da estrutura de pacote gerenciado que você acabou de baixar. Talvez seja necessário adicionar uma barra invertida ao nome do caminho. Se você não fizer isso, o projeto poderá falhar ao localizar o código-fonte da estrutura de pacote gerenciado.

        ```
        <PropertyGroup>
             <ProjectBasePath>your path here\</ProjectBasePath>
             <RegisterWithCodebase>true</RegisterWithCodebase>
          </PropertyGroup>
          <Import Project="$(ProjectBasePath)\ProjectBase.Files" />
        ```

        > [!IMPORTANT]
        > Não se esqueça da barra invertida no final do caminho.

    3. Recarregue o projeto.

    4. Adicione referências aos assemblies a seguir:

        - `Microsoft.VisualStudio.Designer.Interfaces`(em * \<VSSDK install> \VisualStudioIntegration\Common\Assemblies\v2.0*)

        - `WindowsBase`

        - `Microsoft.Build.Tasks.v4.0`

### <a name="to-initialize-the-project-factory"></a>Para inicializar a fábrica de projetos

1. No arquivo *SimpleProjectPackage.cs* , adicione a diretiva a seguir `using` .

    ```csharp
    using Microsoft.VisualStudio.Project;
    ```

2. Derive a `SimpleProjectPackage` classe de `Microsoft.VisualStudio.Package.ProjectPackage` .

    ```csharp
    public sealed class SimpleProjectPackage : ProjectPackage
    ```

3. Registre a fábrica do projeto. Adicione a seguinte linha ao `SimpleProjectPackage.Initialize` método, logo após `base.Initialize` .

    ```csharp
    base.Initialize();
    this.RegisterProjectFactory(new SimpleProjectFactory(this));
    ```

4. Implemente a propriedade abstract `ProductUserContext` :

    ```csharp
    public override string ProductUserContext
        {
            get { return ""; }
    }
    ```

5. No *SimpleProjectFactory.cs*, adicione a diretiva a seguir `using` após as `using` diretivas existentes.

    ```csharp
    using Microsoft.VisualStudio.Project;
    ```

6. Derive a `SimpleProjectFactory` classe de `ProjectFactory` .

    ```csharp
    class SimpleProjectFactory : ProjectFactory
    ```

7. Adicione o seguinte método fictício à `SimpleProjectFactory` classe. Você implementará esse método em uma seção posterior.

    ```csharp
    protected override ProjectNode CreateProject()
    {
        return null;
    }
    ```

8. Adicione o seguinte campo e Construtor à `SimpleProjectFactory` classe. Essa `SimpleProjectPackage` referência é armazenada em cache em um campo particular para que possa ser usada na configuração de um site do provedor de serviços.

    ```csharp
    private SimpleProjectPackage package;

    public SimpleProjectFactory(SimpleProjectPackage package)
        : base(package)
    {
        this.package = package;
    }
    ```

9. Recompile a solução e verifique se ela é compilada sem erros.

## <a name="test-the-project-factory-implementation"></a>Testar a implementação da fábrica do projeto
 Teste se o construtor para a implementação da fábrica do projeto é chamado.

### <a name="to-test-the-project-factory-implementation"></a>Para testar a implementação da fábrica do projeto

1. No arquivo *SimpleProjectFactory.cs* , defina um ponto de interrupção na linha a seguir no `SimpleProjectFactory` Construtor.

    ```csharp
    this.package = package;
    ```

2. Pressione **F5** para iniciar uma instância experimental do Visual Studio.

3. Na instância experimental, comece a criar um novo projeto. Na caixa de diálogo **novo projeto** , selecione o tipo de projeto **SimpleProject** e clique em **OK**. A execução é interrompida no ponto de interrupção.

4. Limpe o ponto de interrupção e interrompa a depuração. Como ainda não criamos um nó de projeto, o código de criação do projeto ainda gera exceções.

## <a name="extend-the-projectnode-class"></a>Estender a classe ProjectNode
 Agora você pode implementar a `SimpleProjectNode` classe, que deriva da `ProjectNode` classe. A `ProjectNode` classe base manipula as seguintes tarefas de criação do projeto:

- Copia o arquivo de modelo de projeto, *SimpleProject. MyProj*, para a nova pasta do projeto. A cópia é renomeada de acordo com o nome inserido na caixa de diálogo **novo projeto** . O `ProjectGuid` valor da propriedade é substituído por um novo GUID.

- Percorre os elementos do MSBuild do arquivo de modelo de projeto, *SimpleProject. MyProj*e procura `Compile` elementos. Para cada `Compile` arquivo de destino, o copia o arquivo para a nova pasta do projeto.

  A `SimpleProjectNode` classe derivada manipula estas tarefas:

- Habilita os ícones para os nós de projeto e de arquivo no **Gerenciador de soluções** ser criados ou selecionados.

- Habilita a especificação de substituições de parâmetro de modelo de projeto adicionais.

### <a name="to-extend-the-projectnode-class"></a>Para estender a classe ProjectNode

1. Adicione uma classe chamada `SimpleProjectNode.cs`.

2. Substitua o código existente pelo código a seguir.

   ```csharp
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
               get { return SimpleProjectPackage.guidSimpleProjectFactory; }
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

   Essa `SimpleProjectNode` implementação de classe tem estes métodos substituídos:

- `ProjectGuid`, que retorna o GUID de fábrica do projeto.

- `ProjectType`, que retorna o nome localizado do tipo de projeto.

- `AddFileFromTemplate`, que copia os arquivos selecionados da pasta de modelo para o projeto de destino. Esse método é posteriormente implementado em uma seção posterior.

  O `SimpleProjectNode` Construtor, como o `SimpleProjectFactory` Construtor, armazena em cache uma `SimpleProjectPackage` referência em um campo particular para uso posterior.

  Para conectar a `SimpleProjectFactory` classe à `SimpleProjectNode` classe, você deve instanciar um novo `SimpleProjectNode` no `SimpleProjectFactory.CreateProject` método e armazená-lo em cache em um campo particular para uso posterior.

### <a name="to-connect-the-project-factory-class-and-the-node-class"></a>Para conectar a classe do Project Factory e a classe node

1. No arquivo *SimpleProjectFactory.cs* , adicione a seguinte `using` diretiva:

    ```csharp
    using IOleServiceProvider =    Microsoft.VisualStudio.OLE.Interop.IServiceProvider;
    ```

2. Substitua o `SimpleProjectFactory.CreateProject` método usando o código a seguir.

    ```csharp
    protected override ProjectNode CreateProject()
    {
        SimpleProjectNode project = new SimpleProjectNode(this.package);

        project.SetSite((IOleServiceProvider)        ((IServiceProvider)this.package).GetService(            typeof(IOleServiceProvider)));
        return project;
    }
    ```

3. Recompile a solução e verifique se ela é compilada sem erros.

## <a name="test-the-projectnode-class"></a>Testar a classe ProjectNode
 Teste sua fábrica de projetos para ver se ele cria uma hierarquia de projeto.

### <a name="to-test-the-projectnode-class"></a>Para testar a classe ProjectNode

1. Pressione **F5** para iniciar a depuração. Na instância experimental, crie um novo SimpleProject.

2. O Visual Studio deve chamar o seu alocador de projeto para criar um projeto.

3. Feche a instância experimental do Visual Studio.

## <a name="add-a-custom-project-node-icon"></a>Adicionar um ícone de nó de projeto personalizado
 O ícone do nó do projeto na seção anterior é um ícone padrão. Você pode alterá-lo para um ícone personalizado.

### <a name="to-add-a-custom-project-node-icon"></a>Para adicionar um ícone de nó de projeto personalizado

1. Na pasta **recursos** , adicione um arquivo de bitmap chamado *SimpleProjectNode.bmp*.

2. Nas janelas **Propriedades** , reduza o bitmap para 16 por 16 pixels. Tornar o bitmap distintivo.

    ![Projeto simples de comunicação](../extensibility/media/simpleprojprojectcomm.png "SimpleProjProjectComm")

3. Na janela **Propriedades** , altere a **ação de Build** do bitmap para **recurso incorporado**.

4. No *SimpleProjectNode.cs*, adicione as seguintes `using` diretivas:

   ```csharp
   using System.Drawing;
   using System.Windows.Forms;
   ```

5. Adicione o seguinte campo estático e o Construtor à `SimpleProjectNode` classe.

   ```csharp
   private static ImageList imageList;

   static SimpleProjectNode()
   {
       imageList =        Utilities.GetImageList(            typeof(SimpleProjectNode).Assembly.GetManifestResourceStream(                "SimpleProject.Resources.SimpleProjectNode.bmp"));
   }
   ```

6. Adicione a propriedade a seguir ao início da `SimpleProjectNode` classe.

   ```csharp
   internal static int imageIndex;
      public override int ImageIndex
      {
          get { return imageIndex; }
      }
   ```

7. Substitua o construtor de instância pelo código a seguir.

   ```csharp
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

   Durante a construção estática, `SimpleProjectNode` o recupera o bitmap do nó do projeto dos recursos de manifesto do assembly e o armazena em cache em um campo particular para uso posterior. Observe a sintaxe do <xref:System.Reflection.Assembly.GetManifestResourceStream%2A> caminho da imagem. Para ver os nomes dos recursos de manifesto inseridos em um assembly, use o <xref:System.Reflection.Assembly.GetManifestResourceNames%2A> método. Quando esse método é aplicado ao `SimpleProject` assembly, os resultados devem ser os seguintes:

- *SimpleProject. Resources. Resources*

- *VisualStudio. Project. Resources*

- *SimpleProject. VSPackage. Resources*

- *Resources.imagelis.bmp*

- *Microsoft. VisualStudio. Project. DontShowAgainDialog. Resources*

- *Microsoft. VisualStudio. Project. SecurityWarningDialog. Resources*

- *SimpleProject.Resources.SimpleProjectNode.bmp*

  Durante a construção da instância, a `ProjectNode` classe base carrega *Resources.imagelis.bmp*, nas quais são inseridos 16 x 16 bitmaps comumente usados de *Resources\imagelis.bmp*. Essa lista de bitmaps é disponibilizada para `SimpleProjectNode` o as `ImageHandler.ImageList` . `SimpleProjectNode`anexa o bitmap do nó do projeto à lista. O deslocamento do bitmap do nó do projeto na lista de imagens é armazenado em cache para uso posterior como o valor da `ImageIndex` propriedade pública. O Visual Studio usa essa propriedade para determinar qual bitmap deve ser exibido como o ícone do nó do projeto.

## <a name="test-the-custom-project-node-icon"></a>Testar o ícone do nó de projeto personalizado
 Teste sua fábrica de projetos para ver se ele cria uma hierarquia de projeto que tem o ícone de nó de projeto personalizado.

### <a name="to-test-the-custom-project-node-icon"></a>Para testar o ícone do nó de projeto personalizado

1. Inicie a depuração e, na instância experimental, crie um novo SimpleProject.

2. No projeto recém-criado, observe que *SimpleProjectNode.bmp* é usado como o ícone do nó do projeto.

     ![Novo nó de projeto do projeto simples](../extensibility/media/simpleprojnewprojectnode.png "SimpleProjNewProjectNode")

3. Abra *Program.cs* no editor de códigos. Você deve ver o código-fonte que se assemelha ao código a seguir.

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

     Observe que os parâmetros de modelo $nameSpace $ e $className $ não têm novos valores. Você aprenderá a implementar a substituição de parâmetro de modelo na próxima seção.

## <a name="substitute-template-parameters"></a>Parâmetros de modelo substitutos
 Em uma seção anterior, você registrou o modelo de projeto com o Visual Studio usando o `ProvideProjectFactory` atributo. Registrar o caminho de uma pasta de modelo dessa maneira permite habilitar a substituição de parâmetro de modelo básico substituindo e expandindo a `ProjectNode.AddFileFromTemplate` classe. Para obter mais informações, consulte [nova geração de projeto: nos bastidores, parte dois](../extensibility/internals/new-project-generation-under-the-hood-part-two.md).

 Agora, adicione o código de substituição à `AddFileFromTemplate` classe.

### <a name="to-substitute-template-parameters"></a>Para substituir parâmetros de modelo

1. No arquivo *SimpleProjectNode.cs* , adicione a diretiva a seguir `using` .

   ```csharp
   using System.IO;
   ```

2. Substitua o `AddFileFromTemplate` método usando o código a seguir.

   ```csharp
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

3. Defina um ponto de interrupção no método, logo após a `className` instrução de atribuição.

   As instruções de atribuição determinam valores razoáveis para um namespace e um novo nome de classe. As duas `ProjectNode.FileTemplateProcessor.AddReplace` chamadas de método substituem os valores de parâmetro de modelo correspondentes usando esses novos valores.

## <a name="test-the-template-parameter-substitution"></a>Testar a substituição de parâmetro de modelo
 Agora você pode testar a substituição de parâmetro de modelo.

### <a name="to-test-the-template-parameter-substitution"></a>Para testar a substituição de parâmetro de modelo

1. Inicie a depuração e, na instância experimental, crie um novo SimpleProject.

2. A execução é interrompida no ponto de interrupção no `AddFileFromTemplate` método.

3. Examine os valores dos `nameSpace` parâmetros e `className` .

   - `nameSpace`recebe o valor do \<RootNamespace> elemento no arquivo de modelo de projeto *\Templates\Projects\SimpleProject\SimpleProject.MyProj* . Nesse caso, o valor é `MyRootNamespace` .

   - `className`recebe o valor do nome do arquivo de origem da classe, sem a extensão de nome de arquivo. Nesse caso, o primeiro arquivo a ser copiado para a pasta de destino é *AssemblyInfo.cs*; Portanto, o valor de className é `AssemblyInfo` .

4. Remova o ponto de interrupção e pressione **F5** para continuar a execução.

    O Visual Studio deve concluir a criação de um projeto.

5. Abra *Program.cs* no editor de códigos. Você deve ver o código-fonte que se assemelha ao código a seguir.

   ```csharp
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

    Observe que o namespace agora é `MyRootNamespace` e o nome da classe agora é `Program` .

6. Comece a depuração do projeto. O novo projeto deve compilar, executar e exibir "Olá VSX!!!" na janela do console.

    ![Comando de projeto simples](../extensibility/media/simpleprojcommand.png "SimpleProjCommand")

   Parabéns! Você implementou um sistema de projeto gerenciado básico.
