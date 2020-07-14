---
title: 'CA1038: enumeradores devem ser fortemente tipados | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- EnumeratorsShouldBeStronglyTyped
- CA1038
helpviewer_keywords:
- EnumeratorsShouldBeStronglyTyped
- CA1038
ms.assetid: 8919f526-d487-42a4-87dc-2b2ee25260c4
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: e660b1af58dca8d0d69ce2844076382c4a5a1f12
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548259"
---
# <a name="ca1038-enumerators-should-be-strongly-typed"></a>CA1038: Enumeradores devem ser fortemente tipados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|EnumeratorsShouldBeStronglyTyped|
|CheckId|CA1038|
|Categoria|Microsoft. Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público ou protegido implementa <xref:System.Collections.IEnumerator?displayProperty=fullName> , mas não fornece uma versão fortemente tipada da <xref:System.Collections.IEnumerator.Current%2A?displayProperty=fullName> propriedade. Tipos que são derivados dos seguintes tipos são isentos desta regra:

- <xref:System.Collections.CollectionBase?displayProperty=fullName>

- <xref:System.Collections.DictionaryBase?displayProperty=fullName>

- <xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName>

## <a name="rule-description"></a>Descrição da Regra
 Essa regra requer <xref:System.Collections.IEnumerator> implementações para também fornecer uma versão fortemente tipada da <xref:System.Collections.IEnumerator.Current%2A> propriedade para que os usuários não precisem converter o valor de retorno para o tipo forte ao usarem a funcionalidade fornecida pela interface. Essa regra pressupõe que o tipo que implementa <xref:System.Collections.IEnumerator> contém uma coleção de instâncias de um tipo que é mais forte que <xref:System.Object> .

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, implemente a propriedade de interface explicitamente (declare-a como `IEnumerator.Current` ). Adicione uma versão pública com rigidez de tipos da propriedade, declarada como `Current` e faça com que ela retorne um objeto fortemente tipado.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Suprimir um aviso desta regra ao implementar um enumerador baseado em objeto para uso com uma coleção baseada em objeto, como uma árvore binária. Os tipos que estendem a nova coleção definirão o enumerador fortemente tipado e exporão a propriedade fortemente tipada.

## <a name="example"></a>Exemplo
 O exemplo a seguir demonstra a maneira correta de implementar um tipo fortemente tipado <xref:System.Collections.IEnumerator> .

 [!code-csharp[FxCop.Design.IEnumeratorStrongTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.IEnumeratorStrongTypes/cs/FxCop.Design.IEnumeratorStrongTypes.cs#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1035: Implementações ICollection têm membros fortemente tipados](../code-quality/ca1035-icollection-implementations-have-strongly-typed-members.md)

 [CA1039: Listas são fortemente tipadas](../code-quality/ca1039-lists-are-strongly-typed.md)

## <a name="see-also"></a>Consulte Também
 <xref:System.Collections.IEnumerator?displayProperty=fullName> <xref:System.Collections.CollectionBase?displayProperty=fullName>
 <xref:System.Collections.DictionaryBase?displayProperty=fullName>
 <xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName>
