---
title: Valor (propriedade dinâmica de XAttribute) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
api_name:
- XAttribute.Value
api_type:
- Assembly
ms.assetid: 019733d2-e050-4120-b537-831cd3fc008e
caps.latest.revision: 4
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: bd9ea1fa163980a39bcd9981b9e1d757d72fcb6a
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49229145"
---
# <a name="value-xattribute-dynamic-property"></a>Valor (propriedade dinâmica de XAttribute)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Obtém ou define o valor de atributo XML.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
attrib.Value   
```  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/valor de retorno  
 <xref:System.String> que contém o valor deste atributo.  
  
## <a name="exceptions"></a>Exceções  
  
|Tipo de exceção|Condição|  
|--------------------|---------------|  
|<xref:System.ArgumentNullException>|Ao definir, `value` é `null`.|  
  
## <a name="remarks"></a>Comentários  
 Esta propriedade é equivalente à propriedade de <xref:System.Xml.Linq.XAttribute.Value%2A> da classe de <xref:System.Xml.Linq.XAttribute?displayProperty=fullName> , mas suporta essa propriedade dinâmica também alterar notificações.  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Xml.Linq.XAttribute.Value%2A?displayProperty=fullName>   
 [Propriedades dinâmicas da classe XAttribute](../designers/xattribute-class-dynamic-properties.md)   
 [Attribute](../designers/attribute-xelement-dynamic-property.md)



