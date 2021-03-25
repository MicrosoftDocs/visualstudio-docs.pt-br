---
title: Elemento EnableEditOfLocationField (modelos do Visual Studio)
description: Saiba mais sobre o elemento EnableEditOfLocationField e como ele especifica se o usuário pode editar o campo local.
titleSuffix: ''
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- EnableEditOfLocationField (Visual Studio project templates)
ms.assetid: 51a91963-8a3f-4741-928e-bc90c11473bb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c3f2ca8799b0816ffe5c33d954d362183f330f25
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070187"
---
# <a name="enableeditoflocationfield-element-visual-studio-templates"></a>Elemento EnableEditOfLocationField (modelos do Visual Studio)
Especifica se o usuário pode editar o campo local.

 \<VSTemplate> \<TemplateData>
 \<EnableEditOfLocationField>

## <a name="syntax"></a>Sintaxe

```
<EnableEditOfLocationField> true/false </EnableEditOfLocationField>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos
 Nenhum

### <a name="child-elements"></a>Elementos filho
 Nenhum

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|Elemento necessário.<br /><br /> Categoriza o modelo e define como ele é exibido no **novo projeto** ou na caixa de diálogo **Adicionar novo item** .|

## <a name="text-value"></a>Valor de texto
 Um valor de texto é obrigatório.

 O texto deve ser `true` ou `false` , indicando se o usuário pode ou não editar a caixa de texto **local** na caixa de diálogo **novo projeto** .

## <a name="remarks"></a>Comentários
 `EnableEditOfLocationField` é um elemento opcional. O valor padrão é `true` , que permite ao usuário editar o valor na caixa de texto **local** na caixa de diálogo **novo projeto** .

 Na caixa de diálogo **novo projeto** , a caixa de texto **local** especifica o diretório em que um novo projeto é salvo.

## <a name="example"></a>Exemplo
 O exemplo a seguir ilustra os metadados de um [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] aplicativo do Windows.

```
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic starter kit</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <EnableEditOfLocationField>false</EnableEditOfLocationField>
        <EnableLocationBrowseButton>false</EnableLocationBrowseButton>
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
- [Criando modelos de projeto e item](../ide/creating-project-and-item-templates.md)
