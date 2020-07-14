---
title: Criando um sistema de projeto básico, parte 2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- writing a project system
- project system
- tutorial
ms.assetid: aee48fc6-a15f-4fd5-8420-7f18824de220
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2b9d5ce673e0ee44e888905239c12251241015ab
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903832"
---
# <a name="create-a-basic-project-system-part-2"></a>Criar um sistema de projeto básico, parte 2
A primeira explicação nesta série, [criar um sistema de projeto básico, parte 1](../extensibility/creating-a-basic-project-system-part-1.md), mostra como criar um sistema de projeto básico. Este tutorial se baseia no sistema de projeto básico adicionando um modelo do Visual Studio, uma página de propriedades e outros recursos. Você deve concluir o primeiro passo a passos antes de iniciar este.

Este tutorial ensina como criar um tipo de projeto que tenha a extensão de nome de arquivo de projeto *. MyProj*. Para concluir o passo a passos, você não precisa criar sua própria linguagem porque o passo a passos faz o empréstimo do sistema de projetos do Visual C# existente.

Este tutorial ensina como realizar essas tarefas:

- Crie um modelo do Visual Studio.

- Implantar um modelo do Visual Studio.

- Crie um nó filho do tipo de projeto na caixa de diálogo **novo projeto** .

- Habilite a substituição de parâmetro no modelo do Visual Studio.

- Criar uma página de propriedades do projeto.

> [!NOTE]
> As etapas neste passo a passos são baseadas em um projeto C#. No entanto, exceto para especificos, como extensões de nome de arquivo e código, você pode usar as mesmas etapas para um projeto de Visual Basic.

## <a name="create-a-visual-studio-template"></a>Criar um modelo do Visual Studio
- [Criar um sistema de projeto básico, parte 1](../extensibility/creating-a-basic-project-system-part-1.md) mostra como criar um modelo de projeto básico e adicioná-lo ao sistema do projeto. Ele também mostra como registrar esse modelo com o Visual Studio usando o <xref:Microsoft.VisualStudio.Shell.ProvideProjectFactoryAttribute> atributo, que grava o caminho completo da pasta * \\ Templates\Projects\SimpleProject \\ * no registro do sistema.

Usando um modelo do Visual Studio (arquivo *. vstemplate* ) em vez de um modelo de projeto básico, você pode controlar como o modelo aparece na caixa de diálogo **novo projeto** e como os parâmetros de modelo são substituídos. Um arquivo *. vstemplate* é um arquivo XML que descreve como os arquivos de origem devem ser incluídos quando um projeto é criado usando o modelo do sistema de projeto. O próprio sistema de projeto é criado coletando o arquivo *. vstemplate* e os arquivos de origem em um arquivo *. zip* e implantado copiando o arquivo *. zip* em um local conhecido pelo Visual Studio. Esse processo é explicado em mais detalhes posteriormente neste passo a passos.

1. No [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] , abra a solução SimpleProject que você criou seguindo [criar um sistema de projeto básico, parte 1](../extensibility/creating-a-basic-project-system-part-1.md).

2. No arquivo *SimpleProjectPackage.cs* , localize o atributo ProvideProjectFactory. Substitua o segundo parâmetro (o nome do projeto) por NULL e o quarto parâmetro (o caminho para a pasta de modelo do projeto) por ". \\ \NullPath ", da seguinte maneira.

    ```
    [ProvideProjectFactory(typeof(SimpleProjectFactory), null,
        "Simple Project Files (*.myproj);*.myproj", "myproj", "myproj",
        ".\\NullPath",
    LanguageVsTemplate = "SimpleProject")]
    ```

3. Adicione um arquivo XML chamado *SimpleProject. vstemplate* à pasta * \\ Templates\Projects\SimpleProject \\ * .

4. Substitua o conteúdo de *SimpleProject. vstemplate* pelo código a seguir.

    ```xml
    <VSTemplate Version="2.0.0" Type="Project"
        xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
      <TemplateData>
        <Name>SimpleProject Application</Name>
        <Description>
          A project for creating a SimpleProject application
        </Description>
        <Icon>SimpleProject.ico</Icon>
        <ProjectType>SimpleProject</ProjectType>
      </TemplateData>
      <TemplateContent>
        <Project File="SimpleProject.myproj" ReplaceParameters="true">
          <ProjectItem ReplaceParameters="true" OpenInEditor="true">
            Program.cs
          </ProjectItem>
          <ProjectItem ReplaceParameters="true" OpenInEditor="false">
            AssemblyInfo.cs
          </ProjectItem>
        </Project>
      </TemplateContent>
    </VSTemplate>
    ```

5. Na janela **Propriedades** , selecione todos os cinco arquivos na pasta * \\ Templates\Projects\SimpleProject \\ * e defina a **ação de Build** como **ZipProject**.

    ![Pasta de projeto simples](../extensibility/media/simpproj2.png "SimpProj2")

    A \<TemplateData> seção determina o local e a aparência do tipo de projeto SimpleProject na caixa de diálogo **novo projeto** , da seguinte maneira:

- O \<Name> elemento nomeia o modelo de projeto para ser SimpleProject aplicativo.

- O \<Description> elemento contém a descrição que aparece na caixa de diálogo **novo projeto** quando o modelo de projeto é selecionado.

- O \<Icon> elemento Especifica o ícone que aparece junto com o tipo de projeto SimpleProject.

- O \<ProjectType> elemento nomeia o tipo de projeto na caixa de diálogo **novo projeto** . Esse nome substitui o parâmetro Project Name do atributo ProvideProjectFactory.

  > [!NOTE]
  > O \<ProjectType> elemento deve corresponder ao `LanguageVsTemplate` argumento do `ProvideProjectFactory` atributo no arquivo SimpleProjectPackage.cs.

  A \<TemplateContent> seção descreve esses arquivos que são gerados quando um novo projeto é criado:

- *SimpleProject. MyProj*

- *Module.vb*

- *AssemblyInfo.cs*

  Todos os três arquivos foram `ReplaceParameters` definidos como true, o que permite a substituição de parâmetros. O arquivo *Program.cs* foi `OpenInEditor` definido como true, o que faz com que o arquivo seja aberto no editor de códigos quando um projeto é criado.

  Para obter mais informações sobre os elementos no esquema de modelo do Visual Studio, consulte a [referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md).

> [!NOTE]
> Se um projeto tiver mais de um modelo do Visual Studio, cada modelo estará em uma pasta separada. Cada arquivo nessa pasta deve ter a **ação de compilação** definida como **ZipProject**.

## <a name="adding-a-minimal-vsct-file"></a>Adicionando um arquivo. vsct mínimo
 O Visual Studio deve ser executado no modo de instalação para reconhecer um modelo novo ou modificado do Visual Studio. O modo de instalação requer que um arquivo *. vsct* esteja presente. Portanto, você deve adicionar um arquivo *. vsct* mínimo ao projeto.

1. Adicione um arquivo XML chamado *SimpleProject. vsct* ao projeto SimpleProject.

2. Substitua o conteúdo do arquivo *SimpleProject. vsct* pelo código a seguir.

    ```
    <?xml version="1.0" encoding="utf-8" ?>
    <CommandTable
      xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable">
    </CommandTable>
    ```

3. Defina a **ação de Build** deste arquivo como **VSCTCompile**. Você pode fazer isso somente no arquivo *. csproj* , não na janela **Propriedades** . Certifique-se de que a **ação de compilação** desse arquivo esteja definida como **nenhum** neste ponto.

    1. Clique com o botão direito do mouse no nó SimpleProject e clique em **Editar SimpleProject. csproj**.

    2. No arquivo *. csproj* , localize o item *SimpleProject. vsct* .

        ```
        <None Include="SimpleProject.vsct" />
        ```

    3. Altere a ação de Build para **VSCTCompile**.

        ```
        <VSCTCompile Include="SimpleProject.vsct" />
        ```

    4. o arquivo de projeto e feche o editor.

    5. Salve o nó SimpleProject e, em seguida, na **Gerenciador de soluções** clique em **recarregar projeto**.

## <a name="examine-the-visual-studio-template-build-steps"></a>Examinar as etapas de compilação do modelo do Visual Studio
 O sistema de compilação de projeto VSPackage normalmente executa o Visual Studio no modo de instalação quando o arquivo *. vstemplate* é alterado ou o projeto que contém o arquivo *. vstemplate* é recriado. Você pode acompanhar Configurando o nível de detalhamento do MSBuild para normal ou superior.

1. No menu **Ferramentas** , clique em **Opções**.

2. Expanda o nó **projetos e soluções** e, em seguida, selecione **Compilar e executar**.

3. Defina **detalhes de saída de compilação do projeto do MSBuild** como **normal**. Clique em **OK**.

4. Reconstrua o projeto SimpleProject.

    A etapa de compilação para criar o arquivo de projeto *. zip* deve ser semelhante ao exemplo a seguir.

```
ZipProjects:
1>  Zipping ProjectTemplates
1>  Zipping <path>\SimpleProject\SimpleProject\obj\Debug\SimpleProject.zip...
1>  Copying file from "<path>\SimpleProject\SimpleProject\obj\Debug\SimpleProject.zip" to "<%LOCALAPPDATA%>\Microsoft\VisualStudio\14.0Exp\ProjectTemplates\\\\SimpleProject.zip".
1>  Copying file from "<path>\SimpleProject\SimpleProject\obj\Debug\SimpleProject.zip" to "bin\Debug\\ProjectTemplates\\\\SimpleProject.zip".
1>  SimpleProject -> <path>\SimpleProject\SimpleProject\bin\Debug\ProjectTemplates\SimpleProject.zip
1>ZipItems:
1>  Zipping ItemTemplates
1>  SimpleProject ->
```

## <a name="deploy-a-visual-studio-template"></a>Implantar um modelo do Visual Studio
Os modelos do Visual Studio não contêm informações de caminho. Portanto, o arquivo *. zip* de modelo deve ser implantado em um local conhecido pelo Visual Studio. O local da pasta ProjectTemplates normalmente é *<% LocalAppData% > \microsoft\visualstudio\14.0exp\projecttemplates*.

Para implantar sua fábrica de projetos, o programa de instalação deve ter privilégios de administrador. Ele implanta modelos no nó de instalação do Visual Studio: *. ..\Microsoft Visual Studio 14.0 \ Common7\IDE\ProjectTemplates*.

## <a name="test-a-visual-studio-template"></a>Testar um modelo do Visual Studio
Teste sua fábrica de projetos para ver se ele cria uma hierarquia de projeto usando o modelo do Visual Studio.

1. Redefina a instância experimental do SDK do Visual Studio.

    Em [!INCLUDE[win7](../debugger/includes/win7_md.md)] : no menu **Iniciar** , localize a pasta **Microsoft Visual Studio/SDK do Microsoft Visual Studio/ferramentas** e, em seguida, selecione **redefinir a instância experimental Microsoft Visual Studio**.

    Em versões posteriores do Windows: na tela **Iniciar** , digite **redefinir a \<version> instância experimental Microsoft Visual Studio**.

2. Uma janela de prompt de comando é exibida. Quando você vir as palavras, **pressione qualquer tecla para continuar**, clique em **Enter**. Depois que a janela for fechada, abra o Visual Studio.

3. Recompile o projeto SimpleProject e inicie a depuração. A instância experimental é exibida.

4. Na instância experimental, crie um projeto SimpleProject. Na caixa de diálogo **novo projeto** , selecione **SimpleProject**.

5. Você deverá ver uma nova instância de SimpleProject.

    ![Nova instância do projeto simples](../extensibility/media/simpproj2_newproj.png "SimpProj2_NewProj")

    ![Nova instância do meu projeto](../extensibility/media/simpproj2_myproj.png "SimpProj2_MyProj")

## <a name="create-a-project-type-child-node"></a>Criar um nó filho do tipo de projeto
Você pode adicionar um nó filho a um nó de tipo de projeto na caixa de diálogo **novo projeto** . Por exemplo, para o tipo de projeto SimpleProject, você poderia ter nós filho para aplicativos de console, aplicativos de janela, aplicativos Web e assim por diante.

Nós filho são criados alterando o arquivo de projeto e adicionando \<OutputSubPath> filhos aos \<ZipProject> elementos. Quando um modelo é copiado durante a compilação ou implantação, cada nó filho se torna uma subpasta da pasta de modelos de projeto.

Esta seção mostra como criar um nó filho do console para o tipo de projeto SimpleProject.

1. Renomeie a pasta * \\ Templates\Projects\SimpleProject \\ * para * \\ Templates\Projects\ConsoleApp \\ *.

2. Na janela **Propriedades** , selecione todos os cinco arquivos na pasta * \\ Templates\Projects\ConsoleApp \\ * e verifique se a **ação de compilação** está definida como **ZipProject**.

3. No arquivo SimpleProject. vstemplate, adicione a seguinte linha ao final da \<TemplateData> seção, logo antes da marca de fechamento.

    ```
    <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>
    ```

    Isso faz com que o modelo de aplicativo de console apareça tanto no nó filho do console quanto no nó pai SimpleProject, que é um nível acima do nó filho.

4. Salve o arquivo *SimpleProject. vstemplate* .

5. No arquivo *. csproj* , adicione \<OutputSubPath> a cada um dos elementos ZipProject. Descarregue o projeto, como antes, e edite o arquivo de projeto.

6. Localize os \<ZipProject> elementos. Para cada \<ZipProject> elemento, adicione um \<OutputSubPath> elemento e dê a ele o valor console. O ZipProject

    ```
    <ZipProject Include="Templates\Projects\ConsoleApp\AssemblyInfo.cs">
      <OutputSubPath>Console</OutputSubPath>
    </ZipProject>
    <ZipProject Include="Templates\Projects\ConsoleApp\Program.cs">
      <OutputSubPath>Console</OutputSubPath>
    </ZipProject>
    <ZipProject Include="Templates\Projects\ConsoleApp\SimpleProject.myproj">
      <OutputSubPath>Console</OutputSubPath>
    </ZipProject>
    <ZipProject Include="Templates\Projects\ConsoleApp\SimpleProject.vstemplate">
      <OutputSubPath>Console</OutputSubPath>
    </ZipProject>
    <ZipProject Include="Templates\Projects\ConsoleApp\SimpleProject.ico">
      <OutputSubPath>Console</OutputSubPath>
    </ZipProject>
    ```

7. Adicione isso \<PropertyGroup> ao arquivo de projeto:

    ```
    <PropertyGroup>
      <VsTemplateLanguage>SimpleProject</VsTemplateLanguage>
    </PropertyGroup>
    ```

8. Salve o arquivo de projeto e recarregue o projeto.

## <a name="test-the-project-type-child-node"></a>Testar o nó filho do tipo de projeto
Teste o arquivo de projeto modificado para ver se o nó filho do **console** aparece na caixa de diálogo **novo projeto** .

1. Execute a ferramenta **redefinir a Microsoft Visual Studio instância experimental** .

2. Recompile o projeto SimpleProject e inicie a depuração. A instância experimental deve aparecer

3. Na caixa de diálogo **novo projeto** , clique no nó **SimpleProject** . O modelo de **aplicativo de console** deve aparecer no painel **modelos** .

4. Expanda o nó **SimpleProject** . O nó filho do **console** deve aparecer. O modelo de **aplicativo SimpleProject** continua aparecendo no painel **modelos** .

5. Clique em **Cancelar** e parar a depuração.

    ![ROLLUP de projeto simples](../extensibility/media/simpproj2_rollup.png "SimpProj2_Rollup")

    ![Nó de console de projeto simples](../extensibility/media/simpproj2_subfolder.png "SimpProj2_Subfolder")

## <a name="substitute-project-template-parameters"></a>Parâmetros de modelo de projeto substituto
- [Criando um sistema de projeto básico, parte 1](../extensibility/creating-a-basic-project-system-part-1.md) mostrou como substituir o `ProjectNode.AddFileFromTemplate` método para fazer um tipo básico de substituição de parâmetro de modelo. Esta seção ensina a usar os parâmetros de modelo mais sofisticados do Visual Studio.

Quando você cria um projeto usando um modelo do Visual Studio na caixa de diálogo **novo projeto** , os parâmetros de modelo são substituídos por cadeias de caracteres para personalizar o projeto. Um parâmetro de modelo é um token especial que começa e termina com um sinal de cifrão, por exemplo, $time $. Os dois parâmetros a seguir são especialmente úteis para habilitar a personalização em projetos baseados no modelo:

- $GUID [1-10] $ é substituído por um novo GUID. Você pode especificar até 10 GUIDs exclusivos, por exemplo, $guid $1.

- $safeprojectname $ é o nome fornecido por um usuário na caixa de diálogo **novo projeto** , modificado para remover todos os caracteres e espaços não seguros.

  Para obter uma lista completa dos parâmetros de modelo, consulte [Parâmetros de modelo](../ide/template-parameters.md).

### <a name="to-substitute-project-template-parameters"></a>Para substituir parâmetros de modelo de projeto

1. No arquivo *SimpleProjectNode.cs* , remova o `AddFileFromTemplate` método.

2. No arquivo * \\ Templates\Projects\ConsoleApp\SimpleProject.MyProj* , localize a \<RootNamespace> propriedade e altere seu valor para $safeprojectname $.

    ```
    <RootNamespace>$safeprojectname$</RootNamespace>
    ```

3. No arquivo * \\ Templates\Projects\SimpleProject\Program.cs* , substitua o conteúdo do arquivo pelo código a seguir:

    ```
    using System;
    using System.Collections.Generic;
    using System.Text;
    using System.Runtime.InteropServices;    // Guid

    namespace $safeprojectname$
    {
        [Guid("$guid1$")]
        public class $safeprojectname$
        {
            static void Main(string[] args)
            {
                Console.WriteLine("Hello VSX!!!");
                Console.ReadKey();
            }
        }
    }
    ```

4. Recompile o projeto SimpleProject e inicie a depuração. A instância experimental deve aparecer.

5. Crie um novo aplicativo de console do SimpleProject. (No painel **tipos de projeto** , selecione **SimpleProject**. Em **modelos instalados do Visual Studio**, selecione **aplicativo de console**.)

6. No projeto criado recentemente, abra *Program.cs*. Ele deve ser semelhante ao seguinte (os valores GUID em seu arquivo serão diferentes.):

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Text;
    using System.Runtime.InteropServices;    // Guid

    namespace Console_Application1
    {
        [Guid("00000000-0000-0000-00000000-00000000)"]
        public class Console_Application1
        {
            static void Main(string[] args)
            {
                Console.WriteLine("Hello VSX!!!");
                Console.ReadKey();
            }
        }
    }
    ```

## <a name="create-a-project-property-page"></a>Criar uma página de propriedades do projeto
Você pode criar uma página de propriedades para o tipo de projeto para que os usuários possam exibir e alterar propriedades em projetos baseados em seu modelo. Esta seção mostra como criar uma página de propriedades independente de configuração. Essa página de propriedades básica usa uma grade de propriedades para exibir as propriedades públicas que você expõe em sua classe de página de propriedades.

Derive sua classe de página de propriedades da `SettingsPage` classe base. A grade de propriedades fornecida pela `SettingsPage` classe reconhece a maioria dos tipos de dados primitivos e sabe como exibi-los. Além disso, a `SettingsPage` classe sabe como manter valores de propriedade no arquivo de projeto.

A página de propriedades criada nesta seção permite alterar e salvar essas propriedades de projeto:

- AssemblyName

- OutputType

- RootNamespace.

1. No arquivo *SimpleProjectPackage.cs* , adicione este `ProvideObject` atributo à `SimpleProjectPackage` classe:

    ```
    [ProvideObject(typeof(GeneralPropertyPage))]
    public sealed class SimpleProjectPackage : ProjectPackage
    ```

    Isso registra a classe da página de propriedades `GeneralPropertyPage` com com.

2. No arquivo *SimpleProjectNode.cs* , adicione esses dois métodos substituídos à `SimpleProjectNode` classe:

    ```csharp
    protected override Guid[] GetConfigurationIndependentPropertyPages()
    {
        Guid[] result = new Guid[1];
        result[0] = typeof(GeneralPropertyPage).GUID;
        return result;
    }
    protected override Guid[] GetPriorityProjectDesignerPages()
    {
        Guid[] result = new Guid[1];
        result[0] = typeof(GeneralPropertyPage).GUID;
        return result;
    }
    ```

    Ambos os métodos retornam uma matriz de GUIDs de página de propriedades. O GUID GeneralPropertyPage é o único elemento na matriz, portanto, a caixa de diálogo **páginas de propriedades** mostrará apenas uma página.

3. Adicione um arquivo de classe chamado *GeneralPropertyPage.cs* ao projeto SimpleProject.

4. Substitua o conteúdo deste arquivo usando o seguinte código:

    ```csharp
    using System;
    using System.Runtime.InteropServices;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.Project;
    using System.ComponentModel;

    namespace SimpleProject
    {
        [ComVisible(true)]
        [Guid("6BC7046B-B110-40d8-9F23-34263D8D2936")]
        public class GeneralPropertyPage : SettingsPage
        {
            private string assemblyName;
            private OutputType outputType;
            private string defaultNamespace;

            public GeneralPropertyPage()
            {
                this.Name = "General";
            }

            [Category("AssemblyName")]
            [DisplayName("AssemblyName")]
            [Description("The output file holding assembly metadata.")]
            public string AssemblyName
            {
                get { return this.assemblyName; }
            }
            [Category("Application")]
            [DisplayName("OutputType")]
            [Description("The type of application to build.")]
            public OutputType OutputType
            {
                get { return this.outputType; }
                set { this.outputType = value; this.IsDirty = true; }
            }
            [Category("Application")]
            [DisplayName("DefaultNamespace")]
            [Description("Specifies the default namespace for added items.")]
            public string DefaultNamespace
            {
                get { return this.defaultNamespace; }
                set { this.defaultNamespace = value; this.IsDirty = true; }
            }

            protected override void BindProperties()
            {
                this.assemblyName = this.ProjectMgr.GetProjectProperty("AssemblyName", true);
                this.defaultNamespace = this.ProjectMgr.GetProjectProperty("RootNamespace", false);

                string outputType = this.ProjectMgr.GetProjectProperty("OutputType", false);
                this.outputType = (OutputType)Enum.Parse(typeof(OutputType), outputType);
            }

            protected override int ApplyChanges()
            {
                this.ProjectMgr.SetProjectProperty("AssemblyName", this.assemblyName);
                this.ProjectMgr.SetProjectProperty("OutputType", this.outputType.ToString());
                this.ProjectMgr.SetProjectProperty("RootNamespace", this.defaultNamespace);
                this.IsDirty = false;

                return VSConstants.S_OK;
            }
        }
    }
    ```

    A `GeneralPropertyPage` classe expõe as três propriedades públicas AssemblyName, OutputType e RootNamespace. Como AssemblyName não tem um método set, ele é exibido como uma propriedade somente leitura. OutputType é uma constante enumerada, portanto aparece como lista suspensa.

    A `SettingsPage` classe base fornece `ProjectMgr` para manter as propriedades. O `BindProperties` método usa `ProjectMgr` para recuperar os valores de propriedade persistente e definir as propriedades correspondentes. O `ApplyChanges` método usa `ProjectMgr` para obter os valores das propriedades e mantê-los no arquivo de projeto. O método de conjunto de propriedades define `IsDirty` como true para indicar que as propriedades precisam ser persistentes. A persistência ocorre quando você salva o projeto ou a solução.

5. Reconstrua a solução SimpleProject e inicie a depuração. A instância experimental deve aparecer.

6. Na instância experimental, crie um novo aplicativo SimpleProject.

7. O Visual Studio chama sua fábrica de projetos para criar um projeto usando o modelo do Visual Studio. O novo arquivo *Program.cs* é aberto no editor de código.

8. Clique com o botão direito do mouse no nó do projeto em **Gerenciador de soluções**e clique em **Propriedades**. A caixa de diálogo **Páginas da Propriedade** é exibida.

    ![Página de propriedades de projeto simples](../extensibility/media/simpproj2_proppage.png "SimpProj2_PropPage")

## <a name="test-the-project-property-page"></a>Testar a página de propriedades do projeto
Agora você pode testar se é possível modificar e alterar os valores de propriedade.

1. Na caixa de diálogo **páginas de propriedades do MyConsoleApplication** , altere o **DefaultNamespace** para **MyApplication**.

2. Selecione a propriedade **OutputType** e, em seguida, selecione **biblioteca de classes**.

3. Clique em **Aplicar** e em **OK**.

4. Reabra a caixa de diálogo **páginas de propriedades** e verifique se as alterações foram persistidas.

5. Feche a instância experimental do Visual Studio.

6. Reabra a instância experimental.

7. Reabra a caixa de diálogo **páginas de propriedades** e verifique se as alterações foram persistidas.

8. Feche a instância experimental do Visual Studio.
    ![Fechar a instância experimental](../extensibility/media/simpproj2_proppage2.png "SimpProj2_PropPage2")
