---
title: 'CA1010: as coleções devem implementar a interface genérica | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1010
- CollectionsShouldImplementGenericInterface
helpviewer_keywords:
- CA1010
- CollectionsShouldImplementGenericInterface
ms.assetid: c7d7126f-fa70-40be-8f93-3243e1760dc5
caps.latest.revision: 26
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: b141d755c717ad6650d2a49c98c2b26547066b7a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545516"
---
# <a name="ca1010-collections-should-implement-generic-interface"></a>CA1010: Coleções devem implementar uma interface genérica
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|CollectionsShouldImplementGenericInterface|
|CheckId|CA1010|
|Categoria|Microsoft. Design|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um tipo visível externamente implementa a <xref:System.Collections.IEnumerable?displayProperty=fullName> interface, mas não implementa a <xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName> interface e os destinos de assembly que a contêm [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] . Essa regra ignora os tipos que implementam <xref:System.Collections.IDictionary?displayProperty=fullName> .

## <a name="rule-description"></a>Descrição da Regra
 Para ampliar a usabilidade de uma coleção, implemente uma das interfaces da coleção genéricas. Em seguida, a coleção pode ser usada para preencher tipos de coleção genéricos, como o seguinte:

- <xref:System.Collections.Generic.List%601?displayProperty=fullName>

- <xref:System.Collections.Generic.Queue%601?displayProperty=fullName>

- <xref:System.Collections.Generic.Stack%601?displayProperty=fullName>

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, implemente uma das seguintes interfaces de coleção genéricas:

- <xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName>

- <xref:System.Collections.Generic.ICollection%601?displayProperty=fullName>

- <xref:System.Collections.Generic.IList%601?displayProperty=fullName>

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra; no entanto, a coleção terá um uso mais limitado.

## <a name="example-violation"></a>Violação de exemplo

### <a name="description"></a>Descrição
 O exemplo a seguir mostra uma classe (tipo de referência) que deriva da classe não genérica `CollectionBase` , que viola essa regra.

### <a name="code"></a>Código
 [!code-csharp[FxCop.Design.CollectionsGenericViolation#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.CollectionsGenericViolation/cs/FxCop.Design.CollectionsGenericViolation.cs#1)]

### <a name="comments"></a>Comentários
 Para corrigir uma violação dessa violação, você deve implementar as interfaces genéricas ou alterar a classe base para um tipo que já implemente as interfaces genéricas e não genéricas, como a `Collection<T>` classe.

## <a name="fix-by-base-class-change"></a>Correção por alteração de classe base

### <a name="description"></a>Descrição
 O exemplo a seguir corrige a violação alterando a classe base da coleção da classe não genérica `CollectionBase` para a `Collection<T>` classe genérica ( `Collection(Of T)` in [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ).

### <a name="code"></a>Código
 [!code-csharp[FxCop.Design.CollectionsGenericBase#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.CollectionsGenericBase/cs/FxCop.Design.CollectionsGenericBase.cs#1)]

### <a name="comments"></a>Comentários
 A alteração da classe base de uma classe já lançada é considerada uma alteração significativa nos consumidores existentes.

## <a name="fix-by-interface-implementation"></a>Corrigir por implementação de interface

### <a name="description"></a>Descrição
 O exemplo a seguir corrige a violação implementando essas interfaces genéricas: `IEnumerable<T>` , `ICollection<T>` , e `IList<T>` ( `IEnumerable(Of T)` , `ICollection(Of T)` e `IList(Of T)` em [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ).

### <a name="code"></a>Código
 [!code-csharp[FxCop.Design.CollectionsGenericInterface#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.CollectionsGenericInterface/cs/FxCop.Design.CollectionsGenericInterface.cs#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1005: Evitar parâmetros excessivos em tipos genéricos](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)

 [CA1000: Não declarar membros estáticos em tipos genéricos](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)

 [CA1002: Não expor listas genéricas](../code-quality/ca1002-do-not-expose-generic-lists.md)

 [CA1006: Não aninhar tipos genéricos em assinaturas de membro](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)

 [CA1004: Métodos genéricos devem fornecer um parâmetro de tipo](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)

 [CA1003: Usar instâncias do manipulador de eventos genérico](../code-quality/ca1003-use-generic-event-handler-instances.md)

 [CA1007: Usar genéricos quando apropriado](../code-quality/ca1007-use-generics-where-appropriate.md)

## <a name="see-also"></a>Consulte Também
 [Genéricos](https://msdn.microsoft.com/library/75ea8509-a4ea-4e7a-a2b3-cf72482e9282)
