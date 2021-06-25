---
title: Referência de esquema de manifesto de modelo do Visual Studio | Microsoft Docs
description: Esta referência de esquema descreve o formato dos arquivos de manifesto do modelo do Visual Studio que são gerados para modelos de projeto ou item do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: bc7d0a81-0df5-41a9-a912-1b30e5da1d13
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 259d2dd050f4681053f331bfd4ec39dd7b214059
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905378"
---
# <a name="visual-studio-template-manifest-schema-reference"></a>Referência de esquema de manifesto de modelo do Visual Studio
Este esquema descreve o formato dos arquivos de manifesto do modelo do Visual Studio (*. vstman*) que são gerados para modelos de projeto ou item do Visual Studio. O esquema também descreve o local e outras informações relevantes sobre o modelo.

 : Como há itens separados e diretórios de modelo de projeto, um manifesto nunca deve ter uma mistura de modelos de item e de projeto.

> [!IMPORTANT]
> Esse manifesto está disponível a partir do Visual Studio 2017.

## <a name="vstemplatemanifest-element"></a>Elemento VSTemplateManifest
 O elemento raiz do manifesto.

### <a name="attributes"></a>Atributos

- **Version**: uma cadeia de caracteres que representa a versão do manifesto do modelo. Obrigatórios.

- **Localidade**: uma cadeia de caracteres que representa a localidade ou as localidades do manifesto do modelo. O valor da localidade se aplica a todos os modelos. Você deve usar um manifesto separado para cada localidade. Opcional.

### <a name="child-elements"></a>Elementos filho

- **VSTemplateContainer** Adicional.

- **VSTemplateDir** Adicional.

### <a name="parent-element"></a>Elemento pai
 Nenhum.

## <a name="vstemplatecontainer"></a>VSTemplateContainer
 O contêiner dos elementos de manifesto do modelo. Um manifesto tem um contêiner de modelo para cada modelo definido por ele.

### <a name="attributes"></a>Atributos
 **Vstemplatetype**: um valor de cadeia de caracteres que especifica o tipo do modelo ( `"Project"` , `"Item"` ou `"ProjectGroup"` ). Obrigatório

### <a name="child-elements"></a>Elementos filho

- **RelativePathOnDisk**: o caminho relativo do arquivo de modelo no disco. Esse local também define o posicionamento do modelo na árvore de modelos mostrada na caixa de diálogo **novo projeto** ou **novo item** . Para modelos implantados como um diretório e arquivos individuais, esse caminho refere-se ao diretório que contém os arquivos de modelo. Para modelos implantados como um arquivo de *.zip* , esse caminho deve ser o caminho para o arquivo de *.zip* .

- * * VSTemplateHeader: um elemento [TemplateData](../extensibility/templatedata-element-visual-studio-templates.md) que descreve o cabeçalho.

### <a name="parent-element"></a>Elemento pai
 **VSTemplateManifest**

## <a name="vstemplatedir"></a>VSTemplateDir
 Descreve o diretório em que o modelo está localizado. Um manifesto pode conter várias entradas de **VSTemplateDir** para fornecer nomes localizados e ordenar a ordem dos diretórios para controlar sua aparência na árvore de categoria de modelo.

 Devido ao seu design, as entradas **VSTemplateDir** devem aparecer apenas em manifestos especificados que não sejam de localidade.

### <a name="attributes"></a>Atributos
 Nenhum.

### <a name="child-elements"></a>Elementos filho

- **RelativePath**: o caminho do modelo. Pode haver apenas uma entrada por caminho, portanto, a primeira será ganhar por todos os manifestos.

- **Localizadaname**: um elemento **NameDescriptionIcon** que especifica o nome localizado. Opcional.

- **SortOrder**: uma cadeia de caracteres que especifica a ordem de classificação. Opcional.

- **ParentFolderOverrideName**: o nome substituído da pasta pai. Opcional. Esse elemento tem um atributo **Name** , que é um valor de cadeia de caracteres que especifica o nome.

### <a name="parent-element"></a>Elemento pai
 **VSTemplateManifest**

## <a name="namedescriptionicon"></a>NameDescriptionIcon
 Especifica o nome e a descrição, possivelmente para modelos localizados. Consulte o **localizador** acima.

### <a name="attributes"></a>Atributos

- **Package**: um valor de cadeia de caracteres que especifica o pacote. Opcional.

- **ID**: um valor de cadeia de caracteres que especifica a ID. Opcional.

### <a name="child-elements"></a>Elementos filho
 Nenhum.

### <a name="parent-element"></a>Elemento pai
 **Localizador**

## <a name="examples"></a>Exemplos
 O código a seguir é um exemplo de um arquivo template *. vstman* do projeto.

```xml
<VSTemplateManifest Version="1.0" Locale="1033" xmlns="http://schemas.microsoft.com/developer/vstemplatemanifest/2015">
  <VSTemplateContainer TemplateType="Project">
    <RelativePathOnDisk>CSharp\1033\TestProjectTemplate</RelativePathOnDisk>
    <TemplateFileName>TestProjectTemplate.vstemplate</TemplateFileName>
    <VSTemplateHeader>
      <TemplateData xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
        <Name>TestProjectTemplate</Name>
        <Description>TestProjectTemplate</Description>
        <Icon>TestProjectTemplate.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
        <SortOrder>1000</SortOrder>
        <TemplateID>aac0aeea-7883-4003-992f-937d53d70ab1</TemplateID>
        <CreateNewFolder>true</CreateNewFolder>
        <DefaultName>TestProjectTemplate</DefaultName>
        <ProvideDefaultName>true</ProvideDefaultName>
      </TemplateData>
    </VSTemplateHeader>
  </VSTemplateContainer>
</VSTemplateManifest>

```

 O código a seguir é um exemplo de um arquivo template *. vstman* de item.

```xml
<VSTemplateManifest Version="1.0" Locale="1033" xmlns="http://schemas.microsoft.com/developer/vstemplatemanifest/2015">
  <VSTemplateContainer TemplateType="Item">
    <RelativePathOnDisk>CSharp\1033\ItemTemplate1</RelativePathOnDisk>
    <TemplateFileName>ItemTemplate1.vstemplate</TemplateFileName>
    <VSTemplateHeader>
      <TemplateData xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
        <Name>ItemTemplate1</Name>
        <Description>ItemTemplate1</Description>
        <Icon>ItemTemplate1.ico</Icon>
        <TemplateID>bfeadf8e-a251-4109-b605-516b88e38c8d</TemplateID>
        <ProjectType>CSharp</ProjectType>
        <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
        <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>
        <DefaultName>Class.cs</DefaultName>
      </TemplateData>
    </VSTemplateHeader>
  </VSTemplateContainer>
</VSTemplateManifest>

```
