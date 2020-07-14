---
title: 'CA2111: os ponteiros não devem ser visíveis | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- PointersShouldNotBeVisible
- CA2111
helpviewer_keywords:
- CA2111
- PointersShouldNotBeVisible
ms.assetid: b3a8d466-895b-43bc-a2df-5d7058fe915f
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 7429251a66ce2fe22a825a153cb90248faabb9fd
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544359"
---
# <a name="ca2111-pointers-should-not-be-visible"></a>CA2111: Ponteiros não devem ser visíveis
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|PointersShouldNotBeVisible|
|CheckId|CA2111|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um campo público ou <xref:System.IntPtr?displayProperty=fullName> protegido <xref:System.UIntPtr?displayProperty=fullName> não é somente leitura.

## <a name="rule-description"></a>Descrição da Regra
 <xref:System.IntPtr>e <xref:System.UIntPtr> são tipos de ponteiro que são usados para acessar memória não gerenciada. Se um ponteiro não for privado, interno ou somente leitura, o código mal-intencionado poderá alterar o valor do ponteiro, potencialmente permitindo o acesso a locais arbitrários na memória ou causando falhas de aplicativo ou sistema.

 Se você pretende proteger o acesso ao tipo que contém o campo ponteiro, consulte [CA2112: tipos protegidos não devem expor campos](../code-quality/ca2112-secured-types-should-not-expose-fields.md).

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Proteja o ponteiro tornando-o somente leitura, interno ou privado.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Suprimir um aviso dessa regra se você não depender do valor do ponteiro.

## <a name="example"></a>Exemplo
 O código a seguir mostra os ponteiros que violam e satisfazem a regra. Observe que os ponteiros não privados também violam a regra [CA1051: Não declare campos de instância visíveis](../code-quality/ca1051-do-not-declare-visible-instance-fields.md).

 [!code-csharp[FxCop.Security.PointersArePrivate#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.PointersArePrivate/cs/FxCop.Security.PointersArePrivate.cs#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2112: Tipos protegidos não devem expor campos](../code-quality/ca2112-secured-types-should-not-expose-fields.md)

 [CA1051: Não declarar campos de instância visíveis](../code-quality/ca1051-do-not-declare-visible-instance-fields.md)

## <a name="see-also"></a>Consulte Também
 <xref:System.IntPtr?displayProperty=fullName> <xref:System.UIntPtr?displayProperty=fullName>
