---
title: 'CA1412: Marcar Interfaces ComSource como IDispatch | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- MarkComSourceInterfacesAsIDispatch
- CA1412
helpviewer_keywords:
- CA1412
- MarkComSourceInterfacesAsIDispatch
ms.assetid: 131a7563-0410-443c-a8f5-52104250cfb4
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: d72dd7e143720ce4ef2fce364a7e5ed3529ff9f3
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65691989"
---
# <a name="ca1412-mark-comsource-interfaces-as-idispatch"></a>CA1412: Marcar interfaces ComSource como IDispatch
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|MarkComSourceInterfacesAsIDispatch|
|CheckId|CA1412|
|Categoria|Microsoft.Interoperability|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo é marcado com o <xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute> atributo e pelo menos uma interface especificada não está marcado com o <xref:System.Runtime.InteropServices.InterfaceTypeAttribute> atributo definido como o `InterfaceIsDispatch` valor.

## <a name="rule-description"></a>Descrição da Regra
 <xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute> é usado para identificar as interfaces de evento que uma classe expõe para clientes do modelo de objeto de componente (COM). Essas interfaces devem ser expostas como `InterfaceIsIDispatch` para permitir que clientes COM do Visual Basic 6 receber notificações de eventos. Por padrão, se uma interface não está marcada com o <xref:System.Runtime.InteropServices.InterfaceTypeAttribute> atributo, ele é exposto como uma interface dupla.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, adicionar ou modificar as <xref:System.Runtime.InteropServices.InterfaceTypeAttribute> de atributo para que seu valor é definido como InterfaceIsIDispatch para todas as interfaces que são especificadas com o <xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute> atributo.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra uma classe em que uma das interfaces viola a regra.

 [!code-csharp[FxCop.Interoperability.MarkIDispatch#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.MarkIDispatch/cs/FxCop.Interoperability.MarkIDispatch.cs#1)]
 [!code-vb[FxCop.Interoperability.MarkIDispatch#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.MarkIDispatch/vb/FxCop.Interoperability.MarkIDispatch.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1408: Não usar AutoDual ClassInterfaceType](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md)

## <a name="see-also"></a>Consulte também
 [Como: Acionar eventos manipulados por um coletor COM](https://msdn.microsoft.com/7c9944b2-e951-4c3e-a0a1-59b2ae37d7fd) [interoperação com código não gerenciado](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)
