---
title: 'CA1007: Use genéricos quando apropriado | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1007
- UseGenericsWhereAppropriate
helpviewer_keywords:
- CA1007
- UseGenericsWhereAppropriate
ms.assetid: eab780ea-3b1f-4d32-b15a-5d48da2df46b
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 4ee33305c1ae0f15e5d8f390a4b65d62c87b6904
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547934"
---
# <a name="ca1007-use-generics-where-appropriate"></a>CA1007: Usar genéricos quando apropriado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|UseGenericsWhereAppropriate|
|CheckId|CA1007|
|Categoria|Microsoft. Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método visível externamente contém um parâmetro de referência do tipo <xref:System.Object?displayProperty=fullName> e os destinos de assembly que o contêm [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] .

## <a name="rule-description"></a>Descrição da Regra
 Um parâmetro de referência é um parâmetro que é modificado usando a `ref` `ByRef` [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] palavra-chave (in). O tipo de argumento fornecido para um parâmetro de referência deve corresponder exatamente ao tipo de parâmetro de referência. Para usar um tipo derivado do tipo de parâmetro de referência, o tipo deve primeiro ser convertido e atribuído a uma variável do tipo de parâmetro de referência. O uso de um método genérico permite que todos os tipos, sujeitos a restrições, sejam passados para o método sem primeiro converter o tipo para o tipo de parâmetro de referência.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, torne o método genérico e substitua o <xref:System.Object> parâmetro usando um parâmetro de tipo.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra uma rotina de permuta de uso geral que é implementada como métodos não genéricos e genéricos. Observe quão eficientemente as cadeias de caracteres são trocadas usando o método genérico em comparação com o método não genérico.

 [!code-csharp[FxCop.Design.UseGenerics#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.UseGenerics/cs/FxCop.Design.UseGenerics.cs#1)]
 [!code-vb[FxCop.Design.UseGenerics#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.UseGenerics/vb/FxCop.Design.UseGenerics.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1005: Evitar parâmetros excessivos em tipos genéricos](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)

 [CA1010: Coleções devem implementar uma interface genérica](../code-quality/ca1010-collections-should-implement-generic-interface.md)

 [CA1000: Não declarar membros estáticos em tipos genéricos](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)

 [CA1002: Não expor listas genéricas](../code-quality/ca1002-do-not-expose-generic-lists.md)

 [CA1006: Não aninhar tipos genéricos em assinaturas de membro](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)

 [CA1004: Métodos genéricos devem fornecer um parâmetro de tipo](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)

 [CA1003: Usar instâncias do manipulador de eventos genérico](../code-quality/ca1003-use-generic-event-handler-instances.md)

## <a name="see-also"></a>Consulte Também
 [Genéricos](https://msdn.microsoft.com/library/75ea8509-a4ea-4e7a-a2b3-cf72482e9282)
