---
title: Elemento PromptForSaveOnCreation (modelos do Visual Studio)
titleSuffix: ''
description: Saiba mais sobre o elemento PromptForSaveOnCreation e como ele especifica se o usuário é solicitado a fornecer um local para salvar o projeto por meio da caixa de diálogo novo projeto.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#PromptForSaveOnCreation
helpviewer_keywords:
- PromptForSaveOnCreation element [Visual Studio project templates]
ms.assetid: 75174674-0c3c-4b57-b2fd-6ea8e817b67d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 5bc3c28bcfa35dac23c96d9a566b9767f8db9c1c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068637"
---
# <a name="promptforsaveoncreation-element-visual-studio-templates"></a>Elemento PromptForSaveOnCreation (modelos do Visual Studio)

Especifica se o usuário é solicitado a fornecer um local para salvar o projeto por meio da caixa de diálogo **novo projeto** ao criar um projeto. Se esse elemento for definido como `true` , o usuário será solicitado a fornecer um local de salvamento. Se `false` , em seguida, eles não são solicitados (ou seja, um projeto temporário é criado).

```xml
\<VSTemplate>
\<TemplateData>
\<PromptForSaveOnCreation>
```

## <a name="syntax"></a>Sintaxe

```xml
<PromptForSaveOnCreation> true/false </PromptForSaveOnCreation>
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

 O texto deve ser `true` ou `false` , `true` indicando que o usuário será solicitado a fornecer um local de salvamento ao criar um novo projeto.

## <a name="remarks"></a>Comentários
 `PromptForSaveOnCreation` é um elemento opcional. O valor padrão é `false`.

 Projetos temporários são projetos que você pode criar e modificar sem salvar o conteúdo desse projeto em disco.

## <a name="example"></a>Exemplo
 O exemplo a seguir define o valor de `PromptForSaveOnCreation` igual a `false` , que especifica para permitir que o projeto seja criado como um projeto temporário.

```xml
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic template</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <PromptForSaveOnCreation>false</PromptForSaveOnCreation>
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
- [Criar modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
