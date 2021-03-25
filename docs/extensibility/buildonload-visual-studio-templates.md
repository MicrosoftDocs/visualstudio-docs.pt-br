---
title: Atributo e elemento BuildOnLoad (modelos do Visual Studio)
titleSuffix: ''
description: Saiba mais sobre o atributo e o elemento BuildOnLoad e como ele especifica se deseja compilar o projeto imediatamente após sua criação.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#BuildOnLoad
helpviewer_keywords:
- BuildOnLoad attribute [Visual Studio Templates]
- BuildOnLoad element [Visual Studio Templates]
ms.assetid: 950f5fc1-d041-4090-9a5c-60844768a4cc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8eb563e765c3d50950f61a0ca49e5349a0e7249a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068174"
---
# <a name="buildonload-attribute-and-element"></a>Elemento e atributo BuildOnLoad

Especifica se o projeto deve ser compilado imediatamente após ser criado. **BuildOnLoad** é um atributo e um elemento.

Hierarquia de elementos:

```xml
<VSTemplate>
  <TemplateData>
    <BuildOnLoad>
```

## <a name="element-syntax"></a>Sintaxe do elemento

```xml
<BuildOnLoad> true/false </BuildOnLoad>
```

## <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|Categoriza o modelo e define como ele é exibido no **novo projeto** ou na caixa de diálogo **Adicionar novo item** .|

## <a name="text-value"></a>Valor de texto

Um valor de texto é necessário para o elemento **BuildOnLoad** . O texto deve ser `true` ou `false` , indicando se deseja criar o projeto imediatamente após sua criação.

## <a name="remarks"></a>Comentários

**BuildOnLoad** é um atributo opcional. O valor padrão é `false`.

## <a name="example"></a>Exemplo

O exemplo a seguir ilustra os metadados de um modelo C# quando **BuildOnLoad** é usado como um elemento:

```xml
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic template</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <BuildOnLoad>true</BuildOnLoad>
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

- [Elemento BuildProjectOnload](buildprojectonload-element-visual-studio-templates.md)
- [Elemento TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)
- [Criando modelos de projeto e item](../ide/creating-project-and-item-templates.md)
- [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
