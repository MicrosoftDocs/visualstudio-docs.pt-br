---
title: Elemento WizardData (modelos do Visual Studio) | Microsoft Docs
description: Saiba mais sobre o elemento WizardData e como ele especifica um XML personalizado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#WizardData
helpviewer_keywords:
- WizardData element [Visual Studio Templates]
- <WizardData> element [Visual Studio Templates]
ms.assetid: d0403a16-5d07-4fe5-b474-19ae3d9fd3ab
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bd7b85433b4e02491852589d32eea9a4f223da14
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061882"
---
# <a name="wizarddata-element-visual-studio-templates"></a>Elemento WizardData (modelos do Visual Studio)

Especifica XML personalizado

```xml
\<VSTemplate>
\<WizardData>
```

## <a name="syntax"></a>Sintaxe

```xml
<WizardData>
    <!-- XML to pass to the custom wizard extension -->
    ...
</WizardData>
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
|[VSTemplate](../extensibility/vstemplate-element-visual-studio-templates.md)|Elemento necessário.<br /><br /> Contém todos os metadados do modelo de projeto, modelo de item ou kit do iniciante.|

## <a name="text-value"></a>Valor de texto

Um valor de texto é opcional.

Esse texto especifica o XML personalizado a ser passado para a extensão do assistente personalizado especificada no elemento [WizardExtension](../extensibility/wizardextension-element-visual-studio-templates.md) .

## <a name="remarks"></a>Comentários

Qualquer XML pode ser especificado neste elemento. O XML será passado como um parâmetro para a extensão do assistente personalizado, permitindo que a extensão use o conteúdo deste elemento. Nenhuma validação é feita nesses dados.

O conteúdo do elemento **WizardData** é passado, inalterado, como um parâmetro dentro do dicionário de cadeia de caracteres de parâmetros no `IWizard.RunStarted` método. A chave do dicionário é nomeada `$wizarddata$` .

## <a name="example"></a>Exemplo

O exemplo a seguir ilustra os metadados para o modelo de projeto padrão para um aplicativo do Windows em C#.

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
    <WizardData>
        <!-- XML to pass to the custom wizard extension -->
    </WizardData>
</VSTemplate>
```

## <a name="see-also"></a>Confira também

- [Referência de esquema do modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
- [Elemento WizardExtension (Modelos do Visual Studio)](../extensibility/wizardextension-element-visual-studio-templates.md)
- [Como usar assistentes com modelos do projeto](../extensibility/how-to-use-wizards-with-project-templates.md)
