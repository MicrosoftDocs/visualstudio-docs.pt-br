---
title: 'CA1012: tipos abstratos não devem ter construtores | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AbstractTypesShouldNotHaveConstructors
- CA1012
helpviewer_keywords:
- CA1012
ms.assetid: 09f458ac-dd88-4cd7-a47f-4106c1e80ece
caps.latest.revision: 27
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 2c88144e788fb35a3c330aa28b4e9d8b91ff8003
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545451"
---
# <a name="ca1012-abstract-types-should-not-have-constructors"></a>CA1012: Tipos abstratos não devem ter construtores
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|AbstractTypesShouldNotHaveConstructors|
|CheckId|CA1012|
|Categoria|Microsoft. Design|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um tipo público é abstrato e tem um construtor público.

## <a name="rule-description"></a>Descrição da Regra
 Construtores em tipos abstratos só podem ser chamados por tipos derivados. Como construtores públicos criam instâncias de um tipo e não é possível criar instâncias de um tipo abstrato, um tipo abstrato com um construtor público é projetado incorretamente.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, torne o construtor protegido ou não declare o tipo como abstrato.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra. O tipo abstrato tem um construtor público.

## <a name="example"></a>Exemplo
 O exemplo a seguir contém um tipo abstrato que viola essa regra.

 [!code-csharp[FxCop.Design.AbstractTypeBad#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AbstractTypeBad/cs/FxCop.Design.AbstractTypeBad.cs#1)]
 [!code-vb[FxCop.Design.AbstractTypeBad#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.AbstractTypeBad/vb/FxCop.Design.AbstractTypeBad.vb#1)]

## <a name="example"></a>Exemplo
 O exemplo a seguir corrige a violação anterior alterando a acessibilidade do construtor de `public` para `protected` .

 [!code-csharp[FxCop.Design.AbstractTypeGood#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AbstractTypeGood/cs/FxCop.Design.AbstractTypeGood.cs#1)]
 [!code-vb[FxCop.Design.AbstractTypeGood#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.AbstractTypeGood/vb/FxCop.Design.AbstractTypeGood.vb#1)]
