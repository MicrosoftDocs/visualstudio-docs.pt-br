---
title: 'CA1403: os tipos de layout automático não devem ser visíveis em COM'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AutoLayoutTypesShouldNotBeComVisible
- CA1403
helpviewer_keywords:
- CA1403
- AutoLayoutTypesShouldNotBeComVisible
ms.assetid: a7007714-f9b4-4730-94e0-67d3dc68991f
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: d84fdd4f352a823614832cc8d5d1b9e57c7a9dfb
ms.sourcegitcommit: 0bf2aff6abe485e3fe940f5344a62a885ad7f44e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2018
ms.locfileid: "37058068"
---
# <a name="ca1403-auto-layout-types-should-not-be-com-visible"></a>CA1403: os tipos de layout automático não devem ser visíveis em COM

|||
|-|-|
|NomeDoTipo|AutoLayoutTypesShouldNotBeComVisible|
|CheckId|CA1403|
|Categoria|Microsoft.Interoperability|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa

Um tipo de valor visível (COM Component Object Model) é marcado com o <xref:System.Runtime.InteropServices.StructLayoutAttribute?displayProperty=fullName> atributo definido como <xref:System.Runtime.InteropServices.LayoutKind.Auto?displayProperty=fullName>.

## <a name="rule-description"></a>Descrição da regra

<xref:System.Runtime.InteropServices.LayoutKind> tipos de layout são gerenciados pelo common language runtime. O layout desses tipos pode ser alterado entre as versões do .NET Framework, que interrompe a clientes COM que esperam um layout específico. Se o <xref:System.Runtime.InteropServices.StructLayoutAttribute> atributo não for especificado, os compiladores do c#, Visual Basic e C++ especificam [LayoutKind](<xref:System.Runtime.InteropServices.LayoutKind.Auto>) para tipos de valor.

Marcado como caso contrário, todos os tipos públicos e não genérica são visíveis no COM, e todos os tipos não públicos e genéricos são invisíveis a com.&lt;1} No entanto, para reduzir os falsos positivos, essa regra exige a visibilidade de COM do tipo a ser declarado explicitamente. O assembly que contém deve ser marcado com o <xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName> definido como `false` e o tipo deve ser marcado com o <xref:System.Runtime.InteropServices.ComVisibleAttribute> definido como `true`.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra, altere o valor da <xref:System.Runtime.InteropServices.StructLayoutAttribute> de atributo para [LayoutKind](<xref:System.Runtime.InteropServices.LayoutKind.Explicit>) ou [LayoutKind](<xref:System.Runtime.InteropServices.LayoutKind.Sequential>), ou fazer com que o tipo invisível a com.&lt;1}

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo

O exemplo a seguir mostra um tipo que viola a regra e um tipo que satisfaça a regra.

[!code-csharp[FxCop.Interoperability.AutoLayout#1](../code-quality/codesnippet/CSharp/ca1403-auto-layout-types-should-not-be-com-visible_1.cs)]
[!code-vb[FxCop.Interoperability.AutoLayout#1](../code-quality/codesnippet/VisualBasic/ca1403-auto-layout-types-should-not-be-com-visible_1.vb)]

## <a name="related-rules"></a>Regras relacionadas

[CA1408: não usar AutoDual ClassInterfaceType](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md)

## <a name="see-also"></a>Consulte também

- [Qualificar os tipos do .NET para interoperação](/dotnet/framework/interop/qualifying-net-types-for-interoperation)
- [Interoperar com código não gerenciado](/dotnet/framework/interop/index)