---
title: 'CA2218: substituir GetHashCode ao substituir Equals | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2218
- OverrideGetHashCodeOnOverridingEquals
helpviewer_keywords:
- OverrideGetHashCodeOnOverridingEquals
- CA2218
ms.assetid: 69b020cd-29e8-45a6-952e-32cf3ce2e21d
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 8083edf04aa799c8031fbcd1b53a2e17104dd4a6
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85538795"
---
# <a name="ca2218-override-gethashcode-on-overriding-equals"></a>CA2218: Substituir GetHashCode ao substituir Equals
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|OverrideGetHashCodeOnOverridingEquals|
|CheckId|CA2218|
|Categoria|Microsoft. Usage|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um tipo público substitui <xref:System.Object.Equals%2A?displayProperty=fullName> , mas não substitui <xref:System.Object.GetHashCode%2A?displayProperty=fullName> .

## <a name="rule-description"></a>Descrição da Regra
 <xref:System.Object.GetHashCode%2A>Retorna um valor, com base na instância atual, que é adequada para algoritmos de hash e estruturas de dados, como uma tabela de hash. Dois objetos que são do mesmo tipo e são iguais devem retornar o mesmo código de hash para garantir que as instâncias dos seguintes tipos funcionem corretamente:

- <xref:System.Collections.Hashtable?displayProperty=fullName>

- <xref:System.Collections.SortedList?displayProperty=fullName>

- <xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName>

- <xref:System.Collections.Generic.SortedDictionary%602?displayProperty=fullName>

- <xref:System.Collections.Generic.SortedList%602?displayProperty=fullName>

- <xref:System.Collections.Specialized.HybridDictionary?displayProperty=fullName>

- <xref:System.Collections.Specialized.ListDictionary?displayProperty=fullName>

- <xref:System.Collections.Specialized.OrderedDictionary?displayProperty=fullName>

- Tipos que implementam<xref:System.Collections.Generic.IEqualityComparer%601?displayProperty=fullName>

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, forneça uma implementação de <xref:System.Object.GetHashCode%2A> . Para um par de objetos do mesmo tipo, você deve garantir que a implementação retorne o mesmo valor se sua implementação de <xref:System.Object.Equals%2A> retornos `true` para o par.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="class-example"></a>Exemplo de classe

### <a name="description"></a>Descrição
 O exemplo a seguir mostra uma classe (tipo de referência) que viola essa regra.

### <a name="code"></a>Código
 [!code-csharp[FxCop.Usage.GetHashCodeErrorClass#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.GetHashCodeErrorClass/cs/FxCop.Usage.GetHashCodeErrorClass.cs#1)]

### <a name="comments"></a>Comentários
 O exemplo a seguir corrige a violação substituindo <xref:System.Object.GetHashCode> .

### <a name="code"></a>Código
 [!code-csharp[FxCop.Usage.GetHashCodeFixedClass#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.GetHashCodeFixedClass/cs/FxCop.Usage.GetHashCodeFixedClass.cs#1)]

## <a name="structure-example"></a>Exemplo de estrutura

### <a name="description"></a>Descrição
 O exemplo a seguir mostra uma estrutura (tipo de valor) que viola essa regra.

### <a name="code"></a>Código
 [!code-csharp[FxCop.Usage.GetHashCodeErrorStruct#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.GetHashCodeErrorStruct/cs/FxCop.Usage.GetHashCodeErrorStruct.cs#1)]

### <a name="comments"></a>Comentários
 O exemplo a seguir corrige a violação substituindo <xref:System.Object.GetHashCode> .

### <a name="code"></a>Código
 [!code-csharp[FxCop.Usage.GetHashCodeFixedStruct#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.GetHashCodeFixedStruct/cs/FxCop.Usage.GetHashCodeFixedStruct.cs#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1046: Não sobrecarregar o operador equals em tipos de referência](../code-quality/ca1046-do-not-overload-operator-equals-on-reference-types.md)

 [CA2225: Sobrecargas de operador têm alternativas nomeadas](../code-quality/ca2225-operator-overloads-have-named-alternates.md)

 [CA2226: Operadores devem ter sobrecargas simétricas](../code-quality/ca2226-operators-should-have-symmetrical-overloads.md)

 [CA2224: Substituir equals ao sobrecarregar operador equals](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md)

 [CA2231: Sobrecarregar operador equals ao substituir ValueType.Equals](../code-quality/ca2231-overload-operator-equals-on-overriding-valuetype-equals.md)

## <a name="see-also"></a>Consulte também

- <xref:System.Object.Equals%2A?displayProperty=fullName>
- <xref:System.Object.GetHashCode%2A?displayProperty=fullName>
- <xref:System.Collections.Hashtable?displayProperty=fullName>
- [Operadores de igualdade](https://msdn.microsoft.com/library/bc496a91-fefb-4ce0-ab4c-61f09964119a)