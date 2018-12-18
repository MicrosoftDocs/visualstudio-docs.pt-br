---
title: 'CA1401: P-Invokes não devem ser visíveis | Microsoft Docs'
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
- PInvokesShouldNotBeVisible
- CA1401
helpviewer_keywords:
- CA1401
- PInvokesShouldNotBeVisible
ms.assetid: 0f4d96c1-f9de-414e-b223-4dc7f691bee3
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 23142fcb226259378be56c59032d3b96d9b94087
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49852499"
---
# <a name="ca1401-pinvokes-should-not-be-visible"></a>CA1401: P/Invokes não deve estar visível
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|PInvokesShouldNotBeVisible|
|CheckId|CA1401|
|Categoria|Microsoft.Interoperability|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método público ou protegido em um tipo público tem o <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName> atributo (também implementado pelos `Declare` palavra-chave em [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]).

## <a name="rule-description"></a>Descrição da Regra
 Métodos que são marcados com o <xref:System.Runtime.InteropServices.DllImportAttribute> atributo (ou métodos que são definidos usando o `Declare` palavra-chave em [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) usar serviços de invocação de plataforma para acessar código não gerenciado. Esses métodos não devem ser expostos. Mantendo esses métodos privado ou interno, você certifique-se de que sua biblioteca não pode ser usada de violação de segurança, permitindo que os chamadores acessem APIs não gerenciadas que não pôde chamar caso contrário.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, altere o nível de acesso do método.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir declara um método que viola essa regra.

 [!code-csharp[FxCop.Interoperability.DllImports#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.DllImports/cs/FxCop.Interoperability.DllImports.cs#1)]
 [!code-vb[FxCop.Interoperability.DllImports#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.DllImports/vb/FxCop.Interoperability.DllImports.vb#1)]



