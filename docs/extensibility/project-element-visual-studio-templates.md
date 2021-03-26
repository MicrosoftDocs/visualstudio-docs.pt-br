---
title: Elemento Project (modelos do Visual Studio) | Microsoft Docs
description: Saiba mais sobre o elemento Project e como ele especifica os arquivos ou diretórios a serem adicionados ao projeto.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Project
helpviewer_keywords:
- Project element [Visual Studio Templates]
- <Project> element [Visual Studio Templates]
ms.assetid: 1da15ea6-26e2-462b-a03e-584ef4996579
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 52bfb5f65aa9d42c46eece619a21152c51e8fa28
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068798"
---
# <a name="project-element-visual-studio-templates"></a>Elemento Project (modelos do Visual Studio)
Especifica os arquivos ou diretórios a serem adicionados ao projeto.

 \<VSTemplate> \<TemplateContent>
 \<Project>

## <a name="syntax"></a>Sintaxe

```
<Project
    File="MyProject.proj"
    TargetFileName="MyTargetProject.proj"
    ReplaceParameters="true/false">
    IgnoreProjectParameter="$myCustomParameter$"
        ...
</Project>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|`File`|Atributo obrigatório.<br /><br /> Especifica o nome do arquivo de projeto no arquivo *. zip* de modelo.|
|`ReplaceParameters`|Atributo opcional.<br /><br /> Um valor booliano que especifica se o arquivo de projeto tem valores de parâmetro que devem ser substituídos quando um projeto é criado a partir do modelo. O valor padrão é `false`.|
|`TargetFileName`|Atributo opcional.<br /><br /> Especifica o nome do arquivo de projeto quando um projeto é criado a partir do modelo.|
|`IgnoreProjectParameter`|Atributo opcional.<br /><br /> Especifica se o projeto deve ser adicionado à solução atual. Se o valor do parâmetro personalizado, "$*myCustomParameter*$" existir no arquivo de substituição de parâmetro, o projeto será criado, mas não adicionado como parte da solução aberta no momento.|

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|[Pasta](../extensibility/folder-element-visual-studio-project-templates.md)|Elemento opcional.<br /><br /> Especifica uma pasta a ser adicionada ao projeto.|
|[ProjectItem](../extensibility/projectitem-element-visual-studio-project-templates.md)|Elemento opcional.<br /><br /> Especifica um arquivo a ser adicionado a um projeto.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|Elemento necessário.|

## <a name="remarks"></a>Comentários
 `Project` é um elemento filho opcional de `TemplateContent` .

 O `Project` elemento é usado para especificar um projeto e, portanto, só é válido em modelos de projeto.

 `Project` os elementos podem ter elementos filho de [pasta](../extensibility/folder-element-visual-studio-project-templates.md) ou elementos filhos [ProjectItem](../extensibility/projectitem-element-visual-studio-project-templates.md) , mas não uma mistura de ambos os `Folder` `ProjectItem` elementos e filhos.

 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] renomeia automaticamente o nome do arquivo de projeto com base no nome inserido pelo usuário na caixa de diálogo **novo projeto** . Use o `TargetFileName` atributo se você quiser fornecer um nome de arquivo alternativo para arquivos de projeto criados com o modelo.

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
- [Criando modelos de projeto e item](../ide/creating-project-and-item-templates.md)
- [Elemento ProjectItem (modelos de projeto do Visual Studio)](../extensibility/projectitem-element-visual-studio-project-templates.md)
- [Elemento Folder (modelos de projeto do Visual Studio)](../extensibility/folder-element-visual-studio-project-templates.md)
