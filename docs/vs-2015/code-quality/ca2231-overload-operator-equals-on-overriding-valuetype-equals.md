---
title: 'CA2231: sobrecarga do operador Equals ao substituir ValueType. Equals | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- OverloadOperatorEqualsOnOverridingValueTypeEquals
- CA2231
- OverrideOperatorEqualsOnOverridingValueTypeEquals
helpviewer_keywords:
- OverloadOperatorEqualsOnOverridingValueTypeEquals
- CA2231
ms.assetid: 114c0161-261a-40ad-8b2c-0932d6909d2a
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: f01495e4238461d0b1dfe5a13a208b528df1581f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540290"
---
# <a name="ca2231-overload-operator-equals-on-overriding-valuetypeequals"></a>CA2231: Sobrecarregar operador equals ao substituir ValueType.Equals
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|OverloadOperatorEqualsOnOverridingValueTypeEquals|
|CheckId|CA2231|
|Categoria|Microsoft. Usage|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um tipo de valor substitui <xref:System.Object.Equals%2A?displayProperty=fullName> mas não implementa o operador de igualdade.

## <a name="rule-description"></a>Descrição da Regra
 Na maioria das linguagens de programação, não há nenhuma implementação padrão do operador de igualdade (= =) para tipos de valor. Se a linguagem de programação oferecer suporte a sobrecargas de operador, você deverá considerar a implementação do operador de igualdade. Seu comportamento deve ser idêntico ao de <xref:System.Object.Equals%2A> .

 Você não pode usar o operador de igualdade padrão em uma implementação sobrecarregada do operador de igualdade. Isso causará um estouro de pilha. Para implementar o operador de igualdade, use o método Object. Equals em sua implementação. Por exemplo:

```vb
If (Object.ReferenceEquals(left, Nothing)) Then
    Return Object.ReferenceEquals(right, Nothing)
Else
    Return left.Equals(right)
End If
```

```csharp
if (Object.ReferenceEquals(left, null))
    return Object.ReferenceEquals(right, null);
return left.Equals(right);
```

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, implemente o operador de igualdade.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra; no entanto, recomendamos que você forneça o operador de igualdade, se possível.

## <a name="example"></a>Exemplo
 O exemplo a seguir define um tipo que viola essa regra.

 [!code-csharp[FxCop.Usage.EqualsGetHashCode#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.EqualsGetHashCode/cs/FxCop.Usage.EqualsGetHashCode.cs#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1046: Não sobrecarregar o operador equals em tipos de referência](../code-quality/ca1046-do-not-overload-operator-equals-on-reference-types.md)

 [CA2225: Sobrecargas de operador têm alternativas nomeadas](../code-quality/ca2225-operator-overloads-have-named-alternates.md)

 [CA2226: Operadores devem ter sobrecargas simétricas](../code-quality/ca2226-operators-should-have-symmetrical-overloads.md)

 [CA2224: Substituir equals ao sobrecarregar operador equals](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md)

 [CA2218: Substituir GetHashCode ao substituir Equals](../code-quality/ca2218-override-gethashcode-on-overriding-equals.md)

## <a name="see-also"></a>Consulte Também
 <xref:System.Object.Equals%2A?displayProperty=fullName>
