---
title: 'CA1403: os tipos de layout automático não devem ser visíveis no COM | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AutoLayoutTypesShouldNotBeComVisible
- CA1403
helpviewer_keywords:
- CA1403
- AutoLayoutTypesShouldNotBeComVisible
ms.assetid: a7007714-f9b4-4730-94e0-67d3dc68991f
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 1752efb5be1828f62703e1fe1a1130b37ff80503
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534921"
---
# <a name="ca1403-auto-layout-types-should-not-be-com-visible"></a>CA1403: Tipos de layout automático não devem ser visíveis no COM
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|AutoLayoutTypesShouldNotBeComVisible|
|CheckId|CA1403|
|Categoria|Microsoft. Interoperability|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo de valor visível Component Object Model (COM) é marcado com o <xref:System.Runtime.InteropServices.StructLayoutAttribute?displayProperty=fullName> atributo definido como <xref:System.Runtime.InteropServices.LayoutKind?displayProperty=fullName> .

## <a name="rule-description"></a>Descrição da Regra
 <xref:System.Runtime.InteropServices.LayoutKind>os tipos de layout são gerenciados pelo Common Language Runtime. O layout desses tipos pode ser alterado entre as versões do .NET Framework, o que interromperá clientes COM que esperam um layout específico. Observe que, se o <xref:System.Runtime.InteropServices.StructLayoutAttribute> atributo não for especificado, os [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] compiladores C#, e C++ especificarão o <xref:System.Runtime.InteropServices.LayoutKind> layout para tipos de valor.

 A menos que marcado de outra forma, todos os tipos públicos não genéricos são visíveis para COM; todos os tipos não públicos e genéricos são invisíveis para COM. No entanto, para reduzir os falsos positivos, essa regra exige que a visibilidade COM do tipo seja explicitamente declarada; o assembly contentor deve ser marcado com o <xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName> definido como `false` e o tipo deve ser marcado com o <xref:System.Runtime.InteropServices.ComVisibleAttribute> definido como `true` .

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, altere o valor do <xref:System.Runtime.InteropServices.StructLayoutAttribute> atributo para <xref:System.Runtime.InteropServices.LayoutKind> ou <xref:System.Runtime.InteropServices.LayoutKind> , ou torne o tipo invisível para com.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola a regra e um tipo que satisfaz a regra.

 [!code-csharp[FxCop.Interoperability.AutoLayout#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.AutoLayout/cs/FxCop.Interoperability.AutoLayout.cs#1)]
 [!code-vb[FxCop.Interoperability.AutoLayout#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.AutoLayout/vb/FxCop.Interoperability.AutoLayout.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1408: Não usar AutoDual ClassInterfaceType](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md)

## <a name="see-also"></a>Consulte Também
 [Introdução à interface de classe](https://msdn.microsoft.com/733c0dd2-12e5-46e6-8de1-39d5b25df024) [qualificando tipos .net para interoperação](https://msdn.microsoft.com/library/4b8afb52-fb8d-4e65-b47c-fd82956a3cdd) [interoperabilidade com código não-gerenciado](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)
