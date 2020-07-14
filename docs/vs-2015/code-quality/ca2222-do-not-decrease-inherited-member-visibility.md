---
title: 'CA2222: não diminua a visibilidade do membro herdada | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotDecreaseInheritedMemberVisibility
- CA2222
helpviewer_keywords:
- DoNotDecreaseInheritedMemberVisibility
- CA2222
ms.assetid: 066c8675-381f-43cc-956c-d757cc494028
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 04109e821d3a739b96ad63e1a441089a5d479cd8
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540771"
---
# <a name="ca2222-do-not-decrease-inherited-member-visibility"></a>CA2222: Não diminuir a visibilidade dos membros herdados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DoNotDecreaseInheritedMemberVisibility|
|CheckId|CA2222|
|Categoria|Microsoft. Usage|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um método particular em um tipo sem lacre tem uma assinatura que é idêntica a um método público declarado em um tipo base. O método particular não é final.

## <a name="rule-description"></a>Descrição da Regra
 Você não deve alterar o modificador de acesso para membros herdados. A alteração de um membro herdado para particular não impede que os chamadores acessem a implementação da classe base do método. Se o membro for tornado privado e o tipo não for lacrado, a herança de tipos poderá chamar a última implementação pública do método na hierarquia de herança. Se você precisar alterar o modificador de acesso, o método deverá ser marcado como final ou seu tipo deve ser lacrado para impedir que o método seja substituído.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, altere o acesso para não privado. Como alternativa, se a linguagem de programação oferecer suporte a ela, você poderá tornar o método final.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola essa regra.

 [!code-csharp[FxCop.Usage.InheritedPublic#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.InheritedPublic/cs/FxCop.Usage.InheritedPublic.cs#1)]
 [!code-vb[FxCop.Usage.InheritedPublic#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.InheritedPublic/vb/FxCop.Usage.InheritedPublic.vb#1)]
