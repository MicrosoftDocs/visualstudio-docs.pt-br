---
title: 'CA1401: P-Invokes não devem ser visíveis | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- PInvokesShouldNotBeVisible
- CA1401
helpviewer_keywords:
- CA1401
- PInvokesShouldNotBeVisible
ms.assetid: 0f4d96c1-f9de-414e-b223-4dc7f691bee3
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 9f13669959a5874c74753d304371b8ab7db14d4e
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547284"
---
# <a name="ca1401-pinvokes-should-not-be-visible"></a>CA1401: P/Invokes não deve estar visível
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|PInvokesShouldNotBeVisible|
|CheckId|CA1401|
|Categoria|Microsoft. Interoperability|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método público ou protegido em um tipo público tem o <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName> atributo (também implementado pela `Declare` palavra-chave em [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ).

## <a name="rule-description"></a>Descrição da Regra
 Os métodos que são marcados com o <xref:System.Runtime.InteropServices.DllImportAttribute> atributo (ou métodos que são definidos usando a `Declare` palavra-chave em [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ) usam os serviços de invocação de plataforma para acessar código não gerenciado. Esses métodos não devem ser expostos. Ao manter esses métodos privados ou internos, certifique-se de que sua biblioteca não pode ser usada para violar a segurança, permitindo que os chamadores acessem APIs não gerenciadas que não podiam chamar de outra forma.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, altere o nível de acesso do método.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir declara um método que viola essa regra.

 [!code-csharp[FxCop.Interoperability.DllImports#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.DllImports/cs/FxCop.Interoperability.DllImports.cs#1)]
 [!code-vb[FxCop.Interoperability.DllImports#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.DllImports/vb/FxCop.Interoperability.DllImports.vb#1)]
