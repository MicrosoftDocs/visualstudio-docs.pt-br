---
title: 'CA1412: marcar interfaces ComSource como IDispatch'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- MarkComSourceInterfacesAsIDispatch
- CA1412
helpviewer_keywords:
- CA1412
- MarkComSourceInterfacesAsIDispatch
ms.assetid: 131a7563-0410-443c-a8f5-52104250cfb4
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: b992f546582fbd5b8bd82732b19ec4d72a6afd25
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45549931"
---
# <a name="ca1412-mark-comsource-interfaces-as-idispatch"></a>CA1412: marcar interfaces ComSource como IDispatch

|||
|-|-|
|NomeDoTipo|MarkComSourceInterfacesAsIDispatch|
|CheckId|CA1412|
|Categoria|Microsoft.Interoperability|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa

Um tipo é marcado com o <xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute> atributo e pelo menos uma interface especificada não está marcado com o <xref:System.Runtime.InteropServices.InterfaceTypeAttribute> atributo definido como o `InterfaceIsDispatch` valor.

## <a name="rule-description"></a>Descrição da regra

<xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute> é usado para identificar as interfaces de evento que uma classe expõe para clientes do modelo de objeto de componente (COM). Essas interfaces devem ser expostas como `InterfaceIsIDispatch` para permitir que clientes COM do Visual Basic 6 receber notificações de eventos. Por padrão, se uma interface não está marcada com o <xref:System.Runtime.InteropServices.InterfaceTypeAttribute> atributo, ele é exposto como uma interface dupla.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra, adicionar ou modificar as <xref:System.Runtime.InteropServices.InterfaceTypeAttribute> de atributo para que seu valor é definido como InterfaceIsIDispatch para todas as interfaces que são especificadas com o <xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute> atributo.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo

O exemplo a seguir mostra uma classe em que uma das interfaces viola a regra.

[!code-csharp[FxCop.Interoperability.MarkIDispatch#1](../code-quality/codesnippet/CSharp/ca1412-mark-comsource-interfaces-as-idispatch_1.cs)]
[!code-vb[FxCop.Interoperability.MarkIDispatch#1](../code-quality/codesnippet/VisualBasic/ca1412-mark-comsource-interfaces-as-idispatch_1.vb)]

## <a name="related-rules"></a>Regras relacionadas

[CA1408: não usar AutoDual ClassInterfaceType](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md)

## <a name="see-also"></a>Consulte também

- [Interoperação com código não gerenciado](/dotnet/framework/interop/index)