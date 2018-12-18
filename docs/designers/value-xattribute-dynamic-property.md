---
title: Valor (propriedade dinâmica de XAttribute)
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-designers
ms.topic: reference
apiname:
- XAttribute.Value
apitype: Assembly
ms.assetid: 019733d2-e050-4120-b537-831cd3fc008e
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 473ff5b0124a050b60c9dc02929b2bad83f3661e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49842333"
---
# <a name="value-xattribute-dynamic-property"></a>Valor (propriedade dinâmica de XAttribute)

Obtém ou define o valor de atributo XML.

## <a name="syntax"></a>Sintaxe

```xaml
attrib.Value
```

## <a name="property-valuereturn-value"></a>Valor da propriedade/valor retornado

<xref:System.String> que contém o valor deste atributo.

## <a name="exceptions"></a>Exceções

|Tipo de exceção|Condição|
| - |---------------|
|<xref:System.ArgumentNullException>|Ao definir, `value` é `null`.|

## <a name="remarks"></a>Comentários

Esta propriedade é equivalente à propriedade de <xref:System.Xml.Linq.XAttribute.Value%2A> da classe de <xref:System.Xml.Linq.XAttribute?displayProperty=fullName> , mas suporta essa propriedade dinâmica também alterar notificações.

## <a name="see-also"></a>Consulte também

- <xref:System.Xml.Linq.XAttribute.Value%2A?displayProperty=fullName>
- [Propriedades dinâmicas da classe XAttribute](../designers/xattribute-class-dynamic-properties.md)
- [Atributo](../designers/attribute-xelement-dynamic-property.md)