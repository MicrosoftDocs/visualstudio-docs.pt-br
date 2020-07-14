---
title: 'CA1034: tipos aninhados não devem ser visíveis | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- NestedTypesShouldNotBeVisible
- CA1034
helpviewer_keywords:
- NestedTypesShouldNotBeVisible
- CA1034
ms.assetid: e9789a2c-2540-42a1-8705-ae7104011194
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 04a982c993ffbb04a3e7600dfb93a00e80727b84
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85542162"
---
# <a name="ca1034-nested-types-should-not-be-visible"></a>CA1034: Tipos aninhados não devem ser visíveis
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|NestedTypesShouldNotBeVisible|
|CheckId|CA1034|
|Categoria|Microsoft. Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo visível externamente contém uma declaração de tipo visível externamente. Enumerações aninhadas e tipos protegidos são isentos dessa regra.

## <a name="rule-description"></a>Descrição da Regra
 Um tipo aninhado é um tipo declarado dentro do escopo de outro tipo. Tipos aninhados são úteis para encapsular detalhes de implementação privada do tipo recipiente. Usados para essa finalidade, os tipos aninhados não devem ser visíveis externamente.

 Não use tipos aninhados externamente visíveis para agrupamento lógico ou para evitar colisões de nome; em vez disso, use namespaces.

 Os tipos aninhados incluem a noção de acessibilidade de membro, que alguns programadores não entendem claramente.

 Os tipos protegidos podem ser usados em subclasses e em tipos aninhados em cenários de personalização prévia.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Se você não pretender que o tipo aninhado fique visível externamente, altere a acessibilidade do tipo. Caso contrário, remova o tipo aninhado de seu pai. Se a finalidade do aninhamento for categorizar o tipo aninhado, use um namespace para criar a hierarquia em vez disso.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola a regra.

 [!code-cpp[FxCop.Design.NestedTypes#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.NestedTypes/cpp/FxCop.Design.NestedTypes.cpp#1)]
 [!code-csharp[FxCop.Design.NestedTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.NestedTypes/cs/FxCop.Design.NestedTypes.cs#1)]
 [!code-vb[FxCop.Design.NestedTypes#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.NestedTypes/vb/FxCop.Design.NestedTypes.vb#1)]
