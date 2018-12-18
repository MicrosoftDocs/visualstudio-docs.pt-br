---
title: 'CA1408: não usar AutoDual ClassInterfaceType'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotUseAutoDualClassInterfaceType
- CA1408
helpviewer_keywords:
- CA1408
- DoNotUseAutoDualClassInterfaceType
ms.assetid: 60ca5e02-3c51-42dd-942b-4f950eecfa0f
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: a4baa4f12a3d4cb113dd99f1cd3e158742c1ed1a
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45545600"
---
# <a name="ca1408-do-not-use-autodual-classinterfacetype"></a>CA1408: não usar AutoDual ClassInterfaceType

|||
|-|-|
|NomeDoTipo|DoNotUseAutoDualClassInterfaceType|
|CheckId|CA1408|
|Categoria|Microsoft.Interoperability|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo visível do modelo de objeto de componente (COM) está marcado com o <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> atributo definido como o `AutoDual` valor <xref:System.Runtime.InteropServices.ClassInterfaceType>.

## <a name="rule-description"></a>Descrição da regra
 Tipos que usam uma interface dupla permitem que clientes sejam associados a um layout de interface específico. Todas as alterações feitas em uma versão futura do layout do tipo ou de qualquer tipo de base interromperão clientes COM associados à interface. Por padrão, se o <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> atributo não for especificado, uma interface somente de expedição é usada.

 Marcado como caso contrário, todos os tipos não genéricos públicos são visíveis para COM; todos os tipos genéricos e não públicos são invisíveis a com.&lt;1}

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, altere o valor da <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> de atributo para o `None` valor de <xref:System.Runtime.InteropServices.ClassInterfaceType> e definir explicitamente a interface.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra, a menos que você tiver certeza de que o layout do tipo e seus tipos base não será alterado em uma versão futura.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra uma classe que viola a regra e uma nova declaração de classe para usar uma interface explícita.

 [!code-csharp[FxCop.Interoperability.AutoDual#1](../code-quality/codesnippet/CSharp/ca1408-do-not-use-autodual-classinterfacetype_1.cs)]
 [!code-vb[FxCop.Interoperability.AutoDual#1](../code-quality/codesnippet/VisualBasic/ca1408-do-not-use-autodual-classinterfacetype_1.vb)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1403: os tipos de layout automático não devem ser visíveis em COM](../code-quality/ca1403-auto-layout-types-should-not-be-com-visible.md)

 [CA1412: marcar interfaces ComSource como IDispatch](../code-quality/ca1412-mark-comsource-interfaces-as-idispatch.md)

## <a name="see-also"></a>Consulte também

- [Qualificando tipos .NET para interoperação](/dotnet/framework/interop/qualifying-net-types-for-interoperation)
- [Interoperação com código não gerenciado](/dotnet/framework/interop/index)