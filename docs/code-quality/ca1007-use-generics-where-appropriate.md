---
title: 'CA1007: usar genéricos quando apropriado'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1007
- UseGenericsWhereAppropriate
helpviewer_keywords:
- CA1007
- UseGenericsWhereAppropriate
ms.assetid: eab780ea-3b1f-4d32-b15a-5d48da2df46b
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: d3e03c1028dc310748aff7c8263ce75ace9985be
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45551722"
---
# <a name="ca1007-use-generics-where-appropriate"></a>CA1007: usar genéricos quando apropriado

|||
|-|-|
|NomeDoTipo|UseGenericsWhereAppropriate|
|CheckId|CA1007|
|Categoria|Microsoft.Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método visível externamente contém um parâmetro de referência do tipo <xref:System.Object?displayProperty=fullName>e os destinos de assembly contendo [!INCLUDE[dnprdnlong](../code-quality/includes/dnprdnlong_md.md)].

## <a name="rule-description"></a>Descrição da regra
 Um parâmetro de referência é um parâmetro que é modificado usando o `ref` (`ByRef` em [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]) palavra-chave. O tipo de argumento que é fornecido para um parâmetro de referência deve corresponder exatamente o tipo de parâmetro de referência. Para usar um tipo que é derivado do tipo de parâmetro de referência, o tipo primeiro ser convertido e atribuído a uma variável do tipo de parâmetro de referência. Uso de um método genérico permite que todos os tipos, sujeitos às restrições a serem passados para o método sem primeiramente converter o tipo para o tipo de parâmetro de referência.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, tornar o método genérico e substitua o <xref:System.Object> parâmetro usando um parâmetro de tipo.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra uma rotina de troca de finalidade geral que é implementada como métodos não genéricos e genéricos. Observe que a eficiência com as cadeias de caracteres são trocadas por meio do método genérico em comparação comparado o método não genérico.

 [!code-vb[FxCop.Design.UseGenerics#1](../code-quality/codesnippet/VisualBasic/ca1007-use-generics-where-appropriate_1.vb)]
 [!code-csharp[FxCop.Design.UseGenerics#1](../code-quality/codesnippet/CSharp/ca1007-use-generics-where-appropriate_1.cs)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1005: evitar parâmetros excessivos em tipos genéricos](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)

 [CA1010: as coleções devem implementar a interface genérica](../code-quality/ca1010-collections-should-implement-generic-interface.md)

 [CA1000: não declarar membros estáticos em tipos genéricos](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)

 [CA1002: não expor listas genéricas](../code-quality/ca1002-do-not-expose-generic-lists.md)

 [CA1006: não aninhar tipos genéricos em assinaturas de membro](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)

 [CA1004: os métodos genéricos devem fornecer o parâmetro de tipo](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)

 [CA1003: usar instâncias do manipulador de eventos genéricos](../code-quality/ca1003-use-generic-event-handler-instances.md)

## <a name="see-also"></a>Consulte também
 [Genéricos](/dotnet/csharp/programming-guide/generics/index)