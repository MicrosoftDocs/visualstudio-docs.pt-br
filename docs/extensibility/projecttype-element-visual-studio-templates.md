---
title: Elemento ProjectType (modelos do Visual Studio) | Microsoft Docs
description: Saiba mais sobre o elemento ProjectType e como ele categoriza o modelo de projeto para que ele apareça na caixa de diálogo novo projeto ou adicionar novo item.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectType
helpviewer_keywords:
- ProjectType element [Visual Studio project templates]
ms.assetid: ccf9d83f-c7f3-49c7-a31f-e1f22bec004c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d494d27b2a3302d0beff68b770d0172edb520f35
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068671"
---
# <a name="projecttype-element-visual-studio-templates"></a>Elemento ProjectType (modelos do Visual Studio)
Categoriza o modelo de projeto para que ele apareça sob o grupo especificado na caixa de diálogo **novo projeto** ou **Adicionar novo item** .

> [!WARNING]
> Modelos de projeto têm suporte para C++ a partir do Visual Studio 2012. Eles não têm suporte para C++ no Visual Studio 2010 e em versões anteriores.

 \<VSTemplate> \<TemplateData>
 \<ProjectType>

## <a name="syntax"></a>Sintaxe

```xml
<ProjectType> CSharp/VisualBasic/VC/Web </ProjectType>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos
 Nenhum.

### <a name="child-elements"></a>Elementos filho
 Nenhum.

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|Categoriza o modelo e define como ele é exibido no **novo projeto** ou na caixa de diálogo **Adicionar novo item** .|

## <a name="text-value"></a>Valor de texto
 Um valor de texto é obrigatório.

 Esse valor especifica o tipo de projeto que o modelo criará e deve conter um dos seguintes valores:

- `CSharp`: Especifica que o modelo cria um [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] projeto ou item.

- `VisualBasic`: Especifica que o modelo cria um [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] projeto ou item.

- `Web`: Especifica que o modelo cria um projeto da Web ou item. Se o `ProjectType` elemento contiver esse valor, o idioma do projeto ou do item será definido no [elemento ProjectSubType (modelos do Visual Studio)](../extensibility/projectsubtype-element-visual-studio-templates.md).

## <a name="remarks"></a>Comentários
 `ProjectType` é um elemento filho obrigatório de `TemplateData` .

 O valor do `ProjectType` elemento especifica onde o modelo está localizado na caixa de diálogo **novo projeto** ou **Adicionar novo item** . Por exemplo, um modelo com um `ProjectType` valor de `CSharp` é exibido sob o nó **Visual C#** na caixa de diálogo **novo projeto** .

 Um subtipo de modelo pode ser especificado usando o elemento [ProjectSubType](../extensibility/projectsubtype-element-visual-studio-templates.md) .

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
- [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Criar modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
- [Elemento ProjectSubType (modelos do Visual Studio)](../extensibility/projectsubtype-element-visual-studio-templates.md)
