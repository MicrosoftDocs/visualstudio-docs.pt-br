---
title: Criar um sistema de projeto básico, parte 2 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- writing a project system
- project system
- tutorial
ms.assetid: aee48fc6-a15f-4fd5-8420-7f18824de220
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 4f5a059562db2409dca8eca1fb53c007059456b9
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49928107"
---
# <a name="create-a-basic-project-system-part-2"></a>Criar um sistema de projeto básico, parte 2
A primeiro passo a passo desta série [criar um sistema de projeto básico, parte 1](../extensibility/creating-a-basic-project-system-part-1.md), mostra como criar um sistema de projeto básico. Este passo a passo se baseia no sistema de projeto básico, adicionando um modelo do Visual Studio, uma página de propriedades e outros recursos. Você deve concluir o passo a passo primeiro antes de iniciar este.  
  
 Este passo a passo ensina como criar um tipo de projeto que tem a extensão de nome de arquivo de projeto *.myproj*. Para concluir o passo a passo, você não precisa criar sua própria linguagem porque pega emprestado o passo a passo do sistema de projeto Visual c# existente.  
  
 Este passo a passo ensina como realizar essas tarefas:  
  
-   Crie um modelo do Visual Studio.  
  
-   Implante um modelo do Visual Studio.  
  
-   Criar um nó do filho do tipo de projeto na **novo projeto** caixa de diálogo.  
  
-   Habilite substituição de parâmetro no modelo do Visual Studio.  
  
-   Crie uma página de propriedades do projeto.  
  
> [!NOTE]
>  As etapas neste passo a passo se baseiam em um projeto c#. No entanto, exceto para obter informações específicas, como extensões de nome de arquivo e código, você pode usar as mesmas etapas para um projeto do Visual Basic.  
  
## <a name="create-a-visual-studio-template"></a>Criar um modelo do Visual Studio  
 [Criar um sistema de projeto básico, parte 1](../extensibility/creating-a-basic-project-system-part-1.md) mostra como criar um modelo de projeto básico e adicioná-lo para o sistema de projeto. Ele também mostra como registrar esse modelo com o Visual Studio usando o <xref:Microsoft.VisualStudio.Shell.ProvideProjectFactoryAttribute> atributo, que grava o caminho completo do *\\Templates\Projects\SimpleProject\\* pasta no sistema Registro.  
  
 Usando um modelo do Visual Studio (*. vstemplate* arquivo) em vez de um modelo de projeto básico, você pode controlar como o modelo aparece na **novo projeto** caixa de diálogo e como são os parâmetros de modelo substituído.  Um *. vstemplate* arquivo é um arquivo XML que descreve como arquivos de origem devem ser incluídas quando um projeto é criado usando o modelo de sistema do projeto. O próprio sistema de projeto é criado por meio da coleta a *. vstemplate* arquivo e os arquivos de origem em um *. zip* de arquivo e implantados copiando-o *. zip* para um local que é conhecido para o Visual Studio. Esse processo é explicado em mais detalhes posteriormente neste passo a passo.  
  
1. Na [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], abra a solução de SimpleProject que você criou seguindo [criar um sistema de projeto básico, parte 1](../extensibility/creating-a-basic-project-system-part-1.md).  
  
2. No *SimpleProjectPackage.cs* arquivo, localize o atributo ProvideProjectFactory. Substitua o segundo parâmetro (o nome do projeto) com null e o quarto parâmetro (o caminho para a pasta de modelo de projeto) ". \\\NullPath ", da seguinte maneira.  
  
   ```  
   [ProvideProjectFactory(typeof(SimpleProjectFactory), null,  
       "Simple Project Files (*.myproj);*.myproj", "myproj", "myproj",  
       ".\\NullPath",  
   LanguageVsTemplate = "SimpleProject")]  
   ```  
  
3. Adicionar um arquivo XML denominado *SimpleProject.vstemplate* para o *\\Templates\Projects\SimpleProject\\* pasta.  
  
4. Substitua o conteúdo do *SimpleProject.vstemplate* com o código a seguir.  
  
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
  
5. No **propriedades** janela, selecione todos os cinco arquivos na *\\Templates\Projects\SimpleProject\\* pasta e defina o **Build Action** para **ZipProject**.  
  
   ![Pasta de projeto simples](../extensibility/media/simpproj2.png "SimpProj2")  
  
   O \<TemplateData > seção determina o local e a aparência do tipo no projeto SimpleProject a **novo projeto** caixa de diálogo, da seguinte maneira:  
  
- O \<nome > elemento nomeia o modelo de projeto para ser SimpleProject aplicativo.  
  
- O \<descrição > elemento contém a descrição que aparece na **novo projeto** caixa de diálogo quando o modelo de projeto é selecionado.  
  
- O \<ícone > elemento Especifica o ícone que aparece junto com o tipo de projeto SimpleProject.  
  
- O \<ProjectType > elemento nomeia o tipo de projeto na **novo projeto** caixa de diálogo. Esse nome substitui o parâmetro de nome de projeto do atributo ProvideProjectFactory.  
  
  > [!NOTE]
  >  O \<ProjectType > elemento deve corresponder a `LanguageVsTemplate` argumento do `ProvideProjectFactory` atributo no arquivo SimpleProjectPackage.cs.  
  
  O \<TemplateContent > seção descreve esses arquivos que são gerados quando um novo projeto é criado:  
  
- *SimpleProject.myproj*  
  
- *Program.cs*  
  
- *AssemblyInfo.cs*  
  
  Todos os três arquivos têm `ReplaceParameters` definida como true, o que permite a substituição de parâmetro.  O *Program.cs* arquivo tem `OpenInEditor` definido como true, o que faz com que o arquivo a ser aberto no editor de código quando um projeto é criado.  
  
  Para obter mais informações sobre os elementos no esquema de modelo do Visual Studio, consulte o [referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md).  
  
> [!NOTE]
>  Se um projeto tiver mais de um modelo do Visual Studio, cada modelo está em uma pasta separada. Todos os arquivos nessa pasta devem ter o **ação de compilação** definido como **ZipProject**.  
  
## <a name="adding-a-minimal-vsct-file"></a>Adicionando um arquivo. VSCT mínimo  
 Visual Studio deve ser executado no modo de instalação para reconhecer um modelo do Visual Studio novo ou modificado. Modo de instalação requer uma *VSCT* arquivo esteja presente. Portanto, você deve adicionar um mínimo *VSCT* arquivo ao projeto.  
  
1.  Adicionar um arquivo XML denominado *SimpleProject.vsct* ao projeto SimpleProject.  
  
2.  Substitua o conteúdo do *SimpleProject.vsct* arquivo pelo código a seguir.  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <CommandTable  
      xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable">  
    </CommandTable>  
    ```  
  
3.  Defina as **ação de compilação** desse arquivo como **VSCTCompile**. Você pode fazer isso apenas na *. csproj* arquivo, não na **propriedades** janela. Certifique-se de que o **ação de compilação** desse arquivo é definido como **None** neste momento.  
  
    1.  Clique com botão direito no nó SimpleProject e, em seguida, clique em **SimpleProject.csproj editar**.  
  
    2.  No *. csproj* do arquivo, localize a *SimpleProject.vsct* item.  
  
        ```  
        <None Include="SimpleProject.vsct" />  
        ```  
  
    3.  Altere a ação de compilação para **VSCTCompile**.  
  
        ```  
        <VSCTCompile Include="SimpleProject.vsct" />  
        ```  
  
    4.  o arquivo de projeto e feche o editor.  
  
    5.  Salve o nó SimpleProject e, em seguida, nos **Gerenciador de soluções** clique em **recarregar projeto**.  
  
## <a name="examine-the-visual-studio-template-build-steps"></a>Examine as etapas de criação de modelo do Visual Studio  
 O sistema de build do projeto de VSPackage normalmente executa o Visual Studio no modo de instalação quando o *. vstemplate* arquivo for alterado ou o projeto que contém o *. vstemplate* arquivo será recriado. Você pode acompanhar, definindo o nível de detalhamento do MSBuild ao Normal ou superior.  
  
1. No menu **Ferramentas**, clique em **Opções**.  
  
2. Expanda o **projetos e soluções** nó e, em seguida, selecione **compilar e executar**.  
  
3. Definir **detalhes da saída de build do projeto do MSBuild** à **Normal**. Clique em **OK**.  
  
4. Recompile o projeto SimpleProject.  
  
   A etapa de compilação para criar o *. zip* arquivo de projeto deve se parecer com o exemplo a seguir.  
  
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
 Modelos do Visual Studio não contêm informações de caminho. Portanto, o modelo *. zip* arquivo deve ser implantado em um local conhecido para o Visual Studio. O local da pasta ProjectTemplates é normalmente *\Microsoft\VisualStudio\14.0Exp\ProjectTemplates < % LOCALAPPDATA % >*.  
  
 Para implantar sua fábrica de projeto, o programa de instalação deve ter privilégios de administrador. Ela implanta modelos sob o nó de instalação do Visual Studio: *...\Microsoft Visual Studio 14.0\Common7\IDE\ProjectTemplates*.  
  
## <a name="test-a-visual-studio-template"></a>Testar um modelo do Visual Studio  
 Teste sua fábrica de projeto para ver se ele cria uma hierarquia de projeto usando o modelo do Visual Studio.  
  
1. Redefina a instância experimental do SDK do Visual Studio.  
  
    Na [!INCLUDE[win7](../debugger/includes/win7_md.md)]: na **iniciar** menu, localizar o **Microsoft Visual Studio para o Microsoft Visual Studio/ferramentas SDK** pasta e, em seguida, selecione **redefinir o Microsoft Visual Studio Experimental instância**.  
  
    Em versões posteriores do Windows: sobre o **inicie** tela, digite **redefinir o Microsoft Visual Studio \<versão > instância Experimental**.  
  
2. É exibida uma janela de prompt de comando. Quando você vir as palavras **pressione qualquer tecla para continuar**, clique em **ENTER**. Depois de fecha a janela, abra o Visual Studio.  
  
3. Recompile o projeto SimpleProject e iniciar a depuração. A instância experimental é exibida.  
  
4. Na instância experimental, crie um projeto de SimpleProject. No **novo projeto** caixa de diálogo, selecione **SimpleProject**.  
  
5. Você deve ver uma nova instância da SimpleProject.  
  
   ![Nova instância de projeto simples](../extensibility/media/simpproj2_newproj.png "SimpProj2_NewProj")  
  
   ![Minha instância do novo projeto](../extensibility/media/simpproj2_myproj.png "SimpProj2_MyProj")  
  
## <a name="create-a-project-type-child-node"></a>Criar um nó de filho de tipo de projeto  
 Você pode adicionar um nó filho para um nó de tipo de projeto na **novo projeto** caixa de diálogo.  Por exemplo, para o tipo de projeto SimpleProject, você poderia ter nós filho para aplicativos de console, aplicativos de janela, aplicativos web e assim por diante.  
  
 Nós filho são criados alterando o arquivo de projeto e adicionando \<OutputSubPath > filhos para o \<ZipProject > elementos. Quando um modelo é copiado durante a compilação ou implantação, todos os nós filho se torna uma subpasta da pasta de modelos de projeto.  
  
 Esta seção mostra como criar um nó filho do Console para o tipo de projeto SimpleProject.  
  
1.  Renomeie o *\\Templates\Projects\SimpleProject\\* pasta a ser  *\\Templates\Projects\ConsoleApp\\*.  
  
2.  No **propriedades** janela, selecione todos os cinco arquivos na *\\Templates\Projects\ConsoleApp\\* pasta e verifique se o **Build Action**é definido como **ZipProject**.  
  
3.  No arquivo SimpleProject.vstemplate, adicione a seguinte linha no final o \<TemplateData > seção logo antes da marca de fechamento.  
  
    ```  
    <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>  
    ```  
  
     Isso faz com que o modelo de aplicativo de Console deve ser exibido no nó filho Console e no nó pai SimpleProject, que é um nível acima do nó filho.  
  
4.  Salvar a *SimpleProject.vstemplate* arquivo.  
  
5.  No *. csproj* do arquivo, adicione \<OutputSubPath > para cada um dos elementos ZipProject. Descarregue o projeto, como antes e edite o arquivo de projeto.  
  
6.  Localize o \<ZipProject > elementos. A cada \<ZipProject > elemento, adicionar um \<OutputSubPath > elemento e dê a ela o valor de Console. O ZipProject  
  
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
  
7.  Adicione isso \<PropertyGroup > ao arquivo de projeto:  
  
    ```  
    <PropertyGroup>  
      <VsTemplateLanguage>SimpleProject</VsTemplateLanguage>  
    </PropertyGroup>  
    ```  
  
8.  Salve o arquivo de projeto e recarregar o projeto.  
  
## <a name="test-the-project-type-child-node"></a>O nó de filho de tipo de projeto de teste  
 Testar o arquivo de projeto modificado para ver se o **Console** nó filho é exibido na **novo projeto** caixa de diálogo.  
  
1. Execute o **redefinir o Visual Studio instância Experimental do Microsoft** ferramenta.  
  
2. Recompile o projeto SimpleProject e iniciar a depuração. A instância experimental deve ser exibida  
  
3. No **novo projeto** caixa de diálogo, clique o **SimpleProject** nó. O **aplicativo de Console** modelo deve aparecer na **modelos** painel.  
  
4. Expanda o **SimpleProject** nó. O **Console** nó filho deve aparecer. O **aplicativo SimpleProject** modelo continuará aparecendo na **modelos** painel.  
  
5. Clique em **Cancelar** e parar a depuração.  
  
   ![Pacote cumulativo de atualizações de projeto simples](../extensibility/media/simpproj2_rollup.png "SimpProj2_Rollup")  
  
   ![Nó de Console simples do projeto](../extensibility/media/simpproj2_subfolder.png "SimpProj2_Subfolder")  
  
## <a name="substitute-project-template-parameters"></a>Substituir parâmetros de modelo de projeto  
 [Criar um sistema de projeto básico, parte 1](../extensibility/creating-a-basic-project-system-part-1.md) mostrou como substituir o `ProjectNode.AddFileFromTemplate` método para fazer um tipo básico de substituição de parâmetro de modelo. Esta seção ensina como usar os parâmetros de modelo do Visual Studio mais sofisticados.  
  
 Quando você cria um projeto usando um modelo do Visual Studio na **novo projeto** caixa de diálogo modelo de parâmetros são substituídos por cadeias de caracteres para personalizar o projeto. Um parâmetro de modelo é um token especial que começa e termina com um sinal de cifrão, por exemplo, $ $time. Os dois parâmetros seguintes são especialmente úteis para possibilitar a personalização em projetos que são baseados no modelo:  
  
- $ $GUID [1-10] é substituído por um novo Guid. Você pode especificar até 10 GUIDs exclusivos, por exemplo, guid1 $$.  
  
- $ $safeprojectname é o nome fornecido por um usuário a **novo projeto** caixa de diálogo, modificada para remover todos os caracteres desprotegidos e espaços.  
  
  Para obter uma lista completa dos parâmetros de modelo, consulte [Parâmetros de modelo](../ide/template-parameters.md).  
  
### <a name="to-substitute-project-template-parameters"></a>Substituir parâmetros de modelo de projeto  
  
1.  No *SimpleProjectNode.cs* do arquivo, remova o `AddFileFromTemplate` método.  
  
2.  No  *\\Templates\Projects\ConsoleApp\SimpleProject.myproj* do arquivo, localize o \<RootNamespace > propriedade e altere seu valor para $ $safeprojectname.  
  
    ```  
    <RootNamespace>$safeprojectname$</RootNamespace>  
    ```  
  
3.  No  *\\Templates\Projects\SimpleProject\Program.cs* de arquivo, substitua o conteúdo do arquivo pelo código a seguir:  
  
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
  
4.  Recompile o projeto SimpleProject e iniciar a depuração. A instância experimental deve aparecer.  
  
5.  Crie um novo aplicativo de SimpleProject Console. (Na **tipos de projeto** painel, selecione **SimpleProject**. Sob **modelos instalados do Visual Studio**, selecione **aplicativo de Console**.)  
  
6.  No projeto recém-criado, abra *Program.cs*. Ele deve ser algo semelhante ao seguinte (os valores GUID em seu arquivo serão diferentes.):  
  
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
  
## <a name="creatr-a-project-property-page"></a>Creatr uma página de propriedades do projeto  
 Você pode criar uma página de propriedades para o tipo de projeto para que os usuários podem exibir e alterar as propriedades em projetos que são baseados no seu modelo. Esta seção mostra como criar uma página de propriedades de configuração independente. Esta página de propriedades básicas usa uma grade de propriedades para exibir as propriedades públicas que expõem em sua classe de página de propriedade.  
  
 Derive sua classe de página de propriedade do `SettingsPage` classe base. A grade de propriedades fornecida pelo `SettingsPage` classe está ciente dos tipos de dados mais primitivos e sabe como exibi-los.  Além disso, o `SettingsPage` classe sabe como manter valores de propriedade para o arquivo de projeto.  
  
 A página de propriedades que você cria essa seção permite que você alterar e salvar essas propriedades do projeto:  
  
-   AssemblyName  
  
-   OutputType  
  
-   RootNamespace.  
  
1. No *SimpleProjectPackage.cs* do arquivo, adicione isso `ProvideObject` de atributo para o `SimpleProjectPackage` classe:  
  
   ```  
   [ProvideObject(typeof(GeneralPropertyPage))]  
   public sealed class SimpleProjectPackage : ProjectPackage  
   ```  
  
    Isso registra a classe de página de propriedade `GeneralPropertyPage` com COM.  
  
2. No *SimpleProjectNode.cs* do arquivo, adicione esses dois métodos substituídos para o `SimpleProjectNode` classe:  
  
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
  
    Ambos os métodos retornam uma matriz de GUIDs de página de propriedades.  O GUID GeneralPropertyPage é o único elemento da matriz, portanto, o **páginas de propriedade** caixa de diálogo mostrará apenas uma página.  
  
3. Adicione um arquivo de classe chamado *GeneralPropertyPage.cs* ao projeto SimpleProject.  
  
4. Substitua o conteúdo desse arquivo, usando o código a seguir:  
  
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
               this.assemblyName = this.ProjectMgr.GetProjectProperty(  
   "AssemblyName", true);  
               this.defaultNamespace = this.ProjectMgr.GetProjectProperty(  
   "RootNamespace", false);  
  
               string outputType = this.ProjectMgr.GetProjectProperty(  
   "OutputType", false);  
               this.outputType =   
   (OutputType)Enum.Parse(typeof(OutputType), outputType);  
           }  
  
           protected override int ApplyChanges()  
           {  
               this.ProjectMgr.SetProjectProperty(  
   "AssemblyName", this.assemblyName);  
               this.ProjectMgr.SetProjectProperty(  
   "OutputType", this.outputType.ToString());  
               this.ProjectMgr.SetProjectProperty(  
   "RootNamespace", this.defaultNamespace);  
               this.IsDirty = false;  
  
               return VSConstants.S_OK;  
           }  
       }  
   }  
   ```  
  
    O `GeneralPropertyPage` classe expõe três propriedades públicas AssemblyName OutputType e RootNamespace. Como AssemblyName não tem nenhum método set, ele será exibido como uma propriedade somente leitura. Tipo de saída é uma constante enumerada, para que ele apareça como a lista suspensa.  
  
    O `SettingsPage` classe base fornece `ProjectMgr` para persistir as propriedades. O `BindProperties` usos de método `ProjectMgr` para recuperar os valores de propriedade persistente e definir as propriedades correspondentes.  O `ApplyChanges` método usa `ProjectMgr` para obter os valores das propriedades e mantê-los ao arquivo de projeto. Método conjuntos de definir a propriedade `IsDirty` como true para indicar que as propriedades precisam ser mantidos.  A persistência ocorre quando você salvar o projeto ou solução.  
  
5. Recompile a solução SimpleProject e iniciar a depuração. A instância experimental deve aparecer.  
  
6. Na instância experimental, crie um novo aplicativo SimpleProject.  
  
7. O Visual Studio chama sua fábrica de projeto para criar um projeto usando o modelo do Visual Studio. O novo *Program.cs* arquivo é aberto no editor de códigos.  
  
8. Clique com botão direito no nó do projeto no **Gerenciador de soluções**e, em seguida, clique em **propriedades**. A caixa de diálogo **Páginas de Propriedades** é exibida.  
  
   ![Página de propriedades de projeto simples](../extensibility/media/simpproj2_proppage.png "SimpProj2_PropPage")  
  
## <a name="test-the-project-property-page"></a>A página de propriedades do projeto de teste
 Agora você pode testar se é possível modificar e alterar valores de propriedade.  
  
1. No **páginas de propriedade MyConsoleApplication** caixa de diálogo, altere o **DefaultNamespace** para **MyApplication**.  
  
2. Selecione o **OutputType** propriedade e, em seguida, selecione **biblioteca de classes**.  
  
3. Clique em **Apply**e, em seguida, clique em **Okey**.  
  
4. Reabra o **páginas de propriedade** caixa de diálogo caixa e verifique se que suas alterações foram mantidas.  
  
5. Feche a instância experimental do Visual Studio.  
  
6. Reabra a instância experimental.  
  
7. Reabra o **páginas de propriedade** caixa de diálogo caixa e verifique se que suas alterações foram mantidas.  
  
8. Feche a instância experimental do Visual Studio.  
  
   ![Feche a instância experimental](../extensibility/media/simpproj2_proppage2.png "SimpProj2_PropPage2")