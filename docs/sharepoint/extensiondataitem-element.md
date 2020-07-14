---
title: Elemento ExtensionDataItem | Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ExtensionDataItem element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 295ee649cec01e50b237b4fad1798806d460727b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546543"
---
# <a name="extensiondataitem-element"></a>Elemento ExtensionDataItem
  Um item de dados personalizado que está associado ao item de projeto do SharePoint, no formato de chave/valor. Tanto a chave quanto o valor devem ser cadeias de caracteres.

## <a name="syntax"></a>Sintaxe

```xml
<ExtensionDataItem Key = "Key of the data item"
    Value = "Value of the data item" />
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|**Chave**|Atributo **xs: String** necessário.<br /><br /> A chave usada para armazenar e recuperar o item de dados.|
|**Valor**|Atributo **xs: String** necessário.<br /><br /> O valor do item de dados.|

### <a name="child-elements"></a>Elementos filho
 Nenhum.

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[ExtensionData](../sharepoint/extensiondata-element.md)|Representa uma coleção de itens de dados personalizados que estão associados ao item de projeto do SharePoint.|

## <a name="remarks"></a>Comentários
 Quando você associa dados personalizados a um item de projeto do SharePoint usando a <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> propriedade de um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem> objeto, o Visual Studio salva os dados em um novo elemento **ExtensionDataItem** no `.spdata` arquivo para o item de projeto. Para obter mais informações, consulte [salvar dados em extensões do sistema de projeto do SharePoint](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md).

## <a name="element-information"></a>Informações do elemento

|Propriedade|Valor|
|-|-|
|**Namespace**|http: \/ \/ schemas.Microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**Nome do esquema**|Esquema de item de projeto do SharePoint|
|**Arquivo de validação**|ProjectItemModelSchema. xsd|
|**Pode estar vazio**|Não|

## <a name="see-also"></a>Confira também
- [Referência de esquema de item de projeto do SharePoint](../sharepoint/sharepoint-project-item-schema-reference.md)
