---
title: Elemento de assembly (Extensão do Assistente de Modelo do Visual Studio)
titleSuffix: ''
description: Saiba mais sobre o elemento assembly e como ele especifica o nome ou o nome forte do assembly que implementa a interface IWizard.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Assembly
helpviewer_keywords:
- Assembly element [Visual Studio Template Wizard Extension]
- <Assembly> element [Visual Studio Template Wizard Extension]
ms.assetid: 0c3dc280-1753-4ea2-a13c-d31d13b935b2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1be9c72c01746b716b0202843b86ed2d5d52d44b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097481"
---
# <a name="assembly-element-visual-studio-template-wizard-extension"></a>Elemento assembly (extensão do assistente de modelo do Visual Studio)
Especifica o nome ou nome forte do assembly que implementa a `IWizard` interface.

 \<VSTemplate>
\<WizardExtension>
\<Assembly>

## <a name="syntax"></a>Sintaxe

```xml
<Assembly>AssemblyName</Assembly>
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
|[WizardExtension](../extensibility/wizardextension-element-visual-studio-templates.md)|Contém os elementos de registro para personalizar o assistente de modelo.|

## <a name="text-value"></a>Valor de texto
 Um valor de texto é obrigatório.

 Esse texto especifica o assembly que implementa a `IWizard` interface. Esse nome de assembly deve ser especificado como um nome de assembly completo. Por exemplo, `MyAssembly, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=b03f5f7f11dd0a3a, Custom = null`.

## <a name="remarks"></a>Comentários
 `Assembly` é um elemento filho obrigatório de `WizardExtension` .

## <a name="example"></a>Exemplo
 O exemplo a seguir ilustra os metadados para o modelo de projeto padrão para um [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] aplicativo do Windows.

```xml
<VSTemplate Version="3.0.0" Type="Item"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyTemplate</Name>
        <Description>Template using IWizard extension</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
    </TemplateData>
    <TemplateContent>
        <Project File="MyTemplate.csproj">
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
    <WizardExtension>
        <Assembly>MyWizard, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=b03f5f7f11dd0a3a, Custom=null</Assembly>
        <FullClassName>MyWizard.CustomWizard</FullClassName>
    </WizardExtension>
</VSTemplate>
```

## <a name="see-also"></a>Confira também

- [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Criando modelos de projeto e item](../ide/creating-project-and-item-templates.md)
- [Como: usar assistentes com modelos de projeto](../extensibility/how-to-use-wizards-with-project-templates.md)
