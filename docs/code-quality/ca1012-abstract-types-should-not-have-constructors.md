---
title: 'CA1012: Tipos abstratos não devem ter construtores'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.topic: reference
f1_keywords:
- AbstractTypesShouldNotHaveConstructors
- CA1012
helpviewer_keywords:
- CA1012
ms.assetid: 09f458ac-dd88-4cd7-a47f-4106c1e80ece
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 81a9fe50b4141b10e3946e3494ff325d1cc302b5
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53825091"
---
# <a name="ca1012-abstract-types-should-not-have-constructors"></a>CA1012: Tipos abstratos não devem ter construtores

|||
|-|-|
|NomeDoTipo|AbstractTypesShouldNotHaveConstructors|
|CheckId|CA1012|
|Categoria|Microsoft.Design|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Um tipo público é abstrato e tem um construtor público.

## <a name="rule-description"></a>Descrição da regra
 Construtores em tipos abstratos só podem ser chamados por tipos derivados. Como construtores públicos criam instâncias de um tipo e não é possível criar instâncias de um tipo abstrato, um tipo abstrato com um construtor público é projetado incorretamente.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, verifique o construtor protegido ou não declarar o tipo como abstrato.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra. O tipo abstrato tem um construtor público.

## <a name="example"></a>Exemplo
 O exemplo a seguir contém um tipo abstrato que viola essa regra.

 [!code-vb[FxCop.Design.AbstractTypeBad#1](../code-quality/codesnippet/VisualBasic/ca1012-abstract-types-should-not-have-constructors_1.vb)]
 [!code-csharp[FxCop.Design.AbstractTypeBad#1](../code-quality/codesnippet/CSharp/ca1012-abstract-types-should-not-have-constructors_1.cs)]

## <a name="example"></a>Exemplo
 O exemplo a seguir corrige a violação anterior, alterando a acessibilidade do construtor de `public` para `protected`.

 [!code-csharp[FxCop.Design.AbstractTypeGood#1](../code-quality/codesnippet/CSharp/ca1012-abstract-types-should-not-have-constructors_2.cs)]
 [!code-vb[FxCop.Design.AbstractTypeGood#1](../code-quality/codesnippet/VisualBasic/ca1012-abstract-types-should-not-have-constructors_2.vb)]