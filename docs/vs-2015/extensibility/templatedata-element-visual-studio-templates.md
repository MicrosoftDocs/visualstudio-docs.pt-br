---
title: Elemento TemplateData (modelos do Visual Studio) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#TemplateData
helpviewer_keywords:
- TemplateData element [Visual Studio project templates]
ms.assetid: db17ec9b-bfdf-46b1-bbe7-5ccc140056e2
caps.latest.revision: 25
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 29b481c8560e47dff4c4fadca9dab869e4f5b361
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51743777"
---
# <a name="templatedata-element-visual-studio-templates"></a>Elemento TemplateData (modelos do Visual Studio)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Categoriza o modelo e define como ele é exibido em qualquer um de **novo projeto** ou o **Adicionar Novo Item** caixa de diálogo.  
  
 \<VSTemplate >  
 \<TemplateData >  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<TemplateData>  
    <Name> ... </Name>  
    <Description> ... </Description>  
    <Icon> ... </Icon>  
    <ProjectType> ... </ProjectType>  
    ...  
</TemplateData>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
 nenhuma.  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[Nome](../extensibility/name-element-visual-studio-templates.md)|Elemento obrigatório.<br /><br /> Especifica o nome do modelo como ele aparece em qualquer um de **novo projeto** ou o **Adicionar Novo Item** caixa de diálogo.|  
|[Descrição](../extensibility/description-element-visual-studio-templates.md)|Elemento obrigatório.<br /><br /> Especifica a descrição do modelo como ele aparece em qualquer um de **novo projeto** ou o **Adicionar Novo Item** caixa de diálogo.|  
|[Ícone](../extensibility/icon-element-visual-studio-templates.md)|Elemento obrigatório.<br /><br /> Especifica o caminho e o nome do arquivo do arquivo de imagem que serve como o ícone, o que é exibido em qualquer um de **novo projeto** ou o **Adicionar Novo Item** caixa de diálogo, para o modelo.|  
|[ProjectType](../extensibility/projecttype-element-visual-studio-templates.md)|Elemento obrigatório.<br /><br /> Categoriza o modelo de projeto para que ele apareça sob o grupo especificado na **novo projeto** caixa de diálogo.|  
|[ProjectSubType](../extensibility/projectsubtype-element-visual-studio-templates.md)|Elemento opcional.<br /><br /> Classifica o modelo de projeto para que ele apareça sob o nó da subcategoria especificado na **novo projeto** caixa de diálogo.|  
|[TemplateID](../extensibility/templateid-element-visual-studio-templates.md)|Elemento opcional.<br /><br /> Especifica a ID do modelo.|  
|[TemplateGroupID](../extensibility/templategroupid-element-visual-studio-templates.md)|Elemento opcional.<br /><br /> Especifica a ID do grupo de modelo.|  
|[Ordem de classificação](../extensibility/sortorder-element-visual-studio-templates.md)|Elemento opcional.<br /><br /> Especifica um valor que é usado para organizar o modelo, entre outros modelos na mesma categoria, como ele aparece em ambos os **novo projeto** ou **Adicionar Novo Item** caixa de diálogo.|  
|[CreateNewFolder](../extensibility/createnewfolder-element-visual-studio-templates.md)|Elemento opcional.<br /><br /> Especifica se uma pasta que contém é criada na instanciação do projeto.|  
|[DefaultName](../extensibility/defaultname-element-visual-studio-templates.md)|Elemento opcional.<br /><br /> Especifica o nome que o sistema de projeto do Visual Studio gerará para o projeto ou item quando ele é criado.|  
|[ProvideDefaultName](../extensibility/providedefaultname-element-visual-studio-templates.md)|Elemento opcional.<br /><br /> Especifica se o sistema de projeto do Visual Studio gerará o nome padrão para um projeto ou item quando ele é criado.|  
|[PromptForSaveOnCreation](../extensibility/promptforsaveoncreation-element-visual-studio-templates.md)|Elemento opcional.<br /><br /> Especifica se o projeto pode ser criado como um projeto temporário.|  
|[EnableLocationBrowseButton](../extensibility/enablelocationbrowsebutton-element-visual-studio-templates.md)|Elemento opcional.<br /><br /> Especifica se o **navegue** botão está disponível na **novo projeto** caixa de diálogo, para que os usuários podem facilmente modificar o diretório padrão em que um novo projeto é salvo.|  
|[Oculto](../extensibility/hidden-element-visual-studio-templates.md)|Elemento opcional.<br /><br /> Especifica se o modelo é exibido em qualquer um de **novo projeto** ou **Adicionar Novo Item** caixa de diálogo.|  
|[NumberOfParentCategoriesToRollUp](../extensibility/numberofparentcategoriestorollup-visual-studio-templates.md)|Elemento opcional.<br /><br /> Especifica o número de categorias pai que exibirá o modelo na **novo projeto** caixa de diálogo.|  
|[LocationFieldMRUPrefix](../extensibility/locationfieldmruprefix-element-visual-studio-templates.md)|Elemento opcional.|  
|[LocationField](../extensibility/locationfield-element-visual-studio-project-templates.md)|Elemento opcional.<br /><br /> Especifica se ou não a **local** caixa de texto a **novo projeto** caixa de diálogo é habilitada, desabilitada ou ocultada para o modelo de projeto.|  
|[RequiredFrameworkVersion](../extensibility/requiredframeworkversion-element-visual-studio-templates.md)|Elemento opcional.<br /><br /> Use esse elemento se o modelo só dá suporte a uma versão específica de mínimo e versões posteriores, se houver, do .NET Framework.|  
|[SupportsMasterPage](../extensibility/supportsmasterpage-element-visual-studio-templates.md)|Elemento opcional.<br /><br /> Especifica se o modelo dá suporte a uma página mestra para projetos web.|  
|[SupportsCodeSeparation](../extensibility/supportscodeseparation-element-visual-studio-templates.md)|Elemento opcional.<br /><br /> Especifica se o modelo dá suporte à separação de código ou o modelo de página code-behind, para projetos web.|  
|[SupportsLanguageDropDown](../extensibility/supportslanguagedropdown-element-visual-studio-templates.md)|Elemento opcional.<br /><br /> Especifica se o modelo é idêntico para vários idiomas e se o **linguagem** opção está disponível na **novo projeto** caixa de diálogo.|  
|[TargetPlatformName](../extensibility/targetplatformname-element-visual-studio-templates.md)|Elemento opcional.<br /><br /> Especifica a plataforma de que os destinos de modelo de projeto. Esse elemento Especifica que um modelo de projeto é usado para criar [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] aplicativos.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[VSTemplate](../extensibility/vstemplate-element-visual-studio-templates.md)|Elemento obrigatório.<br /><br /> Contém todos os metadados para o modelo de projeto, o modelo de item ou o starter kit para.|  
  
## <a name="remarks"></a>Comentários  
 `TemplateData` é um elemento obrigatório.  
  
 Se você não incluir um elemento opcional, o valor padrão para esse elemento é usado.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra os metadados para um modelo de projeto para um [!INCLUDE[csprcs](../includes/csprcs-md.md)] aplicativo.  
  
```  
<VSTemplate Type="Project" Version="3.0.0"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>My template</Name>  
        <Description>A basic starter kit</Description>  
        <Icon>TemplateIcon.ico</Icon>  
        <ProjectType>CSharp</ProjectType>  
    </TemplateData>  
    <TemplateContent>  
        <Project File="MyStarterKit.csproj">  
            <ProjectItem>Form1.cs<ProjectItem>  
            <ProjectItem>Form1.Designer.cs</ProjectItem>  
            <ProjectItem>Program.cs</ProjectItem>  
            <ProjectItem>Properties\AssemblyInfo.cs</ProjectItem>  
            <ProjectItem>Properties\Resources.resx</ProjectItem>  
            <ProjectItem>Properties\Resources.Designer.cs</ProjectItem>  
            <ProjectItem>Properties\Settings.settings</ProjectItem>  
            <ProjectItem>Properties\Settings.Designer.cs</ProjectItem>  
        </Project>  
    </TemplateContent>  
</VSTemplate>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)   
 [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)

