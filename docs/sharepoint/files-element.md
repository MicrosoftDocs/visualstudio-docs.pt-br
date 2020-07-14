---
title: Elemento files | Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Files element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 42e919bbe25047da14940203ac86793430aeadde
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546504"
---
# <a name="files-element"></a>Elemento de arquivos
  Especifica os arquivos a serem implantados com o item de projeto do SharePoint, como arquivos de elemento de recurso e a saída de projetos dependentes que não são do SharePoint.

## <a name="syntax"></a>Sintaxe

```xml
<Files>
  <ProjectItemFile.../>
  <ProjectOutputFile.../>
</Files>
```

## <a name="type"></a>Type
 **Filecollectiontype**

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos
 Nenhum.

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|[ProjectItemfile](../sharepoint/projectitemfile-element.md)|Elemento **ProjectItemFileType** opcional.<br /><br /> Representa um arquivo do SharePoint, como um arquivo de elemento de recurso, a ser incluído com o item de projeto quando ele é implantado no SharePoint.|
|[ProjectOutputFile](../sharepoint/projectoutputfile-element.md)|Elemento **ProjectOutputFileType** opcional.<br /><br /> Representa a saída de um projeto a ser incluído com o item de projeto quando ele é implantado no SharePoint.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[ProjectItem](../sharepoint/projectitem-element.md)|Representa um item de projeto do SharePoint. Esse elemento é o elemento raiz necessário do `.spdata` arquivo.|

## <a name="element-information"></a>Informações do elemento

|Propriedade|Valor|
|-|-|
|**Namespace**|http: \/ \/ schemas.Microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**Nome do esquema**|Esquema de item de projeto do SharePoint|
|**Arquivo de validação**|ProjectItemModelSchema. xsd|
|**Pode estar vazio**|Não|

## <a name="see-also"></a>Confira também
- [Referência de esquema de item de projeto do SharePoint](../sharepoint/sharepoint-project-item-schema-reference.md)
