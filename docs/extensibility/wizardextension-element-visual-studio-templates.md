---
title: Elemento WizardExtension (modelos do Visual Studio) | Microsoft Docs
description: Saiba mais sobre o elemento WizardExtension e como ele contém os elementos de registro para personalizar o assistente de modelo.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#WizardExtension
helpviewer_keywords:
- WizardExtension element [Visual Studio Templates]
- <WizardExtension> element [Visual Studio Templates]
ms.assetid: d54b01c1-50f5-4b65-828c-686e2321cc8c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c32f9f2050e04741a2612de30e2718f45c0603de
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061804"
---
# <a name="wizardextension-element-visual-studio-templates"></a>Elemento WizardExtension (modelos do Visual Studio)
Contém os elementos de registro para personalizar o assistente de modelo.

 \<VSTemplate> ... \<WizardExtension>

## <a name="syntax"></a>Sintaxe

```
<WizardExtension>
    <Assembly>... </Assembly>
    <FullClassName>... </FullClassName>
</WizardExtension>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos
 Nenhum.

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|[Assembly](../extensibility/assembly-element-visual-studio-template-wizard-extension.md)|Elemento necessário.<br /><br /> Especifica o nome ou nome forte de um assembly que aparece no cache de assembly global. Deve haver pelo menos um `Assembly` elemento em um `WizardExtension` elemento.|
|[FullClassName](../extensibility/fullclassname-element-visual-studio-template-wizard-extension.md)|Elemento necessário.<br /><br /> O nome totalmente qualificado da classe que implementa a `IWizard` interface. Deve haver pelo menos um `FullClassName` elemento em um `WizardExtension` elemento.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[VSTemplate](../extensibility/vstemplate-element-visual-studio-templates.md)|Contém todos os metadados do modelo de projeto, modelo de item ou kit do iniciante.|

## <a name="remarks"></a>Comentários
 `WizardExtension` é um elemento filho opcional de `VSTemplate` .

## <a name="example"></a>Exemplo
 O exemplo a seguir ilustra os metadados para o modelo de projeto padrão para um [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] aplicativo do Windows.

```
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
    <WizardExtension>
        <Assembly>MyWizard, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, Custom=null</Assembly>
        <FullClassName>MyWizard.CustomWizard</FullClassName>
    </WizardExtension>
</VSTemplate>
```

## <a name="see-also"></a>Confira também
- [Referência de esquema do modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
- [Como usar assistentes com modelos do projeto](../extensibility/how-to-use-wizards-with-project-templates.md)
