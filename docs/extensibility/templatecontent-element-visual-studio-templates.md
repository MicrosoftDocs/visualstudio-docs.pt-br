---
title: Elemento TemplateContent (modelos do Visual Studio) | Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#TemplateContent
helpviewer_keywords:
- TemplateContent element [Visual Studio project templates]
ms.assetid: 90ae401c-b294-49ac-98da-e0d274f5bebb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 577ce71d3900947cde1de9a1e913124ab778a1ee
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "80699228"
---
# <a name="templatecontent-element-visual-studio-templates"></a>Elemento TemplateContent (modelos do Visual Studio)

Especifica o conteúdo do modelo.

Hierarquia de elementos:

```xml
<VSTemplate>
  <TemplateContent>
```

## <a name="syntax"></a>Syntax

```xml
<TemplateContent>
    ...
</TemplateContent>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|[BuildOnLoad](../extensibility/buildonload-visual-studio-templates.md)|Especifica se a solução deve ser compilada quando um projeto é criado a partir do modelo.|

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|[ProjectCollection](../extensibility/projectcollection-element-visual-studio-templates.md)|Elemento opcional.<br /><br /> Especifica a organização e o conteúdo de modelos de vários projetos.|
|[Projeto](../extensibility/project-element-visual-studio-templates.md)|Elemento opcional.<br /><br /> Especifica os arquivos ou diretórios a serem adicionados ao projeto.|
|[Referências](../extensibility/references-element-visual-studio-templates.md)|Elemento opcional.<br /><br /> Especifica as referências de assembly necessárias para um modelo de item.|
|[ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md)|Elemento opcional.<br /><br /> Especifica um arquivo contido no modelo.|
|[CustomParameters](../extensibility/customparameters-element-visual-studio-templates.md)|Elemento opcional.<br /><br /> Especifica os parâmetros personalizados que devem ser usados quando um projeto ou item é criado a partir do modelo.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[VSTemplate](../extensibility/vstemplate-element-visual-studio-templates.md)|Elemento necessário.<br /><br /> Contém todos os metadados do modelo de projeto, modelo de item ou kit do iniciante.|

## <a name="remarks"></a>Comentários
 `TemplateContent` é um elemento obrigatório.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra os metadados de um modelo de projeto para um [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] aplicativo.

```xml
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
</VSTemplate>
```

## <a name="see-also"></a>Confira também

- [Referência de esquema do modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
