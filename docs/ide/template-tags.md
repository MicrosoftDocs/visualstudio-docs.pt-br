---
title: Adicionar ou editar as marcas nos modelos de projeto
description: Saiba como adicionar ou editar as marcas nos modelos de projeto no Visual Studio.
ms.date: 04/30/2019
author: minsa110
ms.author: somin
manager: jillfra
ms.topic: reference
helpviewer_keywords:
- item templates, updating
- Visual Studio templates, updating
- project templates, updating
- updating templates [Visual Studio]
- template tagging, updating
- template tags, updating
ms.openlocfilehash: 37a1965712920420bdc4d784a003dbfbd2f2167a
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85285212"
---
# <a name="add-tags-to-project-templates"></a>Adicionar marcas aos modelos de projeto

A partir do [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/) versão 16.1 Preview 2, você poderá adicionar marcas de tipo de projeto, plataforma e linguagem aos seus modelos de projeto. 

As marcas são usadas em dois lugares na caixa de diálogo **Novo Projeto**:

- As marcas aparecem sob a descrição do modelo.

   ![O modelo de projeto com as marcas na caixa de diálogo Novo projeto](media/npd-item-with-template-tags.png)

- As marcas permitem que o modelo seja pesquisado e filtrado.

   ![Pesquisar e filtrar na caixa de diálogo Novo projeto](media/npd-search-and-filter.png)

Você pode adicionar marcas ao atualizar o arquivo XML *.vstemplate*. Você pode usar as marcas de modelo que são criadas no Visual Studio ou criar marcas de modelo personalizado. As marcas de modelo aparecem só na caixa de diálogo **Novo projeto** do Visual Studio 2019. As marcas de modelo não afetam como o modelo é renderizado nas versões anteriores do Visual Studio.

## <a name="add-or-edit-tags"></a>Adicionar ou editar marcas

Talvez você queira adicionar ou editar as marcas no XML *.vstemplate* do modelo de projeto ao executar uma das seguintes ações:

* [Criar um novo modelo de projeto](how-to-create-project-templates.md) usando o Assistente para Exportar Modelo.
* [Atualizar seu modelo de projeto existente](how-to-update-existing-templates.md).
* [Criar um novo modelo de projeto do VSIX](../extensibility/getting-started-with-the-vsix-project-template.md).

## <a name="syntax"></a>Sintaxe

```xml
<LanguageTag> Language Name </LanguageTag>
<PlatformTag> Platform Name </PlatformTag>
<ProjectTypeTag> Project Type </ProjectTypeTag>
```

## <a name="attributes"></a>Atributos

Você pode usar os seguintes atributos opcionais em cenários de usuário avançado:

|Atributo|Descrição|
|---------------|-----------------|
|`Package`|Um GUID que especifica a ID do pacote do Visual Studio.|
|`ID`|Especifica a ID de recurso do Visual Studio.|

Sintaxe:

```xml
<LanguageTag Package="{PackageID}" ID="ResourceID" />
<PlatformTag Package="{PackageID}" ID="ResourceID" />
<ProjectTypeTag Package="{PackageID}" ID="ResourceID" />
```

## <a name="elements"></a>Elementos

### <a name="child-elements"></a>Elementos filho

Nenhum.

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|(Obrigatório) Classifica o modelo e define como ele é exibido na caixa de diálogo **Novo Projeto** ou na caixa de diálogo **Adicionar Novo Item**.|

## <a name="text-value"></a>Valor de texto

É necessário um valor de texto, a menos que você use os atributos `Package` e `ID`.

O texto fornece o nome do modelo.

## <a name="built-in-tags"></a>Marcas internas

O Visual Studio oferece uma lista de marcas internas. Ao adicionar uma marca interna, a marca renderiza um recurso localizado. 

A lista a seguir mostra as marcas internas que estão disponíveis no Visual Studio. Os valores correspondentes são mostrados entre parênteses.

| Marca de idioma | Marca de plataforma | Marca de tipo de projeto |
| -- | -- | -- |
| C++ (`cpp`) | Android (`android`) | Nuvem (`cloud`) |
| C# (`csharp`) | Azure (`azure`) | Console (`console`) |
| F# (`fsharp`) | iOS (`ios`) | Área de trabalho (`desktop`) |
| Java (`java`) | Linux (`linux`) | Extensões (`extension`) |
| JavaScript (`javascript`) | macOS (`macos`) | Jogos (`games`) |
| Python (`python`) | tvOS (`tvos`) | IoT (`iot`) |
| Consulta de Idioma (`querylanguage`) | Windows (`windows`) | Biblioteca (`library`) |
| TypeScript (`typescript`) | Xbox (`xbox`) | Machine Learning (`machinelearning`) |
| Visual Basic (`visualbasic`) | | Dispositivo móvel (`mobile`) |
| | | Office (`office`) |
| | | Outros (`other`) |
| | | Serviço (`service`) |
| | | Teste (`test`) |
| | | UWP (`uwp`) |
| | | Web (`web`) |

## <a name="example"></a>Exemplo

O exemplo a seguir mostra os metadados para um modelo de projeto de um aplicativo do Visual C#:

```xml
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic template</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>csharp</ProjectType>
        <LanguageTag>C#</LanguageTag>
        <PlatformTag>windows</PlatformTag>
        <PlatformTag>linux</PlatformTag>
        <PlatformTag>My Platform</PlatformTag>
        <ProjectTypeTag>console</ProjectTypeTag>
        <ProjectTypeTag>desktop</ProjectTypeTag>
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

## <a name="see-also"></a>Veja também

- [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Criar modelos de projeto e de item](creating-project-and-item-templates.md)
- [Personalizar modelos de projeto e de item](customizing-project-and-item-templates.md)
- [Introdução ao modelo de projeto do VSIX](../extensibility/getting-started-with-the-vsix-project-template.md)
