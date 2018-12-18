---
title: Elemento ProjectItemFolder | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ProjectItemFolder element
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 54d47165117b88041346e9b666db8db17a20ddb9
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37118544"
---
# <a name="projectitemfolder-element"></a>Elemento ProjectItemFolder
  Representa uma pasta mapeada.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<ProjectItemFolder Target = "Path of SharePoint folder the mapped folder corresponds to"  
    Type = "Type of deployment for the mapped folder" />  
```  
  
## <a name="type"></a>Tipo  
 **ProjectItemFolderType**  
  
## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|**Target**|Exigido **xs: string** atributo.<br /><br /> O caminho da pasta de instalação do SharePoint que a pasta mapeada corresponde a, em relação à pasta raiz de implantação. Pasta raiz de implantação é determinada pelo tipo de implantação especificado pelo **tipo** atributo.<br /><br /> Para obter mais informações, consulte as descrições para o **caminho de implantação** e **raiz da implantação** propriedades do SharePoint itens de projeto do [SharePoint desenvolver soluções](../sharepoint/developing-sharepoint-solutions.md).|  
|**Tipo**|Exigido **xs: string** atributo.<br /><br /> O tipo de implantação para a pasta mapeada. Para obter mais informações sobre os valores possíveis, consulte a descrição para o **tipo de implantação** propriedade de itens de projeto do SharePoint no [soluções do SharePoint desenvolver](../sharepoint/developing-sharepoint-solutions.md).|  
  
### <a name="child-elements"></a>Elementos filho
 nenhuma.  
  
### <a name="parent-elements"></a>Elementos pai
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[Item de projeto](../sharepoint/projectitem-element.md)|Representa um item de projeto do SharePoint. Este é o elemento raiz necessário do *. spdata* arquivo.|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre pastas mapeadas, consulte [como: adicionar e remover pastas mapeadas](../sharepoint/how-to-add-and-remove-mapped-folders.md).  
  
## <a name="element-information"></a>Informações sobre o elemento
  
|||  
|-|-|  
|**Namespace**|HTTP<nolink>: //schemas.microsoft.com/VisualStudio/2010/<br>SharePointTools/SharePointProjectItemModel|  
|**Nome do esquema**|Esquema de Item de projeto do SharePoint|  
|**Arquivo de validação**|ProjectItemModelSchema.xsd|  
|**Pode estar vazio**|Não|  
  
## <a name="see-also"></a>Consulte também
 [Referência de esquema de item de projeto do SharePoint](../sharepoint/sharepoint-project-item-schema-reference.md)   
 [Como: adicionar e remover pastas mapeadas](../sharepoint/how-to-add-and-remove-mapped-folders.md)  
  
