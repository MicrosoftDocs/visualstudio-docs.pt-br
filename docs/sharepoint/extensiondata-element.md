---
title: Elemento ExtensionData | Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ExtensionData element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 3b700239f97153cef94ab1d7010ad16ed9aa6001
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546556"
---
# <a name="extensiondata-element"></a>Elemento ExtensionData
  Representa uma coleção de itens de dados personalizados que estão associados ao item de projeto do SharePoint.

## <a name="syntax"></a>Sintaxe

```xml
<ExtensionData>
  <ExtensionDataItem.../>
</ExtensionData>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos
 Nenhum.

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|[ExtensionDataItem](../sharepoint/extensiondataitem-element.md)|Elemento opcional.<br /><br /> Representa um item de dados personalizado que está associado ao item de projeto do SharePoint, no formato de chave/valor. Tanto a chave quanto o valor devem ser cadeias de caracteres.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[ProjectItem](../sharepoint/projectitem-element.md)|Representa um item de projeto do SharePoint. Esse elemento é o elemento raiz necessário do `.spdata` arquivo.|

## <a name="remarks"></a>Comentários
 Quando você associa dados personalizados a um item de projeto do SharePoint usando a <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> propriedade de um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem> objeto, o Visual Studio salva os dados no elemento **ExtensionData** no `.spdata` arquivo para o item de projeto. Para obter mais informações, consulte [salvar dados em extensões do sistema de projeto do SharePoint](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md).

## <a name="element-information"></a>Informações do elemento

|Propriedade|Valor|
|-|-|
|**Namespace**|http: \/ \/ schemas.Microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**Nome do esquema**|Esquema de item de projeto do SharePoint|
|**Arquivo de validação**|ProjectItemModelSchema. xsd|
|**Pode estar vazio**|Não|

## <a name="see-also"></a>Consulte também
- [Referência de esquema de item de projeto do SharePoint](../sharepoint/sharepoint-project-item-schema-reference.md)
