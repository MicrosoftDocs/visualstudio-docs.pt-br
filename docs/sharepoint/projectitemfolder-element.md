---
title: Elemento ProjectItemFolder | Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ProjectItemFolder element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 38f8f70cc6480554441809e33c4083735600fbbb
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539809"
---
# <a name="projectitemfolder-element"></a>Elemento ProjectItemFolder
  Representa uma pasta mapeada.

## <a name="syntax"></a>Sintaxe

```xml
<ProjectItemFolder Target = "Path of SharePoint folder the mapped folder corresponds to"
    Type = "Type of deployment for the mapped folder" />
```

## <a name="type"></a>Type
 **ProjectItemFolderType**

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|**Destino**|Atributo **xs: String** necessário.<br /><br /> O caminho da pasta na instalação do SharePoint à qual a pasta mapeada corresponde, em relação à pasta raiz da implantação. A pasta raiz de implantação é determinada pelo tipo de implantação especificado pelo atributo de **tipo** .<br /><br /> Para obter mais informações, consulte as descrições das propriedades **caminho de implantação** e raiz de **implantação** dos itens de projeto do SharePoint em [desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md).|
|**Tipo**|Atributo **xs: String** necessário.<br /><br /> O tipo de implantação para a pasta mapeada. Para obter mais informações sobre os valores possíveis, consulte a descrição para a propriedade **tipo de implantação** de itens de projeto do SharePoint em [desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md).|

### <a name="child-elements"></a>Elementos filho
 Nenhum.

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[ProjectItem](../sharepoint/projectitem-element.md)|Representa um item de projeto do SharePoint. Esse é o elemento raiz necessário do arquivo *. COMDATA* .|

## <a name="remarks"></a>Comentários
 Para obter mais informações sobre pastas mapeadas, consulte [como adicionar e remover pastas mapeadas](../sharepoint/how-to-add-and-remove-mapped-folders.md).

## <a name="element-information"></a>Informações do elemento

|Propriedade|Valor|
|-|-|
|**Namespace**|http: \/ \/ schemas.Microsoft.com/VisualStudio/2010/<br>SharePointTools/SharePointProjectItemModel|
|**Nome do esquema**|Esquema de item de projeto do SharePoint|
|**Arquivo de validação**|ProjectItemModelSchema. xsd|
|**Pode estar vazio**|Não|

## <a name="see-also"></a>Consulte também
- [Referência de esquema de item de projeto do SharePoint](../sharepoint/sharepoint-project-item-schema-reference.md)
- [Como: Adicionar e remover pastas mapeadas](../sharepoint/how-to-add-and-remove-mapped-folders.md)
