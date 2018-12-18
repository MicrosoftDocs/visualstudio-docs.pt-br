---
title: 'CA2111: Ponteiros não devem estar visíveis | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- PointersShouldNotBeVisible
- CA2111
helpviewer_keywords:
- CA2111
- PointersShouldNotBeVisible
ms.assetid: b3a8d466-895b-43bc-a2df-5d7058fe915f
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 0d96a71a27a235887fe1744bbee09027c2c6d434
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49888913"
---
# <a name="ca2111-pointers-should-not-be-visible"></a>CA2111: os ponteiros não devem estar visíveis
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|PointersShouldNotBeVisible|
|CheckId|CA2111|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um público ou protegido <xref:System.IntPtr?displayProperty=fullName> ou <xref:System.UIntPtr?displayProperty=fullName> campo não é somente leitura.

## <a name="rule-description"></a>Descrição da Regra
 <xref:System.IntPtr> e <xref:System.UIntPtr> são tipos de ponteiro que são usados para acessar a memória não gerenciada. Se um ponteiro não for privado, interno ou somente leitura, o código mal-intencionado pode alterar o valor do ponteiro, potencialmente permitindo o acesso a locais arbitrários na memória ou causando falhas no aplicativo ou sistema.

 Se você pretender para proteger o acesso para o tipo que contém o campo de ponteiro, consulte [CA2112: tipos seguros não devem expor campos](../code-quality/ca2112-secured-types-should-not-expose-fields.md).

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Proteger o ponteiro, tornando-o somente leitura, interno ou privado.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Suprima um aviso nessa regra, se você não confie no valor do ponteiro.

## <a name="example"></a>Exemplo
 O código a seguir mostra os ponteiros que violam e atendem à regra. Observe que os ponteiros não privados também violam a regra [CA1051: não declarar campos de instância visíveis](../code-quality/ca1051-do-not-declare-visible-instance-fields.md).

 [!code-csharp[FxCop.Security.PointersArePrivate#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.PointersArePrivate/cs/FxCop.Security.PointersArePrivate.cs#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2112: os tipos seguros não devem expor campos](../code-quality/ca2112-secured-types-should-not-expose-fields.md)

 [CA1051: não declarar campos de instância visíveis](../code-quality/ca1051-do-not-declare-visible-instance-fields.md)

## <a name="see-also"></a>Consulte também
 <xref:System.IntPtr?displayProperty=fullName> <xref:System.UIntPtr?displayProperty=fullName>



