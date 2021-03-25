---
title: Elemento CreateNewFolder (modelos do Visual Studio) | Microsoft Docs
description: Saiba mais sobre o elemento CreateNewFolder e como ele determina se deve verificar se o diretório de destino onde o projeto deve ser criado não existe.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#CreateNewFolder
helpviewer_keywords:
- CreateNewFolder element [Visual Studio project templates]
ms.assetid: acef2016-4140-45d6-ace8-b8160eabd676
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3c2d8da615c350fc53b81532972cef65f6cd6ed7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089466"
---
# <a name="createnewfolder-element-visual-studio-templates"></a>Elemento CreateNewFolder (modelos do Visual Studio)
Determina se deve ser verificado se o diretório de destino onde o projeto será criado existe ou não. Se o diretório não existir, um novo diretório poderá ser criado para o projeto. Essa configuração é normalmente substituída pelo sinalizador de registro `NewProjectRequiresNewFolder(VsTemplate)` (`HKEY_LOCAL_MACHINE/SOFTWARE(/Wow6432Node)/Microsoft/VisualStudio/<version number>/Projects/<project GUID>`) que todos os tipos de projetos comuns usam para determinar se um novo projeto deve ser criado ou não em um novo diretório.

 \<VSTemplate> \<TemplateData>
 \<CreateNewFolder>

## <a name="syntax"></a>Sintaxe

```
<CreateNewFolder>
    true/false
</CreateNewFolder>
```

## <a name="type"></a>Type
 `Boolean`

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

 O texto deve ser `true` ou `false`, indicando se uma nova pasta de contêiner deve ou não ser criada quando um projeto é criado a partir do modelo.

## <a name="remarks"></a>Comentários
 `CreateNewFolder` é um elemento opcional. O valor padrão é `true`.

 O valor especificado no elemento `CreateNewFolder` só será considerado por [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] se o sistema de projeto subjacente suportá-lo.

## <a name="example"></a>Exemplo
 O exemplo de código a seguir especifica para não criar uma nova pasta quando um projeto é criado a partir do modelo.

```
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic template</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <CreateNewFolder>false</CreateNewFolder>
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
