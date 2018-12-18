---
title: 'CA1010: as coleções devem implementar a interface genérica'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1010
- CollectionsShouldImplementGenericInterface
helpviewer_keywords:
- CA1010
- CollectionsShouldImplementGenericInterface
ms.assetid: c7d7126f-fa70-40be-8f93-3243e1760dc5
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 5264292e6dc1e8cf86a64d41dc15154d836a8444
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49915276"
---
# <a name="ca1010-collections-should-implement-generic-interface"></a>CA1010: as coleções devem implementar a interface genérica

|||
|-|-|
|NomeDoTipo|CollectionsShouldImplementGenericInterface|
|CheckId|CA1010|
|Categoria|Microsoft.Design|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Um tipo visível externamente implementa o <xref:System.Collections.IEnumerable?displayProperty=fullName> interface, mas não implementa o <xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName> interface e os destinos de assembly que contém [!INCLUDE[dnprdnlong](../code-quality/includes/dnprdnlong_md.md)]. Essa regra sempre ignora os tipos que implementam <xref:System.Collections.IDictionary?displayProperty=fullName>.

## <a name="rule-description"></a>Descrição da regra
 Para ampliar a usabilidade de uma coleção, implemente uma das interfaces da coleção genéricas. Em seguida, a coleção pode ser usada para popular tipos de coleção genérica, como o seguinte:

- <xref:System.Collections.Generic.List%601?displayProperty=fullName>

- <xref:System.Collections.Generic.Queue%601?displayProperty=fullName>

- <xref:System.Collections.Generic.Stack%601?displayProperty=fullName>

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, implemente uma das seguintes interfaces de coleção genérica:

- <xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName>

- <xref:System.Collections.Generic.ICollection%601?displayProperty=fullName>

- <xref:System.Collections.Generic.IList%601?displayProperty=fullName>

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir um aviso nessa regra; No entanto, a coleção terá um uso mais limitado.

## <a name="example-violation"></a>Violação de exemplo

### <a name="description"></a>Descrição
 O exemplo a seguir mostra uma classe (tipo de referência) que deriva de não-genérica `CollectionBase` classe, que viola essa regra.

### <a name="code"></a>Código
 [!code-csharp[FxCop.Design.CollectionsGenericViolation#1](../code-quality/codesnippet/CSharp/ca1010-collections-should-implement-generic-interface_1.cs)]

### <a name="comments"></a>Comentários
 Para corrigir uma violação dessa violação, você deve implementar as interfaces genéricas ou altere a classe base para um tipo que já implementa ambas as interfaces genéricas e não genéricas, como o `Collection<T>` classe.

## <a name="fix-by-base-class-change"></a>Corrigir pela mudança de classe Base

### <a name="description"></a>Descrição
 O exemplo a seguir corrige a violação ao alterar a classe base da coleção de não-genérica `CollectionBase` classe genérica `Collection<T>` (`Collection(Of T)` em [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]) classe.

### <a name="code"></a>Código
 [!code-csharp[FxCop.Design.CollectionsGenericBase#1](../code-quality/codesnippet/CSharp/ca1010-collections-should-implement-generic-interface_2.cs)]

### <a name="comments"></a>Comentários
 Alterando a classe base de uma classe já lançada é considerada uma alteração significativa para os consumidores existentes.

## <a name="fix-by-interface-implementation"></a>Corrigir pela implementação da Interface

### <a name="description"></a>Descrição
 O exemplo a seguir corrige a violação ao implementar essas interfaces genéricas: `IEnumerable<T>`, `ICollection<T>`, e `IList<T>` (`IEnumerable(Of T)`, `ICollection(Of T)`, e `IList(Of T)` em [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]).

### <a name="code"></a>Código
 [!code-csharp[FxCop.Design.CollectionsGenericInterface#1](../code-quality/codesnippet/CSharp/ca1010-collections-should-implement-generic-interface_3.cs)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1005: evitar parâmetros excessivos em tipos genéricos](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)

 [CA1000: não declarar membros estáticos em tipos genéricos](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)

 [CA1002: não expor listas genéricas](../code-quality/ca1002-do-not-expose-generic-lists.md)

 [CA1006: não aninhar tipos genéricos em assinaturas de membro](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)

 [CA1004: os métodos genéricos devem fornecer o parâmetro de tipo](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)

 [CA1003: usar instâncias do manipulador de eventos genéricos](../code-quality/ca1003-use-generic-event-handler-instances.md)

 [CA1007: usar genéricos quando apropriado](../code-quality/ca1007-use-generics-where-appropriate.md)

## <a name="see-also"></a>Consulte também
 [Genéricos](/dotnet/csharp/programming-guide/generics/index)