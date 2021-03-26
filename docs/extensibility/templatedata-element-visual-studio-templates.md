---
title: Elemento TemplateData (modelos do Visual Studio) | Microsoft Docs
description: Saiba mais sobre o elemento TemplateData e como ele categoriza o modelo e define como ele é exibido no novo projeto ou na caixa de diálogo Adicionar novo item.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#TemplateData
helpviewer_keywords:
- TemplateData element [Visual Studio project templates]
ms.assetid: db17ec9b-bfdf-46b1-bbe7-5ccc140056e2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b5bc7f9b94553bda2bd2fcf020264ddb0d850c32
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085566"
---
# <a name="templatedata-element-visual-studio-templates"></a>Elemento TemplateData (modelos do Visual Studio)
Categoriza o modelo e define como ele é exibido no **novo projeto** ou na caixa de diálogo **Adicionar novo item** .

 \<VSTemplate> \<TemplateData>

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
 Nenhum.

### <a name="child-elements"></a>Elementos filho

| Elemento | Descrição |
| - | - |
| [Nome](../extensibility/name-element-visual-studio-templates.md) | Elemento necessário.<br /><br /> Especifica o nome do modelo como ele aparece no **novo projeto** ou na caixa de diálogo **Adicionar novo item** . |
| [Descrição](../extensibility/description-element-visual-studio-templates.md) | Elemento necessário.<br /><br /> Especifica a descrição do modelo como ele aparece no **novo projeto** ou na caixa de diálogo **Adicionar novo item** . |
| [Ícone](../extensibility/icon-element-visual-studio-templates.md) | Elemento necessário.<br /><br /> Especifica o caminho e o nome do arquivo de imagem que serve como o ícone, que aparece na caixa de diálogo **novo projeto** ou **Adicionar novo item** , para o modelo. |
| [ProjectType](../extensibility/projecttype-element-visual-studio-templates.md) | Elemento necessário.<br /><br /> Categoriza o modelo de projeto para que ele apareça sob o grupo especificado na caixa de diálogo **novo projeto** . |
| [ProjectSubType](../extensibility/projectsubtype-element-visual-studio-templates.md) | Elemento opcional.<br /><br /> Classifica o modelo de projeto para que ele apareça sob a subcategoria especificada na caixa de diálogo **novo projeto** . |
| [TemplateID](../extensibility/templateid-element-visual-studio-templates.md) | Elemento opcional.<br /><br /> Especifica a ID do modelo. |
| [TemplateGroupID](../extensibility/templategroupid-element-visual-studio-templates.md) | Elemento opcional.<br /><br /> Especifica a ID do grupo de modelos. |
| [SortOrder](../extensibility/sortorder-element-visual-studio-templates.md) | Elemento opcional.<br /><br /> Especifica um valor que é usado para organizar o modelo, entre outros modelos na mesma categoria, como aparece na caixa de diálogo **novo projeto** ou **Adicionar novo item** . |
| [CreateNewFolder](../extensibility/createnewfolder-element-visual-studio-templates.md) | Elemento opcional.<br /><br /> Especifica se uma pasta recipiente é criada na instanciação do projeto. |
| [DefaultName](../extensibility/defaultname-element-visual-studio-templates.md) | Elemento opcional.<br /><br /> Especifica o nome que o sistema de projeto do Visual Studio gerará para o projeto ou item quando ele for criado. |
| [ProvideDefaultName](../extensibility/providedefaultname-element-visual-studio-templates.md) | Elemento opcional.<br /><br /> Especifica se o sistema de projeto do Visual Studio irá gerar o nome padrão para um projeto ou item quando ele for criado. |
| [PromptForSaveOnCreation](../extensibility/promptforsaveoncreation-element-visual-studio-templates.md) | Elemento opcional.<br /><br /> Especifica se o projeto pode ser criado como um projeto temporário (somente Visual Studio 2017). |
| [EnableLocationBrowseButton](../extensibility/enablelocationbrowsebutton-element-visual-studio-templates.md) | Elemento opcional.<br /><br /> Especifica se o botão **procurar** está disponível na caixa de diálogo **novo projeto** , para que os usuários possam modificar facilmente o diretório padrão em que um novo projeto é salvo. |
| [Oculto](../extensibility/hidden-element-visual-studio-templates.md) | Elemento opcional.<br /><br /> Especifica se o modelo aparece na caixa de diálogo **novo projeto** ou **Adicionar novo item** . |
| [NumberOfParentCategoriesToRollUp](../extensibility/numberofparentcategoriestorollup-visual-studio-templates.md) | Elemento opcional.<br /><br /> Especifica o número de categorias pai que exibirá o modelo na caixa de diálogo **novo projeto** . |
| [LocationFieldMRUPrefix](../extensibility/locationfieldmruprefix-element-visual-studio-templates.md) | Elemento opcional. |
| [LocationField](../extensibility/locationfield-element-visual-studio-project-templates.md) | Elemento opcional.<br /><br /> Especifica se a caixa de texto **local** na caixa de diálogo **novo projeto** está habilitada, desabilitada ou oculta para o modelo de projeto. |
| [RequiredFrameworkVersion](../extensibility/requiredframeworkversion-element-visual-studio-templates.md) | Elemento opcional.<br /><br /> Use este elemento se o modelo der suporte apenas a uma versão mínima específica e versões posteriores, se houver, do .NET Framework. |
| [SupportsMasterPage](../extensibility/supportsmasterpage-element-visual-studio-templates.md) | Elemento opcional.<br /><br /> Especifica se o modelo oferece suporte a uma página mestra para projetos Web. |
| [SupportsCodeSeparation](../extensibility/supportscodeseparation-element-visual-studio-templates.md) | Elemento opcional.<br /><br /> Especifica se o modelo oferece suporte à separação de código ou ao modelo de página code-behind, para projetos Web. |
| [SupportsLanguageDropDown](../extensibility/supportslanguagedropdown-element-visual-studio-templates.md) | Elemento opcional.<br /><br /> Especifica se o modelo é idêntico a vários idiomas e se a opção de **idioma** está disponível na caixa de diálogo **novo projeto** . |
| [TargetPlatformName](../extensibility/targetplatformname-element-visual-studio-templates.md) | Elemento opcional.<br /><br /> Especifica a plataforma de destino do modelo de projeto. Esse elemento Especifica que um modelo de projeto é usado para criar [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] aplicativos. |

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[VSTemplate](../extensibility/vstemplate-element-visual-studio-templates.md)|Elemento necessário.<br /><br /> Contém todos os metadados do modelo de projeto, modelo de item ou kit do iniciante.|

## <a name="remarks"></a>Comentários
 `TemplateData` é um elemento obrigatório.

 Se você não incluir um elemento opcional, o valor padrão desse elemento será usado.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra os metadados de um modelo de projeto para um [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] aplicativo.

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

## <a name="see-also"></a>Confira também
- [Referência de esquema do modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
