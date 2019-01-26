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
ms.openlocfilehash: 815846ad310fa32ebcd3195806956cb34e40fd86
ms.sourcegitcommit: c0202a77d4dc562cdc55dc2e6223c062281d9749
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54876168"
---
# <a name="extensiondata-element"></a>Elemento ExtensionData
  Representa uma coleção de itens de dados personalizados que estão associados com o item de projeto do SharePoint.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<ExtensionData>  
  <ExtensionDataItem.../>  
</ExtensionData>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
 nenhuma.  
  
### <a name="child-elements"></a>Elementos filho
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[ExtensionDataItem](../sharepoint/extensiondataitem-element.md)|Elemento opcional.<br /><br /> Representa um item de dados personalizado que está associado com o item de projeto do SharePoint, no formato de chave/valor. A chave e o valor devem ser cadeias de caracteres.|  
  
### <a name="parent-elements"></a>Elementos pai
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[ProjectItem](../sharepoint/projectitem-element.md)|Representa um item de projeto do SharePoint. Esse elemento o elemento raiz necessário do `.spdata` arquivo.|  
  
## <a name="remarks"></a>Comentários  
 Quando você associar dados personalizados com um item de projeto do SharePoint usando o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> propriedade de um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem> do objeto, o Visual Studio salva os dados para o **ExtensionData** elemento no `.spdata` arquivo para o projeto item. Para obter mais informações, consulte [salvar os dados nas extensões do sistema de projeto do SharePoint](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md).  
  
## <a name="element-information"></a>Informações sobre o elemento
  
|||  
|-|-|  
|**Namespace**|http<nolink>://schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|  
|**Nome do esquema**|Esquema de Item de projeto do SharePoint|  
|**Arquivo de validação**|ProjectItemModelSchema.xsd|  
|**Pode estar vazio**|Não|  
  
## <a name="see-also"></a>Consulte também
 [Referência de esquema de item de projeto do SharePoint](../sharepoint/sharepoint-project-item-schema-reference.md)  
