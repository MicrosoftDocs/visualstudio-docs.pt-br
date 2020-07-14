---
title: 'CA1405: tipos base do tipo visível COM visíveis devem ser visíveis no COM | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1405
- ComVisibleTypeBaseTypesShouldBeComVisible
helpviewer_keywords:
- CA1405
- ComVisibleTypeBaseTypesShouldBeComVisible
ms.assetid: a762ea2f-5285-4f73-bfb9-9eb10aea4290
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 779d3ec1ed520d5d48043f90e7cb6272553012a6
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535038"
---
# <a name="ca1405-com-visible-type-base-types-should-be-com-visible"></a>CA1405: Tipos base de tipo visível no COM devem ser visíveis no COM
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|ComVisibleTypeBaseTypesShouldBeComVisible|
|CheckId|CA1405|
|Categoria|Microsoft. Interoperability|
|Alteração Significativa|DependsOnFix|

## <a name="cause"></a>Causa
 Um tipo visível Component Object Model (COM) deriva de um tipo que não é visível COM.

## <a name="rule-description"></a>Descrição da Regra
 Quando um tipo visível COM adiciona membros em uma nova versão, ele deve obedecer a diretrizes estritas para evitar a interrupção de clientes COM que se associam à versão atual. Um tipo invisível para COM pressupõe que ele não precisa seguir essas regras de controle de versão COM ao adicionar novos membros. No entanto, se um tipo visível COM for derivado do tipo invisível COM e expor uma interface de classe de <xref:System.Runtime.InteropServices.ClassInterfaceType?displayProperty=fullName> ou <xref:System.Runtime.InteropServices.ClassInterfaceType> (o padrão), todos os membros públicos do tipo base (a menos que estejam explicitamente marcados como com invisível, que seriam redundantes) serão expostos ao com. Se o tipo base adicionar novos membros em uma versão subsequente, todos os clientes COM que se associarem à interface de classe do tipo derivado poderão ser interrompidos. Tipos visíveis COM devem derivar somente de tipos visíveis COM para reduzir a chance de quebrar clientes COM.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, torne os tipos base COM visíveis ou o tipo derivado COM invisível.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola a regra.

 [!code-csharp[FxCop.Interoperability.ComBaseTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComBaseTypes/cs/FxCop.Interoperability.ComBaseTypes.cs#1)]
 [!code-vb[FxCop.Interoperability.ComBaseTypes#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComBaseTypes/vb/FxCop.Interoperability.ComBaseTypes.vb#1)]

## <a name="see-also"></a>Consulte Também
 <xref:System.Runtime.InteropServices.ClassInterfaceAttribute?displayProperty=fullName>[Introdução à interface de classe](https://msdn.microsoft.com/733c0dd2-12e5-46e6-8de1-39d5b25df024) [interoperação com código não gerenciado](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)
