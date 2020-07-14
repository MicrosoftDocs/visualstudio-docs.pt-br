---
title: 'CA1035: implementações ICollection têm membros fortemente tipados | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ICollectionImplementationsHaveStronglyTypedMembers
- CA1035
helpviewer_keywords:
- CA1035
- ICollectionImplementationsHaveStronglyTypedMembers
ms.assetid: ad404eb5-cf6a-44b7-b78a-8ebfb654bc7f
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 2e679fb3cc62ba80cfb7b56dfd7fa6590375565e
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546608"
---
# <a name="ca1035-icollection-implementations-have-strongly-typed-members"></a>CA1035: Implementações ICollection têm membros fortemente tipados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|ICollectionImplementationsHaveStronglyTypedMembers|
|CheckId|CA1035|
|Categoria|Microsoft. Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público ou protegido implementa <xref:System.Collections.ICollection?displayProperty=fullName> , mas não fornece um método fortemente tipado para <xref:System.Collections.ICollection.CopyTo%2A?displayProperty=fullName> . A versão fortemente tipada do <xref:System.Collections.ICollection.CopyTo%2A> deve aceitar dois parâmetros e não pode ter um <xref:System.Array?displayProperty=fullName> ou uma matriz de <xref:System.Object?displayProperty=fullName> como seu primeiro parâmetro.

## <a name="rule-description"></a>Descrição da Regra
 Essa regra requer <xref:System.Collections.ICollection> implementações para fornecer membros fortemente tipados para que os usuários não precisem converter argumentos para o <xref:System.Object> tipo quando usarem a funcionalidade fornecida pela interface. Essa regra pressupõe que o tipo que implementa <xref:System.Collections.ICollection> faz isso para gerenciar uma coleção de instâncias de um tipo que é mais forte do que <xref:System.Object> .

 <xref:System.Collections.ICollection> implementa a interface <xref:System.Collections.IEnumerable?displayProperty=fullName>. Se os objetos na coleção se estenderem <xref:System.ValueType?displayProperty=fullName> , você deverá fornecer um membro fortemente tipado para <xref:System.Collections.IEnumerable.GetEnumerator%2A> para evitar a redução no desempenho causado por boxing. Isso não é necessário quando os objetos da coleção são um tipo de referência.

 Para implementar uma versão fortemente tipada de um membro de interface, implemente os membros da interface explicitamente usando nomes no formulário `InterfaceName.InterfaceMemberName` , como <xref:System.Collections.ICollection.CopyTo%2A> . Os membros da interface explícita usam os tipos de dados declarados pela interface. Implemente os membros fortemente tipados usando o nome de membro da interface, como <xref:System.Collections.ICollection.CopyTo%2A> . Declare os membros fortemente tipados como públicos e declare parâmetros e valores de retorno como sendo do tipo forte que é gerenciado pela coleção. Os tipos fortes substituem tipos mais fracos, como <xref:System.Object> e <xref:System.Array> que são declarados pela interface.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, implemente o membro da interface explicitamente (declare-o como <xref:System.Collections.ICollection.CopyTo%2A> ). Adicione o membro fortemente tipado público, declarado como `CopyTo` , e faça com que ele use uma matriz fortemente tipada como seu primeiro parâmetro.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Suprimir um aviso dessa regra se você implementar uma nova coleção baseada em objeto, como uma árvore binária, em que os tipos que estendem a nova coleção determinam o tipo forte. Esses tipos devem estar em conformidade com essa regra e expor membros fortemente tipados.

## <a name="example"></a>Exemplo
 O exemplo a seguir demonstra a maneira correta de implementar <xref:System.Collections.ICollection> .

 [!code-csharp[FxCop.Design.ICollectionStrongTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ICollectionStrongTypes/cs/FxCop.Design.ICollectionStrongTypes.cs#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1038: Enumeradores devem ser fortemente tipados](../code-quality/ca1038-enumerators-should-be-strongly-typed.md)

 [CA1039: Listas são fortemente tipadas](../code-quality/ca1039-lists-are-strongly-typed.md)

## <a name="see-also"></a>Consulte Também
 <xref:System.Array?displayProperty=fullName> <xref:System.Collections.IEnumerable?displayProperty=fullName>
 <xref:System.Collections.ICollection?displayProperty=fullName>
 <xref:System.Object?displayProperty=fullName>
