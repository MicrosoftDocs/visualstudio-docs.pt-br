---
title: 'CA1007: usar genéricos quando apropriado'
ms.date: 11/04/2016
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
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: d2c9416d1cdc655df110c7230b9f0e29290221a7
ms.sourcegitcommit: 485ffaedb1ade71490f11cf05962add1718945cc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72441693"
---
# <a name="ca1007-use-generics-where-appropriate"></a>CA1007: usar genéricos quando apropriado

|||
|-|-|
|NomeDoTipo|UseGenericsWhereAppropriate|
|CheckId|CA1007|
|Categoria|Microsoft. Design|
|Alteração significativa|Quebra|

## <a name="cause"></a>Causa
Um método visível externamente contém um parâmetro de referência do tipo <xref:System.Object?displayProperty=fullName> e os destinos de assembly que o contêm .NET Framework 2,0.

## <a name="rule-description"></a>Descrição da regra
Um parâmetro de referência é um parâmetro que é modificado usando a palavra-chave `ref` (`ByRef` na [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]). O tipo de argumento fornecido para um parâmetro de referência deve corresponder exatamente ao tipo de parâmetro de referência. Para usar um tipo derivado do tipo de parâmetro de referência, o tipo deve primeiro ser convertido e atribuído a uma variável do tipo de parâmetro de referência. O uso de um método genérico permite que todos os tipos, sujeitos a restrições, sejam passados para o método sem primeiro converter o tipo para o tipo de parâmetro de referência.

## <a name="how-to-fix-violations"></a>Como corrigir violações
Para corrigir uma violação dessa regra, torne o método genérico e substitua o parâmetro <xref:System.Object> usando um parâmetro de tipo.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
O exemplo a seguir mostra uma rotina de permuta de uso geral que é implementada como métodos não genéricos e genéricos. Observe quão eficientemente as cadeias de caracteres são trocadas usando o método genérico em comparação com o método não genérico.

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
