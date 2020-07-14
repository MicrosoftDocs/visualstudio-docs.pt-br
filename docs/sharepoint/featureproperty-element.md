---
title: Elemento FeatureProperty | Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- FeatureProperty element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 61eeea33c6941624ed18a00db482590590a44a8f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546517"
---
# <a name="featureproperty-element"></a>Elemento FeatureProperty
  Representa uma propriedade personalizada que é incluída com um recurso quando é implantada no SharePoint. Depois que um recurso é implantado, você pode acessar a propriedade em seu código.

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
|**Chave**|Atributo **xs: String** necessário.<br /><br /> A chave usada para armazenar e recuperar o valor da propriedade. Cada propriedade deve ter uma chave que seja exclusiva dentro do recurso.|
|**Valor**|Atributo **xs: String** necessário.<br /><br /> O valor da propriedade.|

### <a name="child-elements"></a>Elementos filho
 Nenhum.

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Recursoproperties](../sharepoint/featureproperties-element.md)|Representa uma coleção de valores de propriedade que são incluídos com um recurso quando ele é implantado no SharePoint.|

## <a name="remarks"></a>Comentários
 Para obter mais informações sobre as propriedades do recurso, consulte [fornecendo informações de pacote e de implantação em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md).

## <a name="element-information"></a>Informações do elemento

|Propriedade|Valor|
|-|-|
|**Namespace**|http: \/ \/ schemas.Microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**Nome do esquema**|Esquema de item de projeto do SharePoint|
|**Arquivo de validação**|ProjectItemModelSchema. xsd|
|**Pode estar vazio**|Não|

## <a name="see-also"></a>Consulte também
- [Referência de esquema de item de projeto do SharePoint](../sharepoint/sharepoint-project-item-schema-reference.md)
- [Fornecer informações de empacotamento e implantação em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)
