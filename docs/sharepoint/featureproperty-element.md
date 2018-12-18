---
title: Elemento FeatureProperty | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- FeatureProperty element
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: ccc9e0d628d5c17283368de135c8e83dbd40bec1
ms.sourcegitcommit: e6b13898cfbd89449f786c2e8f3e3e7377afcf25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/22/2018
ms.locfileid: "36325976"
---
# <a name="featureproperty-element"></a>Elemento FeatureProperty
  Representa uma propriedade personalizada que está incluída com um recurso quando ele é implantado no SharePoint. Depois que um recurso é implantado, você pode acessar a propriedade em seu código.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<FeatureProperty Key = "Key of the property value"  
    Value = "Property value" />  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|**Chave**|Exigido **xs: string** atributo.<br /><br /> A chave que é usada para armazenar e recuperar o valor da propriedade. Cada propriedade deve ter uma chave que é exclusiva dentro do recurso.|  
|**Value**|Exigido **xs: string** atributo.<br /><br /> O valor da propriedade.|  
  
### <a name="child-elements"></a>Elementos filho
 nenhuma.  
  
### <a name="parent-elements"></a>Elementos pai
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[FeatureProperties](../sharepoint/featureproperties-element.md)|Representa uma coleção de valores de propriedade que são incluídos com um recurso quando ele é implantado no SharePoint.|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre as propriedades do recurso, consulte [fornecer informações de implantação de pacote e em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md).  
  
## <a name="element-information"></a>Informações sobre o elemento
  
|||  
|-|-|  
|**Namespace**|HTTP<nolink>: //schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|  
|**Nome do esquema**|Esquema de Item de projeto do SharePoint|  
|**Arquivo de validação**|ProjectItemModelSchema.xsd|  
|**Pode estar vazio**|Não|  
  
## <a name="see-also"></a>Consulte também
 [Referência de esquema de item de projeto do SharePoint](../sharepoint/sharepoint-project-item-schema-reference.md)   
 [Fornecer informações de empacotamento e implantação em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)  
  
  
