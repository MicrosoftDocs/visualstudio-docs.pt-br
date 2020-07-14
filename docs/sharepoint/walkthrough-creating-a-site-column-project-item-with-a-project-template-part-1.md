---
title: Criar item de projeto de coluna de site com modelo de projeto, parte 1
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project items, defining your own types
- project items [SharePoint development in Visual Studio], defining your own types
- SharePoint projects, creating custom templates
- SharePoint development in Visual Studio, defining new project item types
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: fea425da8a6e49643997151c6273fbbffc7033db
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016505"
---
# <a name="walkthrough-create-a-site-column-project-item-with-a-project-template-part-1"></a>Walkthrough: criar um item de projeto de coluna de site com um modelo de projeto, parte 1
  Projetos do SharePoint são contêineres para um ou mais itens de projeto do SharePoint. Você pode estender o sistema de projeto do SharePoint no Visual Studio criando seus próprios tipos de item de projeto do SharePoint e, em seguida, associando-os a um modelo de projeto. Neste tutorial, você definirá um tipo de item de projeto para criar uma coluna de site e, em seguida, criará um modelo de projeto que pode ser usado para criar um novo projeto que contém um item de projeto de coluna de site.

 Este tutorial demonstra as seguintes tarefas:

- Criar uma extensão do Visual Studio que define um novo tipo de item de projeto do SharePoint para uma coluna de site. O tipo de item de projeto inclui uma propriedade personalizada simples que aparece na janela **Propriedades** .

- Criando um [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] modelo de projeto para o item de projeto.

- Criando um [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de VSIX (extensão) para implantar o modelo de projeto e o assembly de extensão.

- Depurando e testando o item do projeto.

  Trata-se de uma explicação autônoma. Depois de concluir este passo a passos, você pode aprimorar o item de projeto adicionando um assistente ao modelo de projeto. Para obter mais informações, consulte [Walkthrough: criar um item de projeto de coluna de site com um modelo de projeto, parte 2](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md).

> [!NOTE]
> Para obter uma série de fluxos de trabalho de exemplo, consulte [exemplos de fluxo de trabalho do SharePoint](/sharepoint/dev/general-development/sharepoint-workflow-samples).

## <a name="prerequisites"></a>Pré-requisitos
 Você precisa dos seguintes componentes no computador de desenvolvimento para concluir este passo a passos:

- Edições com suporte do Microsoft Windows, SharePoint e [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] .

- O [!include[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)]. Este tutorial usa o modelo de **projeto VSIX** no SDK para criar um pacote VSIX para implantar o item de projeto. Para obter mais informações, consulte [estender as ferramentas do SharePoint no Visual Studio](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md).

  O conhecimento do conceito a seguir é útil, mas não obrigatório, para concluir o passo a passos:

- Colunas do site no SharePoint. Para obter mais informações, consulte [colunas](/previous-versions/office/developer/sharepoint-2010/ms196085(v=office.14)).

- Modelos de projeto no Visual Studio. Para obter mais informações, consulte [Criando modelos de item e de projeto](../ide/creating-project-and-item-templates.md).

## <a name="create-the-projects"></a>Criar os projetos
 Para concluir este passo a passos, você precisa criar três projetos:

- Um projeto VSIX. Este projeto cria o pacote VSIX para implantar o item de projeto coluna do site e o modelo do projeto.

- Um projeto de modelo de projeto. Este projeto cria um modelo de projeto que pode ser usado para criar um novo projeto do SharePoint que contém o item de projeto de coluna do site.

- Um projeto de biblioteca de classes. Este projeto que implementa uma extensão do Visual Studio que define o comportamento do item de projeto de coluna de site.

  Inicie o passo a passos criando os projetos.

#### <a name="to-create-the-vsix-project"></a>Para criar o projeto VSIX

1. Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].

2. Na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**.

3. Na parte superior da caixa de diálogo **novo projeto** , certifique-se de que **.NET Framework 4,5** seja escolhido na lista de versões do .NET Framework.

4. Expanda os nós **Visual Basic** ou **Visual C#** e escolha o nó **extensibilidade** .

    > [!NOTE]
    > O nó **extensibilidade** só estará disponível se você instalar o SDK do Visual Studio. Para obter mais informações, consulte a seção pré-requisitos anteriormente neste tópico.

5. Na lista de modelos de projeto, escolha **projeto VSIX**.

6. Na caixa **nome** , digite **SiteColumnProjectItem**e, em seguida, escolha o botão **OK** .

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Adiciona o projeto **SiteColumnProjectItem** ao **Gerenciador de soluções**.

#### <a name="to-create-the-project-template-project"></a>Para criar o projeto de modelo de projeto

1. No **Gerenciador de soluções**, abra o menu de atalho para o nó da solução, escolha **Adicionar**e, em seguida, escolha **novo projeto**.

2. Na parte superior da caixa de diálogo **novo projeto** , certifique-se de que **.NET Framework 4,5** seja escolhido na lista de versões do .NET Framework.

3. Expanda o nó **Visual C#** ou **Visual Basic** e, em seguida, escolha o nó **extensibilidade** .

4. Na lista de modelos de projeto, escolha o modelo de projeto **C#** ou modelo de **modelo de projeto de Visual Basic** .

5. Na caixa **nome** , digite **SiteColumnProjectTemplate**e, em seguida, escolha o botão **OK** .

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Adiciona o projeto **SiteColumnProjectTemplate** à solução.

6. Exclua o arquivo de código Class1 do projeto.

7. Se você criou um projeto Visual Basic, exclua também os seguintes arquivos do projeto:

    - *MyApplication. designer. vb*

    - MyApplication. MyApp

    - *Resources. designer. vb*

    - *Recursos. resx*

    - *Settings. designer. vb*

    - Settings. Settings

#### <a name="to-create-the-extension-project"></a>Para criar o projeto de extensão

1. No **Gerenciador de soluções**, abra o menu de atalho para o nó da solução, escolha **Adicionar**e, em seguida, escolha **novo projeto**.

2. Na parte superior da caixa de diálogo **novo projeto** , certifique-se de que **.NET Framework 4,5** seja escolhido na lista de versões do .NET Framework.

3. Expanda os nós do **Visual C#** ou do **Visual Basic** , escolha o nó **Windows** e, em seguida, escolha o modelo **biblioteca de classes** .

4. Na caixa **nome** , digite **projectItemTypeDefinition** e, em seguida, escolha o botão **OK** .

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Adiciona o projeto **projectItemTypeDefinition** à solução e abre o arquivo de código de Class1 padrão.

5. Exclua o arquivo de código Class1 do projeto.

## <a name="configure-the-extension-project"></a>Configurar o projeto de extensão
 Adicione arquivos de código e referências de assembly para configurar o projeto de extensão.

#### <a name="to-configure-the-project"></a>Para configurar o projeto

1. No projeto ProjectItemTypeDefinition, adicione um arquivo de código chamado **SiteColumnProjectItemTypeProvider**.

2. Na barra de menus, escolha **projeto**  >  **Adicionar referência**.

3. Na caixa de diálogo **Gerenciador de referências-projectItemTypeDefinition** , expanda o nó **assemblies** , escolha o nó **estrutura** e marque a caixa de seleção System. ComponentModel. composição.

4. Escolha o nó **extensões** , marque a caixa de seleção ao lado do assembly Microsoft. VisualStudio. SharePoint e, em seguida, escolha o botão **OK** .

## <a name="define-the-new-sharepoint-project-item-type"></a>Definir o novo tipo de item de projeto do SharePoint
 Crie uma classe que implemente a <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> interface para definir o comportamento do novo tipo de item de projeto. Implemente essa interface sempre que desejar definir um novo tipo de item de projeto.

#### <a name="to-define-the-new-sharepoint-project-item-type"></a>Para definir o novo tipo de item de projeto do SharePoint

1. No arquivo de código **SiteColumnProjectItemTypeProvider** , substitua o código padrão pelo código a seguir e salve o arquivo.

     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#1](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projectitemtypedefinition/sitecolumnprojectitemtypeprovider.cs#1)]
     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#1](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projectitemtypedefinition/sitecolumnprojectitemtypeprovider.vb#1)]

## <a name="create-a-visual-studio-project-template"></a>Criar um modelo de projeto do Visual Studio
 Ao criar um modelo de projeto, você permite que outros desenvolvedores criem projetos do SharePoint que contenham itens de projeto de coluna de site. Um modelo de projeto do SharePoint inclui arquivos que são necessários para todos os projetos no Visual Studio, como arquivos *. csproj* ou *. vbproj* e *. vstemplate* , e arquivos que são específicos para projetos do SharePoint. Para obter mais informações, consulte [criar modelos de item e modelos de projeto para itens de projeto do SharePoint](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md).

 Neste procedimento, você cria um projeto do SharePoint vazio para gerar os arquivos que são específicos para projetos do SharePoint. Em seguida, adicione esses arquivos ao projeto SiteColumnProjectTemplate para que eles sejam incluídos no modelo gerado neste projeto. Você também configura o arquivo de projeto SiteColumnProjectTemplate para especificar onde o modelo de projeto aparece na caixa de diálogo **novo projeto** .

#### <a name="to-create-the-files-for-the-project-template"></a>Para criar os arquivos para o modelo de projeto

1. Inicie uma segunda instância do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] com credenciais administrativas.

2. Crie um projeto do SharePoint 2010 chamado **BaseSharePointProject**.

   > [!IMPORTANT]
   > No **Assistente para personalização do SharePoint**, não selecione o botão de opção **implantar como uma solução de farm** .

3. Adicione um item de elemento vazio ao projeto e, em seguida, nomeie o item **campo1**.

4. Salve o projeto e, em seguida, feche a segunda instância do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] .

5. Na instância do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] que tem a solução SiteColumnProjectItem aberta, em **Gerenciador de soluções**, abra o menu de atalho para o nó do projeto **SiteColumnProjectTemplate** , escolha **Adicionar**e, em seguida, escolha **Item existente**.

6. Na caixa de diálogo **Adicionar item existente** , abra a lista de extensões de arquivo e, em seguida, escolha **todos os arquivos ( \* . \* )**.

7. No diretório que contém o projeto BaseSharePointProject, selecione o arquivo Key. snk e, em seguida, escolha o botão **Adicionar** .

   > [!NOTE]
   > Neste tutorial, o modelo de projeto que você cria usa o mesmo arquivo Key. SNK para assinar cada projeto que é criado usando o modelo. Para saber como expandir este exemplo para criar um arquivo Key. SNK diferente para cada instância de projeto, consulte [passo a passos: criar um item de projeto de coluna de site com um modelo de projeto, parte 2](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md).

8. Repita as etapas 5-8 para adicionar os seguintes arquivos das subpastas especificadas no diretório BaseSharePointProject:

   - *\Field1\Elements.xml*

   - *\Field1\SharePointProjectItem.spdata*

   - *\Features\Feature1\Feature1.feature*

   - *\Features\Feature1\Feature1.Template.xml*

   - *\Package\Package.package*

   - *\Package\Package.Template.xml*

     Adicione esses arquivos diretamente ao projeto SiteColumnProjectTemplate; Não recrie as subpastas campo1, Features ou Package no projeto. Para obter mais informações sobre esses arquivos, consulte [criar modelos de item e modelos de projeto para itens de projeto do SharePoint](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md).

#### <a name="to-configure-how-developers-discover-the-project-template-in-the-new-project-dialog-box"></a>Para configurar como os desenvolvedores descobrem o modelo de projeto na caixa de diálogo novo projeto

1. No **Gerenciador de soluções**, abra o menu de atalho para o nó do projeto **SiteColumnProjectTemplate** e escolha **descarregar projeto**. Se for solicitado que você salve as alterações em todos os arquivos, escolha o botão **Sim** .

2. Abra o menu de atalho para o nó **SiteColumnProjectTemplate** novamente e escolha **Editar SiteColumnProjectTemplate. csproj** ou **Editar SiteColumnProjectTemplate. vbproj**.

3. No arquivo de projeto, localize o seguinte `VSTemplate` elemento.

    ```xml
    <VSTemplate Include="SiteColumnProjectTemplate.vstemplate">
    ```

4. Substitua esse elemento pelo XML a seguir.

    ```xml
    <VSTemplate Include="SiteColumnProjectTemplate.vstemplate">
      <OutputSubPath>SharePoint\SharePoint14</OutputSubPath>
    </VSTemplate>
    ```

     O `OutputSubPath` elemento especifica pastas adicionais no caminho em que o modelo de projeto é criado quando você cria o projeto. As pastas especificadas aqui garantem que o modelo de projeto estará disponível somente quando os clientes abrirem a caixa de diálogo **novo projeto** , expandir o nó do **SharePoint** e, em seguida, escolher o nó **2010** .

5. Salve e feche o arquivo.

6. No **Gerenciador de soluções**, abra o menu de atalho para o projeto **SiteColumnProjectTemplate** e, em seguida, escolha **recarregar projeto**.

## <a name="edit-the-project-template-files"></a>Editar os arquivos de modelo de projeto
 No projeto SiteColumnProjectTemplate, edite os seguintes arquivos para definir o comportamento do modelo de projeto:

- *AssemblyInfo.cs* ou *AssemblyInfo. vb*

- *Elements.xml*

- *SharePointProjectItem. COMDATA*

- *Feature1. Feature*

- *Pacote. Package*

- *SiteColumnProjectTemplate. vstemplate*

- *ProjectTemplate. csproj* ou *ProjectTemplate. vbproj*

  Nos procedimentos a seguir, você adicionará parâmetros substituíveis a alguns desses arquivos. Um parâmetro substituível é um token que inicia e termina com o caractere de cifrão ($). Quando um usuário usa esse modelo de projeto para criar um projeto, o Visual Studio substitui automaticamente esses parâmetros no novo projeto com valores específicos. Para obter mais informações, consulte [parâmetros substituíveis](../sharepoint/replaceable-parameters.md).

#### <a name="to-edit-the-assemblyinfocs-or-assemblyinfovb-file"></a>Para editar o arquivo AssemblyInfo.cs ou AssemblyInfo. vb

1. No projeto SiteColumnProjectTemplate, abra o arquivo *AssemblyInfo.cs* ou *AssemblyInfo. vb* e, em seguida, adicione a seguinte instrução à parte superior dele:

    ```vb
    Imports System.Security
    ```

    ```csharp
    using System.Security;
    ```

     Quando a propriedade de **solução de área restrita** de um projeto do SharePoint é definida como **true**, o Visual Studio adiciona o <xref:System.Security.AllowPartiallyTrustedCallersAttribute> ao arquivo de código AssemblyInfo. No entanto, o arquivo de código AssemblyInfo no modelo de projeto não importa o <xref:System.Security> namespace por padrão. Você deve adicionar essa instrução **using** ou **Imports** para evitar erros de compilação.

2. Salve e feche o arquivo.

#### <a name="to-edit-the-elementsxml-file"></a>Para editar o arquivo de Elements.xml

1. No projeto SiteColumnProjectTemplate, substitua o conteúdo do arquivo *Elements.xml* pelo seguinte XML.

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
      <Field ID="{$guid5$}"
          Name="$safeprojectname$"
          DisplayName="$projectname$"
          Type="Text"
          Group="Custom Columns">
      </Field>
    </Elements>
    ```

     O novo XML adiciona um `Field` elemento que define o nome da coluna site, seu tipo base e o grupo no qual listar a coluna site na galeria. Para obter mais informações sobre o conteúdo desse arquivo, consulte [esquema de definição de campo](/previous-versions/office/developer/sharepoint-2010/ms196289(v=office.14)).

2. Salve e feche o arquivo.

#### <a name="to-edit-the-sharepointprojectitemspdata-file"></a>Para editar o arquivo SharePointProjectItem. COMDATA

1. No projeto SiteColumnProjectTemplate, substitua o conteúdo do arquivo *SharePointProjectItem. COMDATA* pelo seguinte XML.

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <ProjectItem Type="Contoso.SiteColumn" DefaultFile="Elements.xml"
                xmlns="http://schemas.microsoft.com/VisualStudio/2010/SharePointTools/SharePointProjectItemModel">
     <Files>
       <ProjectItemFile Source="Elements.xml" Target="$safeprojectname$\" Type="ElementManifest" />
     </Files>
   </ProjectItem>
   ```

    O novo XML faz as seguintes alterações no arquivo:

   - Altera o `Type` atributo do `ProjectItem` elemento para a mesma cadeia de caracteres que é passada para a <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute> na definição de item do projeto (a `SiteColumnProjectItemTypeProvider` classe que você criou anteriormente neste guia).

   - Remove os `SupportedTrustLevels` `SupportedDeploymentScopes` atributos e do `ProjectItem` elemento. Esses valores de atributo são desnecessários porque os níveis de confiança e os escopos de implantação estão especificados na `SiteColumnProjectItemTypeProvider` classe no projeto ProjectItemTypeDefinition.

     Para obter mais informações sobre o conteúdo de arquivos *. OnData* , consulte [referência de esquema de item de projeto do SharePoint](../sharepoint/sharepoint-project-item-schema-reference.md).

2. Salve e feche o arquivo.

#### <a name="to-edit-the-feature1feature-file"></a>Para editar o arquivo Feature1. Feature

1. No projeto SiteColumnProjectTemplate, substitua o conteúdo do arquivo *Feature1. Feature* pelo XML a seguir.

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <feature xmlns:dm0="http://schemas.microsoft.com/VisualStudio/2008/DslTools/Core" dslVersion="1.0.0.0" Id="$guid4$" featureId="$guid4$"
            imageUrl="" solutionId="00000000-0000-0000-0000-000000000000" title="Site Column Feature1" version=""
            deploymentPath="$SharePoint.Project.FileNameWithoutExtension$_$SharePoint.Feature.FileNameWithoutExtension$"
            xmlns="http://schemas.microsoft.com/VisualStudio/2008/SharePointTools/FeatureModel">
     <projectItems>
       <projectItemReference itemId="$guid2$" />
     </projectItems>
   </feature>
   ```

    O novo XML faz as seguintes alterações no arquivo:

   - Altera os valores dos `Id` atributos e `featureId` do `feature` elemento para `$guid4$` .

   - Altera os valores do `itemId` atributo do `projectItemReference` elemento para `$guid2$` .

     Para obter mais informações sobre arquivos *. Feature* , consulte [criar modelos de item e modelos de projeto para itens de projeto do SharePoint](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md).

2. Salve e feche o arquivo.

#### <a name="to-edit-the-packagepackage-file"></a>Para editar o pacote. arquivo de pacote

1. No projeto SiteColumnProjectTemplate, substitua o conteúdo do arquivo *Package. Package* pelo XML a seguir.

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <package xmlns:dm0="http://schemas.microsoft.com/VisualStudio/2008/DslTools/Core" dslVersion="1.0.0.0"
            Id="$guid3$" solutionId="$guid3$" resetWebServer="false" name="$safeprojectname$"
            xmlns="http://schemas.microsoft.com/VisualStudio/2008/SharePointTools/PackageModel">
     <features>
       <featureReference itemId="$guid4$" />
     </features>
   </package>
   ```

    O novo XML faz as seguintes alterações no arquivo:

   - Altera os valores dos `Id` atributos e `solutionId` do `package` elemento para `$guid3$` .

   - Altera os valores do `itemId` atributo do `featureReference` elemento para `$guid4$` .

     Para obter mais informações sobre arquivos *. Package* , consulte [criar modelos de item e modelos de projeto para itens de projeto do SharePoint](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md).

2. Salve e feche o arquivo.

#### <a name="to-edit-the-sitecolumnprojecttemplatevstemplate-file"></a>Para editar o arquivo SiteColumnProjectTemplate. vstemplate

1. No projeto SiteColumnProjectTemplate, substitua o conteúdo do arquivo SiteColumnProjectTemplate. vstemplate por uma das seções a seguir de XML.

   - Se você estiver criando um modelo de projeto do Visual C#, use o XML a seguir.

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <VSTemplate Version="3.0.0" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" Type="Project">
     <TemplateData>
       <Name>Site Column</Name>
       <Description>Creates a new site column in SharePoint</Description>
       <FrameworkVersion>3.5</FrameworkVersion>
       <ProjectType>CSharp</ProjectType>
       <CreateNewFolder>true</CreateNewFolder>
       <CreateInPlace>true</CreateInPlace>
       <ProvideDefaultName>true</ProvideDefaultName>
       <DefaultName>SiteColumn</DefaultName>
       <LocationField>Enabled</LocationField>
       <EnableLocationBrowseButton>true</EnableLocationBrowseButton>
       <PromptForSaveOnCreation>true</PromptForSaveOnCreation>
       <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>
       <Icon>SiteColumnProjectTemplate.ico</Icon>
       <SortOrder>1000</SortOrder>
     </TemplateData>
     <TemplateContent>
       <Project TargetFileName="SharePointProject1.csproj" File="ProjectTemplate.csproj" ReplaceParameters="true">
         <ProjectItem ReplaceParameters="true" TargetFileName="Properties\AssemblyInfo.cs">AssemblyInfo.cs</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Features\Feature1\Feature1.feature">Feature1.feature</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Features\Feature1\Feature1.Template.xml">Feature1.template.xml</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Package\Package.package">Package.package</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Package\Package.Template.xml">Package.Template.xml</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Field1\SharePointProjectItem.spdata">SharePointProjectItem.spdata</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Field1\Elements.xml" OpenInEditor="true">Elements.xml</ProjectItem>
         <ProjectItem ReplaceParameters="false" TargetFileName="key.snk">key.snk</ProjectItem>
       </Project>
     </TemplateContent>
   </VSTemplate>
   ```

   - Se você estiver criando um modelo de projeto Visual Basic, use o XML a seguir.

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <VSTemplate Version="3.0.0" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" Type="Project">
     <TemplateData>
       <Name>Site Column</Name>
       <Description>Creates a new site column in SharePoint</Description>
       <FrameworkVersion>3.5</FrameworkVersion>
       <ProjectType>VisualBasic</ProjectType>
       <CreateNewFolder>true</CreateNewFolder>
       <CreateInPlace>true</CreateInPlace>
       <ProvideDefaultName>true</ProvideDefaultName>
       <DefaultName>SiteColumn</DefaultName>
       <LocationField>Enabled</LocationField>
       <EnableLocationBrowseButton>true</EnableLocationBrowseButton>
       <PromptForSaveOnCreation>true</PromptForSaveOnCreation>
       <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>
       <Icon>SiteColumnProjectTemplate.ico</Icon>
       <SortOrder>1000</SortOrder>
     </TemplateData>
     <TemplateContent>
       <Project TargetFileName="SharePointProject1.vbproj" File="ProjectTemplate.vbproj" ReplaceParameters="true">
         <ProjectItem ReplaceParameters="true" TargetFileName="My Project\AssemblyInfo.vb">AssemblyInfo.vb</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Features\Feature1\Feature1.feature">Feature1.feature</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Features\Feature1\Feature1.Template.xml">Feature1.template.xml</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Package\Package.package">Package.package</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Package\Package.Template.xml">Package.Template.xml</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Field1\SharePointProjectItem.spdata">SharePointProjectItem.spdata</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Field1\Elements.xml" OpenInEditor="true">Elements.xml</ProjectItem>
         <ProjectItem ReplaceParameters="false" TargetFileName="key.snk">key.snk</ProjectItem>
       </Project>
     </TemplateContent>
   </VSTemplate>
   ```

    O novo XML faz as seguintes alterações no arquivo:

   - Define o `Name` elemento para a **coluna de site**de valor. (Esse nome aparece na caixa de diálogo **novo projeto** ).

   - Adiciona `ProjectItem` elementos para cada fileproject incluído em cada instância do projeto.

   - Usa o namespace `http://schemas.microsoft.com/developer/vstemplate/2005` . Outros arquivos de projeto nesta solução usam o `http://schemas.microsoft.com/developer/msbuild/2003` namespace. Portanto, as mensagens de aviso do esquema XML serão geradas, mas você poderá desconsiderar-as neste passo a passos.

     Para obter mais informações sobre o conteúdo de arquivos *. vstemplate* , consulte [referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md).

2. Salve e feche o arquivo.

#### <a name="to-edit-the-projecttemplatecsproj-or-projecttemplatevbproj-file"></a>Para editar o arquivo ProjectTemplate. csproj ou ProjectTemplate. vbproj

1. No projeto SiteColumnProjectTemplate, substitua o conteúdo do arquivo *ProjectTemplate. csproj* ou *ProjectTemplate. vbproj* por uma das seções a seguir do XML.

    - Se você estiver criando um modelo de projeto do Visual C#, use o XML a seguir.

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <Project ToolsVersion="4.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
      <PropertyGroup>
        <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
        <Platform Condition=" '$(Platform)' == '' ">AnyCPU</Platform>
        <SchemaVersion>2.0</SchemaVersion>
        <ProjectGuid>{$guid1$}</ProjectGuid>
        <OutputType>Library</OutputType>
        <AppDesignerFolder>Properties</AppDesignerFolder>
        <RootNamespace>$safeprojectname$</RootNamespace>
        <AssemblyName>$safeprojectname$</AssemblyName>
        <TargetFrameworkVersion>v3.5</TargetFrameworkVersion>
        <FileAlignment>512</FileAlignment>
        <ProjectTypeGuids>{BB1F664B-9266-4fd6-B973-E1E44974B511};{14822709-B5A1-4724-98CA-57A101D1B079};{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}</ProjectTypeGuids>
      </PropertyGroup>
      <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
        <DebugSymbols>true</DebugSymbols>
        <DebugType>full</DebugType>
        <Optimize>false</Optimize>
        <OutputPath>bin\Debug\</OutputPath>
        <DefineConstants>DEBUG;TRACE</DefineConstants>
        <ErrorReport>prompt</ErrorReport>
        <WarningLevel>4</WarningLevel>
        <UseVSHostingProcess>false</UseVSHostingProcess>
      </PropertyGroup>
      <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|AnyCPU' ">
        <DebugType>pdbonly</DebugType>
        <Optimize>true</Optimize>
        <OutputPath>bin\Release\</OutputPath>
        <DefineConstants>TRACE</DefineConstants>
        <ErrorReport>prompt</ErrorReport>
        <WarningLevel>4</WarningLevel>
      </PropertyGroup>
      <PropertyGroup>
        <SignAssembly>true</SignAssembly>
        <AssemblyOriginatorKeyFile>key.snk</AssemblyOriginatorKeyFile>
      </PropertyGroup>
      <ItemGroup>
        <Reference Include="System" />
        <Reference Include="System.Core" />
        <Reference Include="System.Data" />
        <Reference Include="System.Data.DataSetExtensions" />
        <Reference Include="System.Web" />
        <Reference Include="System.Xml" />
        <Reference Include="System.Xml.Linq" />
        <Reference Include="Microsoft.SharePoint" />
        <Reference Include="Microsoft.SharePoint.Security" />
      </ItemGroup>
      <ItemGroup>
        <Compile Include="Properties\AssemblyInfo.cs" />
      </ItemGroup>
      <ItemGroup>
        <None Include="Field1\SharePointProjectItem.spdata">
          <SharePointProjectItemId>{$guid2$}</SharePointProjectItemId>
        </None>
        <None Include="Field1\Elements.xml" />
      </ItemGroup>
      <ItemGroup>
        <None Include="key.snk" />
        <None Include="Package\Package.package">
          <PackageId>{$guid3$}</PackageId>
        </None>
        <None Include="Package\Package.Template.xml">
          <DependentUpon>Package.package</DependentUpon>
        </None>
        <None Include="Features\Feature1\Feature1.feature">
          <FeatureId>{$guid4$}</FeatureId>
        </None>
        <None Include="Features\Feature1\Feature1.Template.xml">
          <DependentUpon>Feature1.feature</DependentUpon>
        </None>
      </ItemGroup>
      <Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />
      <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v10.0\SharePointTools\Microsoft.VisualStudio.SharePoint.targets" />
    </Project>
    ```

    1. Se você estiver criando um modelo de projeto Visual Basic, use o XML a seguir.

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <Project ToolsVersion="4.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
      <PropertyGroup>
        <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
        <Platform Condition=" '$(Platform)' == '' ">AnyCPU</Platform>
        <ProductVersion>
        </ProductVersion>
        <SchemaVersion>
        </SchemaVersion>
        <ProjectGuid>{$guid1$}</ProjectGuid>
        <OutputType>Library</OutputType>
        <RootNamespace>$safeprojectname$</RootNamespace>
        <AssemblyName>$safeprojectname$</AssemblyName>
        <TargetFrameworkVersion>v3.5</TargetFrameworkVersion>
        <FileAlignment>512</FileAlignment>
        <ProjectTypeGuids>{BB1F664B-9266-4fd6-B973-E1E44974B511};{D59BE175-2ED0-4C54-BE3D-CDAA9F3214C8};{F184B08F-C81C-45F6-A57F-5ABD9991F28F}</ProjectTypeGuids>
        <OptionExplicit>On</OptionExplicit>
        <OptionCompare>Binary</OptionCompare>
        <OptionStrict>Off</OptionStrict>
        <OptionInfer>On</OptionInfer>
      </PropertyGroup>
      <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
        <DebugSymbols>true</DebugSymbols>
        <DebugType>full</DebugType>
        <DefineDebug>true</DefineDebug>
        <DefineTrace>true</DefineTrace>
        <OutputPath>bin\Debug\</OutputPath>
        <WarningLevel>4</WarningLevel>
        <UseVSHostingProcess>false</UseVSHostingProcess>
      </PropertyGroup>
      <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|AnyCPU' ">
        <DebugType>pdbonly</DebugType>
        <DefineDebug>false</DefineDebug>
        <DefineTrace>true</DefineTrace>
        <Optimize>true</Optimize>
        <OutputPath>bin\Release\</OutputPath>
        <UseVSHostingProcess>false</UseVSHostingProcess>
      </PropertyGroup>
      <PropertyGroup>
        <SignAssembly>true</SignAssembly>
        <AssemblyOriginatorKeyFile>key.snk</AssemblyOriginatorKeyFile>
      </PropertyGroup>
      <ItemGroup>
        <Reference Include="System" />
        <Reference Include="System.Core" />
        <Reference Include="System.Data" />
        <Reference Include="System.Data.DataSetExtensions" />
        <Reference Include="System.Xml" />
        <Reference Include="System.Xml.Linq" />
        <Reference Include="Microsoft.SharePoint" />
        <Reference Include="Microsoft.SharePoint.Security" />
      </ItemGroup>
      <ItemGroup>
        <Import Include="Microsoft.VisualBasic" />
        <Import Include="System" />
        <Import Include="System.Collections" />
        <Import Include="System.Collections.Generic" />
        <Import Include="System.Data" />
        <Import Include="System.Diagnostics" />
        <Import Include="System.Linq" />
        <Import Include="System.Xml.Linq" />
        <Import Include="Microsoft.SharePoint" />
        <Import Include="Microsoft.SharePoint.Security" />
      </ItemGroup>
      <ItemGroup>
        <Compile Include="My Project\AssemblyInfo.vb" />
      </ItemGroup>
      <ItemGroup>
        <AppDesigner Include="My Project\" />
      </ItemGroup>
      <ItemGroup>
        <None Include="Features\Feature1\Feature1.feature">
          <FeatureId>{$guid4$}</FeatureId>
        </None>
        <None Include="Field1\SharePointProjectItem.spdata">
          <SharePointProjectItemId>{$guid2$}</SharePointProjectItemId>
        </None>
        <None Include="key.snk" />
        <None Include="Package\Package.package">
          <PackageId>{$guid3$}</PackageId>
        </None>
        <None Include="Package\Package.Template.xml">
          <DependentUpon>Package.package</DependentUpon>
        </None>
      </ItemGroup>
      <ItemGroup>
        <None Include="Features\Feature1\Feature1.Template.xml">
          <DependentUpon>Feature1.feature</DependentUpon>
        </None>
        <None Include="Field1\Elements.xml" />
      </ItemGroup>
      <Import Project="$(MSBuildToolsPath)\Microsoft.VisualBasic.targets" />
      <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v10.0\SharePointTools\Microsoft.VisualStudio.SharePoint.targets" />
    </Project>
    ```

     O novo XML faz as seguintes alterações no arquivo:

    - Usa o `TargetFrameworkVersion` elemento para especificar o .NET Framework 3,5, não 4,5.

    - Adiciona `SignAssembly` `AssemblyOriginatorKeyFile` elementos e para assinar a saída do projeto.

    - Adiciona `Reference` elementos para referências de assembly que os projetos do SharePoint usam.

    - Adiciona elementos para cada arquivo padrão no projeto, como *Elements.xml* e *SharePointProjectItem. COMDATA*.

2. Salve e feche o arquivo.

## <a name="create-a-vsix-package-to-deploy-the-project-template"></a>Criar um pacote VSIX para implantar o modelo de projeto
 Para implantar a extensão, use o projeto VSIX na solução **SiteColumnProjectItem** para criar um pacote VSIX. Primeiro, configure o pacote VSIX modificando o arquivo. Extension. vsixmanifest de origem que está incluído no projeto VSIX. Em seguida, crie o pacote VSIX criando a solução.

#### <a name="to-configure-and-create-the-vsix-package"></a>Para configurar e criar o pacote VSIX

1. No **Gerenciador de soluções**, no projeto **SiteColumnProjectItem** , abra o arquivo Source. Extension. vsixmanifest no editor de manifesto.

     O arquivo Source. Extension. vsixmanifest é a base para o arquivo extension. vsixmanifest que todos os pacotes VSIX exigem. Para obter mais informações sobre esse arquivo, consulte [referência do esquema de extensão do VSIX 1,0](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b).

2. Na caixa **nome do produto** , insira a **coluna site**.

3. Na caixa **autor** , digite **contoso**.

4. Na caixa **Descrição** , insira **um projeto do SharePoint para criar colunas de site**.

5. Escolha a guia **ativos** e, em seguida, escolha o botão **novo** .

     A caixa de diálogo **Adicionar novo ativo** é aberta.

6. Na lista **tipo** , escolha **Microsoft. VisualStudio. ProjectTemplate**.

    > [!NOTE]
    > Esse valor corresponde ao `ProjectTemplate` elemento no arquivo extension. vsixmanifest. Esse elemento identifica a subpasta no pacote VSIX que contém o modelo de projeto. Para obter mais informações, consulte [elemento ProjectTemplate (esquema VSX)](/previous-versions/visualstudio/visual-studio-2010/dd393735\(v\=vs.100\)).

7. Na lista **origem** , escolha **um projeto na solução atual**.

8. Na lista **projeto** , escolha **SiteColumnProjectTemplate**e, em seguida, escolha o botão **OK** .

9. Escolha o botão **novo** novamente.

     A caixa de diálogo **Adicionar novo ativo** é aberta.

10. Na lista **tipo** , escolha **Microsoft. VisualStudio. MefComponent**.

    > [!NOTE]
    > Esse valor corresponde ao `MefComponent` elemento no arquivo extension. vsixmanifest. Esse elemento Especifica o nome de um assembly de extensão no pacote VSIX. Para obter mais informações, consulte [elemento MEFComponent (esquema VSX)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\)).

11. Na lista **origem** , escolha **um projeto na solução atual**.

12. Na lista **projeto** , escolha **projectItemTypeDefinition**e, em seguida, escolha o botão **OK** .

13. Na barra de menus, escolha **criar**  >  **solução de compilação**e, em seguida, certifique-se de que o projeto seja compilado sem erros.

## <a name="test-the-project-template"></a>Testar o modelo do projeto
 Agora você está pronto para testar o modelo de projeto. Primeiro, inicie a depuração da solução SiteColumnProjectItem na instância experimental do Visual Studio. Em seguida, teste o projeto de **coluna do site** na instância experimental do Visual Studio. Por fim, compile e execute o projeto do SharePoint para verificar se a coluna site funciona conforme o esperado.

#### <a name="to-start-debugging-the-solution"></a>Para iniciar a depuração da solução

1. Reinicie o Visual Studio com credenciais administrativas e, em seguida, abra a solução SiteColumnProjectItem.

2. No arquivo de código SiteColumnProjectItemTypeProvider, adicione um ponto de interrupção à primeira linha de código no `InitializeType` método e escolha a tecla **F5** para iniciar a depuração.

     O Visual Studio instala a extensão para%UserProfile%\AppData\Local\Microsoft\VisualStudio\10.0Exp\Extensions\Contoso\Site Column\1.0 e inicia uma instância experimental do Visual Studio. Você testará o item de projeto nesta instância do Visual Studio.

#### <a name="to-test-the-project-in-visual-studio"></a>Para testar o projeto no Visual Studio

1. Na instância experimental do Visual Studio, na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**.

2. Expanda o nó **Visual C#** ou **Visual Basic** (dependendo do idioma ao qual o modelo de projeto dá suporte), expanda o nó do **SharePoint** e escolha o nó **2010** .

3. Na lista de modelos de projeto, escolha o modelo de **coluna site** .

4. Na caixa **nome** , digite **SiteColumnTest** e, em seguida, escolha o botão **OK** .

     No **Gerenciador de soluções**, um novo projeto é exibido com um item de projeto chamado **Field1**.

5. Verifique se o código na outra instância do Visual Studio é interrompido no ponto de interrupção que você definiu anteriormente no `InitializeType` método e, em seguida, escolha a tecla **F5** para continuar a depurar o projeto.

6. Em **Gerenciador de soluções**, escolha o nó **campo1** e, em seguida, escolha a tecla **F4** .

     A janela **Propriedades** é aberta.

7. Na lista Propriedades, verifique se a **Propriedade exemplo** de propriedade é exibida.

#### <a name="to-test-the-site-column-in-sharepoint"></a>Para testar a coluna site no SharePoint

1. Em **Gerenciador de soluções**, escolha o nó **SiteColumnTest** .

2. Na janela **Propriedades** , na caixa de texto que está ao lado da propriedade **URL do site** , digite **http://localhost** .

     Esta etapa especifica o site do SharePoint local no computador de desenvolvimento que você deseja usar para a depuração.

    > [!NOTE]
    > A propriedade **URL do site** está vazia por padrão porque o modelo de projeto coluna do site não fornece um assistente para coletar esse valor quando o projeto é criado. Para saber como adicionar um assistente que solicita ao desenvolvedor esse valor e, em seguida, configura essa propriedade no novo projeto, consulte [passo a passos: criar um item de projeto de coluna de site com um modelo de projeto, parte 2](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md).

3. Pressione a tecla **F5**.

     A coluna site é empacotada e implantada no site do SharePoint que é especificado na propriedade **URL do site** do projeto. O navegador da Web é aberto na página padrão deste site.

    > [!NOTE]
    > Se a caixa de diálogo **depuração de script desabilitada** for exibida, escolha o botão **Sim** para continuar a depurar o projeto.

4. No menu **ações do site** , escolha **configurações do site**.

5. Na página **configurações do site** , na lista **galerias** , escolha o link **colunas do site** .

6. Na lista de colunas do site, verifique se um grupo de **colunas personalizadas** contém uma coluna denominada **SiteColumnTest**.

7. Feche o navegador da web.

## <a name="clean-up-the-development-computer"></a>Limpar o computador de desenvolvimento
 Depois de concluir o teste do projeto, remova o modelo de projeto da instância experimental do Visual Studio.

#### <a name="to-clean-up-the-development-computer"></a>Para limpar o computador de desenvolvimento

1. Na instância experimental do Visual Studio, na barra de menus, escolha **ferramentas**  >  **extensões e atualizações**.

     A caixa de diálogo **Extensões e Atualizações** é aberta.

2. Na lista de extensões, escolha a extensão de **coluna do site** e, em seguida, escolha o botão **desinstalar** .

3. Na caixa de diálogo exibida, escolha o botão **Sim** para confirmar que você deseja desinstalar a extensão.

4. Escolha o botão **fechar** para concluir a desinstalação.

5. Feche as duas instâncias do Visual Studio (a instância experimental e a instância do Visual Studio na qual a solução SiteColumnProjectItem está aberta).

## <a name="next-steps"></a>Próximas etapas
 Depois de concluir este passo a passos, você pode adicionar um assistente ao modelo de projeto. Quando um usuário cria um projeto de coluna de site, o assistente solicita ao usuário a URL do site a ser usada para depuração e se a nova solução está em área restrita e o assistente configura o novo projeto com essas informações. O assistente também coleta informações sobre a coluna (como o tipo base e o grupo no qual listar a coluna na Galeria de colunas do site) e adiciona essas informações ao arquivo de *Elements.xml* no novo projeto. Para obter mais informações, consulte [Walkthrough: criar um item de projeto de coluna de site com um modelo de projeto, parte 2](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md).

## <a name="see-also"></a>Consulte também

- [Walkthrough: criar um item de projeto de coluna de site com um modelo de projeto, parte 2](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)
- [Definir tipos de item de projeto personalizados do SharePoint](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [Criar modelos de item e modelos de projeto para itens de projeto do SharePoint](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [Salvar dados em extensões do sistema de projeto do SharePoint](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)
- [Associar dados personalizados a extensões de ferramentas do SharePoint](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)