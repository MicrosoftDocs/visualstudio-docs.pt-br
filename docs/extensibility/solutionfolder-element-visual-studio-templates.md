---
title: Elemento SolutionFolder (modelos do Visual Studio) | Microsoft Docs
description: Saiba mais sobre o elemento SolutionFolder e como ele agrupa projetos em modelos de vários projetos.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#SolutionFolder
helpviewer_keywords:
- <SolutionFolder> element [Visual Studio Templates]
- SolutionFolder element [Visual Studio Templates]
ms.assetid: 963f0398-fb50-4d8e-879d-d48f8b7c6d80
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f65607a5411270e7f21e6ec6cdac0c087824b32b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056331"
---
# <a name="solutionfolder-element-visual-studio-templates"></a>Elemento SolutionFolder (modelos do Visual Studio)
Agrupa projetos em modelos de vários projetos.

 \<VSTemplate> \<TemplateContent>
 \<ProjectCollection>
 \<SolutionFolder>

## <a name="syntax"></a>Sintaxe

```
<SolutionFolder Name="DirectoryName">
    ...
</SolutionFolder>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|`Name`|Atributo obrigatório.<br /><br /> O nome da pasta da solução.|

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|[ProjectTemplateLink](../extensibility/projecttemplatelink-element-visual-studio-templates.md)|Elemento opcional.<br /><br /> Especifica o caminho para o arquivo .vstemplate de um projeto em um modelo de vários projetos.|
|`SolutionFolder`|Elemento opcional.<br /><br /> Agrupa projetos em modelos de vários projetos.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[ProjectCollection](../extensibility/projectcollection-element-visual-studio-templates.md)|Especifica a organização e o conteúdo de modelos de vários projetos.|
|`SolutionFolder`|Agrupa projetos em modelos de vários projetos.|

## <a name="remarks"></a>Comentários
 Os modelos de vários projetos atuam como contêineres para dois ou mais projetos. O `SolutionFolder` elemento é usado para organizar os projetos no modelo em grupos. As pastas especificadas por `SolutionFolder` elementos são criadas como pastas de solução no projeto no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] . Para obter mais informações sobre modelos de vários projetos, consulte [como: criar modelos de vários projetos](../ide/how-to-create-multi-project-templates.md).

## <a name="example"></a>Exemplo
 Este exemplo usa o `SolutionFolder` elemento para dividir o modelo de vários projetos em dois grupos `Math Classes` e `Graphics Classes` . O modelo contém quatro projetos, dois dos quais são colocados em cada pasta de solução.

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
            <SolutionFolder Name="Math Classes">
                <ProjectTemplateLink ProjectName="MathClassLib1">
                    MathClassLib1\MyTemplate.vstemplate
                </ProjectTemplateLink>
                <ProjectTemplateLink ProjectName="MathClassLib2">
                    MathClassLib2\MyTemplate.vstemplate
                </ProjectTemplateLink>
            </SolutionFolder>
            <SolutionFolder Name="Graphics Classes">
                <ProjectTemplateLink ProjectName="GraphicsClassLib1">
                    GraphicsClassLib1\MyTemplate.vstemplate
                </ProjectTemplateLink>
                <ProjectTemplateLink ProjectName="GraphicsClassLib2">
                    GraphicsClassLib2\MyTemplate.vstemplate
                </ProjectTemplateLink>
            </SolutionFolder>
        </ProjectCollection>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>Confira também
- [Referência de esquema do modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
- [Como criar modelos multiprojeto](../ide/how-to-create-multi-project-templates.md)
