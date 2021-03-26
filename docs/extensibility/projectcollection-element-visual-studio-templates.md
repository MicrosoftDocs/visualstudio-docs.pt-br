---
title: Elemento ProjectCollection (modelos do Visual Studio) | Microsoft Docs
description: Saiba mais sobre o elemento ProjectCollection e como ele especifica a organização e o conteúdo de modelos de vários projetos.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectCollection
helpviewer_keywords:
- <ProjectCollection> element [Visual Studio Templates]
- ProjectCollection element [Visual Studio Templates]
ms.assetid: deb27180-2035-49ed-b835-c47bb3cd2f8f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e835843094b9495b8907a3ada727435b8806c78d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068759"
---
# <a name="projectcollection-element-visual-studio-templates"></a>Elemento ProjectCollection (modelos do Visual Studio)
Especifica a organização e o conteúdo de modelos de vários projetos.

 \<VSTemplate> \<TemplateContent>
 \<ProjectCollection>

## <a name="syntax"></a>Sintaxe

```xml
<ProjectCollection>
    <ProjectTemplateLink> ... </ProjectTemplateLink>
    <SolutionFolder> ... </SolutionFolder>
</ProjectCollection>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos
 Nenhum.

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|[ProjectTemplateLink](../extensibility/projecttemplatelink-element-visual-studio-templates.md)|Elemento opcional.<br /><br /> Especifica um projeto em um modelo de vários projetos.|
|[SolutionFolder](../extensibility/solutionfolder-element-visual-studio-templates.md)|Elemento opcional.<br /><br /> Agrupa projetos em modelos de vários projetos.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|Elemento necessário.<br /><br /> Especifica o conteúdo do modelo.|

## <a name="remarks"></a>Comentários
 Os modelos de vários projetos atuam como contêineres para dois ou mais projetos. O `ProjectCollection` elemento é usado para especificar os projetos a serem contidos no modelo. Para obter mais informações sobre modelos de vários projetos, consulte [como: criar modelos de vários projetos](../ide/how-to-create-multi-project-templates.md).

## <a name="example"></a>Exemplo
 Este exemplo mostra um arquivo de raiz *. vstemplate* de vários projetos simples. Neste exemplo, o modelo contém dois projetos, `My Windows Application` e `My Class Library`. O atributo `ProjectName` no elemento `ProjectTemplateLink` define o nome do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para atribuir este projeto. Se o `ProjectName` atributo não existir, o nome do arquivo *. vstemplate* será usado como o nome do projeto.

```
<VSTemplate Version="3.0.0" Type="ProjectGroup"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>Multi-Project Template Sample</Name>
        <Description>An example of a multi-project template</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>VisualBasic</ProjectType>
    </TemplateData>
    <TemplateContent>
        <ProjectCollection>
            <ProjectTemplateLink ProjectName="My Windows Application">
                WindowsApp\MyTemplate.vstemplate
            </ProjectTemplateLink>
            <ProjectTemplateLink ProjectName="My Class Library">
                ClassLib\MyTemplate.vstemplate
            </ProjectTemplateLink>
        </ProjectCollection>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>Confira também
- [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Criar modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
- [Como: criar modelos de vários projetos](../ide/how-to-create-multi-project-templates.md)
