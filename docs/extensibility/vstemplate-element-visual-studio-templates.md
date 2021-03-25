---
title: Elemento VSTemplate (modelos do Visual Studio) | Microsoft Docs
description: Saiba mais sobre o elemento VSTemplate e como ele contém todos os metadados sobre o modelo de projeto, o modelo de item ou o kit do iniciante.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#VSTemplate
helpviewer_keywords:
- VSTemplate element [Visual Studio project templates]
ms.assetid: f8ac561b-3b0b-4246-9ec9-118d2447e9a9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7509614613ac80bc4f697f7f93358819eb9ecde4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062207"
---
# <a name="vstemplate-element-visual-studio-templates"></a>Elemento VSTemplate (modelos do Visual Studio)
Contém todos os metadados sobre o modelo de projeto, modelo de item ou kit do iniciante.

## <a name="syntax"></a>Sintaxe

```csharp
<VSTemplate Type="TemplateType" Version="x.x.x">
    <TemplateData>    </TemplateData>
    <TemplateContent>    </TemplateContent>
    ...
</VSTemplate>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

| Atributo | Descrição |
|-----------| - |
| `Type` | Identifica o modelo como um modelo de projeto ou um modelo de item. Esse atributo pode ter um valor de `Project` ou `Item` . |
| `Version` | Especifica um número de versão para o modelo. Modelos no [!INCLUDE[vs_dev10_long](../code-quality/includes/vs_dev10_long_md.md)] e [!INCLUDE[vs_dev11_long](../data-tools/includes/vs_dev11_long_md.md)] têm um `Version` valor de atributo de `3.0.0` . |

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|Elemento necessário.<br /><br /> Especifica os dados que categorizam o modelo e define como ele é exibido na caixa de diálogo **novo projeto** ou **Adicionar novo item** .|
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|Elemento necessário.<br /><br /> Especifica o conteúdo do modelo.|
|[WizardExtension](../extensibility/wizardextension-element-visual-studio-templates.md)|Elemento opcional.|
|[WizardData](../extensibility/wizarddata-element-visual-studio-templates.md)|Elemento opcional.|

### <a name="parent-elements"></a>Elementos pai
 Nenhum.

## <a name="remarks"></a>Comentários
 O `VSTemplate` elemento é o elemento raiz de arquivos *. vstemplate* .

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra os metadados de um modelo de projeto para um [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] aplicativo.

```xml
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
            <ProjectItem>Form1.cs</ProjectItem>
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
- [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Criando modelos de projeto e item](../ide/creating-project-and-item-templates.md)
