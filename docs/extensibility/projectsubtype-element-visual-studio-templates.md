---
title: Elemento ProjectSubType (modelos do Visual Studio) | Microsoft Docs
description: Saiba mais sobre o elemento ProjectSubType e como ele classifica o modelo em uma subcategoria do valor especificado no elemento ProjectType.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectSubType
helpviewer_keywords:
- ProjectSubType element [Visual Studio Templates]
- <ProjectSubType> element [Visual Studio Templates]
ms.assetid: f6895cd4-3e95-4f0e-aa9e-8c7750f46ed4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 02dd5573de12e4626c267fa014f6c7fc8f243b72
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068668"
---
# <a name="projectsubtype-element-visual-studio-templates"></a>Elemento ProjectSubType (modelos do Visual Studio)
Classifica o modelo em uma subcategoria do valor especificado no `ProjectType` elemento.

 \<VSTemplate> \<TemplateData>
 \<ProjectSubType>

## <a name="syntax"></a>Sintaxe

```xml
<ProjectSubType> SubType </ProjectSubType>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|Elemento necessário.<br /><br /> Categoriza o modelo e define como ele é exibido no **novo projeto** ou na caixa de diálogo **Adicionar novo item** .|

## <a name="text-value"></a>Valor de texto
 Um valor de texto é obrigatório.

 Esse valor especifica a subcategoria do modelo.

## <a name="remarks"></a>Comentários
 `ProjectSubType` é um elemento filho opcional de `TemplateData` .

 O `ProjectSubType` elemento fornece uma subcategoria ao elemento [ProjectType](../extensibility/projecttype-element-visual-studio-templates.md) . Esse valor pode incluir:

- `SmartDevice-NETCFv1`: Especifica que o modelo tem como alvo a [!INCLUDE[Compact](../extensibility/includes/compact_md.md)] versão 1,0.

- `SmartDevice-NETCFv2`: Especifica que o modelo tem como alvo a [!INCLUDE[Compact](../extensibility/includes/compact_md.md)] versão 2,0.

  Se um modelo contiver um `ProjectType` elemento com um valor de `Web` , o `ProjectSubType` elemento especificará a linguagem de programação do modelo. Esse elemento pode ter os seguintes valores:

- `CSharp`: Especifica que o modelo cria um [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] projeto da Web ou item.

- `VisualBasic`: Especifica que o modelo cria um [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] projeto da Web ou item.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra os metadados de um modelo de projeto para um [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] aplicativo de dispositivo destinado à [!INCLUDE[Compact](../extensibility/includes/compact_md.md)] versão 2,0.

```
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic device template</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <ProjectSubType>SmartDevice-NETCFv2</ProjectSubType>
    </TemplateData>
    <TemplateContent>
        <Project File="MyTemplate.csproj">
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
- [Criando modelos de projeto e item](../ide/creating-project-and-item-templates.md)
- [Elemento ProjectType (modelos do Visual Studio)](../extensibility/projecttype-element-visual-studio-templates.md)
