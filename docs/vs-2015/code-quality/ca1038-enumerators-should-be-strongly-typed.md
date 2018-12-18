---
title: 'CA1038: Os enumeradores devem ser fortemente tipados | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- EnumeratorsShouldBeStronglyTyped
- CA1038
helpviewer_keywords:
- EnumeratorsShouldBeStronglyTyped
- CA1038
ms.assetid: 8919f526-d487-42a4-87dc-2b2ee25260c4
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: aafd89a068a57ef1eb89584441195e1ece8b8f52
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49899065"
---
# <a name="ca1038-enumerators-should-be-strongly-typed"></a>CA1038: os enumeradores devem ser fortemente tipados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|EnumeratorsShouldBeStronglyTyped|
|CheckId|CA1038|
|Categoria|Microsoft.Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público ou protegido implementa <xref:System.Collections.IEnumerator?displayProperty=fullName> , mas não fornece uma versão fortemente tipada do <xref:System.Collections.IEnumerator.Current%2A?displayProperty=fullName> propriedade. Tipos que são derivados dos seguintes tipos são isentos dessa regra:

-   <xref:System.Collections.CollectionBase?displayProperty=fullName>

-   <xref:System.Collections.DictionaryBase?displayProperty=fullName>

-   <xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName>

## <a name="rule-description"></a>Descrição da Regra
 Essa regra exige <xref:System.Collections.IEnumerator> implementações também forneçam uma versão fortemente tipada do <xref:System.Collections.IEnumerator.Current%2A> propriedade para que os usuários não sejam obrigados a converter o valor de retorno para o tipo forte quando usarem a funcionalidade fornecida pela interface. Esta regra pressupõe que o tipo que implementa <xref:System.Collections.IEnumerator> contém uma coleção de instâncias de um tipo que é mais forte que <xref:System.Object>.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, implemente a propriedade de interface explicitamente (declare-o como `IEnumerator.Current`). Adicionar uma versão pública fortemente tipada da propriedade, declarada como `Current`, e retornará um objeto fortemente tipado.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Suprima um aviso nessa regra ao implementar um enumerador baseado em objeto para uso com uma coleção baseada em objeto, como uma árvore binária. Tipos que estendem a nova coleção serão definir o enumerador com rigidez de tipos e expor a propriedade com rigidez de tipos.

## <a name="example"></a>Exemplo
 O exemplo a seguir demonstra a maneira correta de implementar fortemente tipado <xref:System.Collections.IEnumerator> tipo.

 [!code-csharp[FxCop.Design.IEnumeratorStrongTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.IEnumeratorStrongTypes/cs/FxCop.Design.IEnumeratorStrongTypes.cs#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1035: as implementações de ICollection têm membros fortemente tipados](../code-quality/ca1035-icollection-implementations-have-strongly-typed-members.md)

 [CA1039: as listas são fortemente tipadas](../code-quality/ca1039-lists-are-strongly-typed.md)

## <a name="see-also"></a>Consulte também
 <xref:System.Collections.IEnumerator?displayProperty=fullName> <xref:System.Collections.CollectionBase?displayProperty=fullName>
 <xref:System.Collections.DictionaryBase?displayProperty=fullName>
 <xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName>



