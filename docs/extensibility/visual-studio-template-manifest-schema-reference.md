---
title: Referência de esquema do manifesto de modelo do Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: bc7d0a81-0df5-41a9-a912-1b30e5da1d13
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 38581d7c7dd788fef481676283fdc96c8abc96ba
ms.sourcegitcommit: 56ae5032d99d948aae0548ae318ca2bae97ea962
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2018
ms.locfileid: "39586295"
---
# <a name="visual-studio-template-manifest-schema-reference"></a>Referência de esquema do manifesto de modelo do Visual Studio
Esse esquema descreve o formato do manifesto de modelo do Visual Studio (*vstman*) arquivos que são gerados para os modelos de projeto ou item do Visual Studio. O esquema também descreve o local e outras informações relevantes sobre o modelo.  
  
 : Porque há item separado e diretórios do modelo de projeto, um manifesto nunca deve ter uma mistura de modelos de item e projeto.  
  
> [!IMPORTANT]
>  Esse manifesto está disponível a partir do Visual Studio 2017.  
  
## <a name="vstemplatemanifest-element"></a>Elemento VSTemplateManifest  
 O elemento raiz do manifesto.  
  
### <a name="attributes"></a>Atributos  
  
-   **Versão**: uma cadeia de caracteres que representa a versão do manifesto do modelo. Necessário.  
  
-   **Localidade**: uma cadeia de caracteres que representa a localidade ou localidades do manifesto do modelo. O valor da localidade se aplica a todos os modelos. Você deve usar um manifesto separado para cada localidade. Opcional.  
  
### <a name="child-elements"></a>Elementos filho  
  
-   **VSTemplateContainer** opcional.  
  
-   **VSTemplateDir** opcional.  
  
### <a name="parent-element"></a>Elemento pai  
 nenhuma.  
  
## <a name="vstemplatecontainer"></a>VSTemplateContainer  
 O contêiner do modelo de elementos do manifesto. Um manifesto tem um contêiner de modelo para cada modelo que ela define.  
  
### <a name="attributes"></a>Atributos  
 **VSTemplateType**: um valor de cadeia de caracteres que especifica o tipo do modelo (`"Project"`, `"Item"`, ou `"ProjectGroup"`). Necessária  
  
### <a name="child-elements"></a>Elementos filho  
  
-   **RelativePathOnDisk**: O caminho relativo do arquivo de modelo em disco. Esse local também define o posicionamento do modelo na árvore de modelo mostrado na **novo projeto** ou **Novo Item** caixa de diálogo. Para modelos implantados como um diretório e arquivos individuais, esse caminho se refere ao diretório que contém os arquivos de modelo. Para modelos implantados como uma *. zip* arquivo, esse caminho deve ser o caminho para o *. zip* arquivo.  
  
-   * * VSTemplateHeader: Um [TemplateData](../extensibility/templatedata-element-visual-studio-templates.md) elemento que descreve o cabeçalho.  
  
### <a name="parent-element"></a>Elemento pai  
 **VSTemplateManifest**  
  
## <a name="vstemplatedir"></a>VSTemplateDir  
 Descreve o diretório onde o modelo está localizado. Um manifesto pode conter vários **VSTemplateDir** entradas para fornecer o nome localizado e a ordem de classificação diretórios para controlar sua aparência na árvore de categoria do modelo.  
  
 Devido ao seu design **VSTemplateDir** entradas devem aparecer somente em manifestos de localidade não especificados.  
  
### <a name="attributes"></a>Atributos  
 nenhuma.  
  
### <a name="child-elements"></a>Elementos filho  
  
-   **RelativePath**: O caminho do modelo. Pode haver apenas uma entrada por caminho, portanto, a primeira delas será a vencedora para todos os manifestos.  
  
-   **LocalizedName**: uma **NameDescriptionIcon** elemento que especifica o nome localizado. Opcional.  
  
-   **SortOrder**: uma cadeia de caracteres que especifica a ordem de classificação. Opcional.  
  
-   **ParentFolderOverrideName**: O nome substituído da pasta pai. Opcional. Este elemento tem um **nome** atributo, que é um valor de cadeia de caracteres que especifica o nome.  
  
### <a name="parent-element"></a>Elemento pai  
 **VSTemplateManifest**  
  
## <a name="namedescriptionicon"></a>NameDescriptionIcon  
 Especifica o nome e descrição, possivelmente para modelos localizados. Ver **LocalizedName** acima.  
  
### <a name="attributes"></a>Atributos  
  
-   **Pacote**: um valor de cadeia de caracteres que especifica o pacote. Opcional.  
  
-   **ID**: um valor de cadeia de caracteres que especifica a ID. Opcional.  
  
### <a name="child-elements"></a>Elementos filho  
 nenhuma.  
  
### <a name="parent-element"></a>Elemento pai  
 **LocalizedName**  
  
## <a name="examples"></a>Exemplos  
 O código a seguir está um exemplo de um modelo de projeto *vstman* arquivo.  
  
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
  
 O código a seguir está um exemplo de um modelo de item *vstman* arquivo.  
  
```xml  
VSTemplateManifest Version="1.0" Locale="1033" xmlns="http://schemas.microsoft.com/developer/vstemplatemanifest/2015">  
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