---
title: 'CA1039: as listas são fortemente tipadas | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1039
- ListsAreStronglyTyped
helpviewer_keywords:
- CA1039
- ListsAreStronglyTyped
ms.assetid: 5ac366c4-fd87-4d5c-95d5-f755510c8e5c
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 4e485375c12564b5416c79bd3a41dedb1da76dc0
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85533439"
---
# <a name="ca1039-lists-are-strongly-typed"></a>CA1039: Listas são fortemente tipadas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|ListsAreStronglyTyped|
|CheckId|CA1039|
|Categoria|Microsoft. Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 O tipo público ou protegido implementa <xref:System.Collections.IList?displayProperty=fullName> , mas não fornece um método fortemente tipado para um ou mais dos seguintes:

- IList. Item

- IList. Add

- IList. Contains

- IList. IndexOf

- IList. Insert

- IList. Remove

## <a name="rule-description"></a>Descrição da Regra
 Essa regra requer <xref:System.Collections.IList> implementações para fornecer membros fortemente tipados para que os usuários não precisem converter argumentos para o <xref:System.Object?displayProperty=fullName> tipo quando usarem a funcionalidade fornecida pela interface. A <xref:System.Collections.IList> interface é implementada por coleções de objetos que podem ser acessados por índice. Essa regra pressupõe que o tipo que implementa <xref:System.Collections.IList> faz isso para gerenciar uma coleção de instâncias de um tipo que é mais forte do que <xref:System.Object> .

 <xref:System.Collections.IList>implementa as <xref:System.Collections.ICollection?displayProperty=fullName> <xref:System.Collections.IEnumerable?displayProperty=fullName> interfaces e. Se você implementar <xref:System.Collections.IList> o, deverá fornecer os membros com rigidez de tipos necessários para o <xref:System.Collections.ICollection> . Se os objetos na coleção se estenderem <xref:System.ValueType?displayProperty=fullName> , você deverá fornecer um membro fortemente tipado para <xref:System.Collections.IEnumerable.GetEnumerator%2A> para evitar a redução no desempenho causado por Boxing; isso não é necessário quando os objetos da coleção são um tipo de referência.

 Para obedecer a essa regra, implemente os membros da interface explicitamente usando nomes no formato InterfaceName. InterfaceMemberName, como <xref:System.Collections.IList.Add%2A> . Os membros da interface explícita usam os tipos de dados declarados pela interface. Implemente os membros fortemente tipados usando o nome de membro da interface, como `Add` . Declare os membros fortemente tipados como públicos e declare parâmetros e valores de retorno como sendo do tipo forte que é gerenciado pela coleção. Os tipos fortes substituem tipos mais fracos, como <xref:System.Object> e <xref:System.Array> que são declarados pela interface.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, implemente explicitamente <xref:System.Collections.IList> os membros e forneça alternativas fortemente tipadas para os membros que foram observados anteriormente. Para o código que implementa corretamente a <xref:System.Collections.IList> interface e fornece os membros com rigidez de tipos necessários, consulte o exemplo a seguir.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Suprimir um aviso desta regra ao implementar uma nova coleção baseada em objeto, como uma lista vinculada, em que os tipos que estendem a nova coleção determinam o tipo forte. Esses tipos devem estar em conformidade com essa regra e expor membros fortemente tipados.

## <a name="example"></a>Exemplo
 No exemplo a seguir, o tipo `YourType` estende <xref:System.Collections.CollectionBase?displayProperty=fullName> , como deve todas as coleções com rigidez de tipos. Observe que <xref:System.Collections.CollectionBase> o fornece a implementação explícita da <xref:System.Collections.IList> interface para você. Portanto, você deve fornecer somente os membros fortemente tipados para <xref:System.Collections.IList> e <xref:System.Collections.ICollection> .

 [!code-csharp[FxCop.Design.IListStrongTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.IListStrongTypes/cs/FxCop.Design.IListStrongTypes.cs#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1035: Implementações ICollection têm membros fortemente tipados](../code-quality/ca1035-icollection-implementations-have-strongly-typed-members.md)

 [CA1038: Enumeradores devem ser fortemente tipados](../code-quality/ca1038-enumerators-should-be-strongly-typed.md)

## <a name="see-also"></a>Consulte Também
 <xref:System.Collections.CollectionBase?displayProperty=fullName> <xref:System.Collections.ICollection?displayProperty=fullName>
 <xref:System.Collections.IEnumerable?displayProperty=fullName>
 <xref:System.Collections.IList?displayProperty=fullName>
 <xref:System.Object?displayProperty=fullName>
