---
title: 'CA1035: As implementações de ICollection têm membros fortemente tipados | Microsoft Docs'
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
- ICollectionImplementationsHaveStronglyTypedMembers
- CA1035
helpviewer_keywords:
- CA1035
- ICollectionImplementationsHaveStronglyTypedMembers
ms.assetid: ad404eb5-cf6a-44b7-b78a-8ebfb654bc7f
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: c5a20352b92c5cf4089029d9b613fdf8a83a8c2e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49930148"
---
# <a name="ca1035-icollection-implementations-have-strongly-typed-members"></a>CA1035: as implementações de ICollection têm membros fortemente tipados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|ICollectionImplementationsHaveStronglyTypedMembers|
|CheckId|CA1035|
|Categoria|Microsoft.Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público ou protegido implementa <xref:System.Collections.ICollection?displayProperty=fullName> , mas não fornece um método com rigidez de tipos para <xref:System.Collections.ICollection.CopyTo%2A?displayProperty=fullName>. A versão fortemente tipada da <xref:System.Collections.ICollection.CopyTo%2A> deve aceitar dois parâmetros e não pode ter um <xref:System.Array?displayProperty=fullName> ou uma matriz de <xref:System.Object?displayProperty=fullName> como seu primeiro parâmetro.

## <a name="rule-description"></a>Descrição da Regra
 Essa regra exige <xref:System.Collections.ICollection> implementações para fornecer fortemente tipados membros para que os usuários não sejam obrigados a converter argumentos para o <xref:System.Object> de tipo quando usarem a funcionalidade fornecida pela interface. Esta regra pressupõe que o tipo que implementa <xref:System.Collections.ICollection> faz então, para gerenciar uma coleção de instâncias de um tipo que é mais forte que <xref:System.Object>.

 <xref:System.Collections.ICollection> implementa a interface <xref:System.Collections.IEnumerable?displayProperty=fullName>. Se os objetos na coleção estendem <xref:System.ValueType?displayProperty=fullName>, você deve fornecer um membro com rigidez de tipos para <xref:System.Collections.IEnumerable.GetEnumerator%2A> para evitar a diminuição no desempenho causado pela conversão boxing. Isso não é necessário quando os objetos da coleção são um tipo de referência.

 Para implementar uma versão fortemente tipada de um membro de interface, implementar os membros de interface explicitamente por meio de nomes no formato `InterfaceName.InterfaceMemberName`, tais como <xref:System.Collections.ICollection.CopyTo%2A>. Os membros de interface explícita usam os tipos de dados que são declarados pela interface. Implementar os membros fortemente tipados usando o nome do membro de interface, como <xref:System.Collections.ICollection.CopyTo%2A>. Declarar os membros fortemente tipados como público e declarar parâmetros e retornar valores para ser do tipo forte que é gerenciado pela coleção. Os tipos fortes substituir tipos mais fracos, como <xref:System.Object> e <xref:System.Array> que são declaradas pela interface.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, implemente o membro de interface explicitamente (declare-o como <xref:System.Collections.ICollection.CopyTo%2A>). Adicionar o membro com rigidez de tipos público, declarado como `CopyTo`, e fazê-lo a levar a uma matriz fortemente tipada como seu primeiro parâmetro.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Suprima um aviso nessa regra, se você implementar uma nova coleção baseada em objeto, como uma árvore binária, onde tipos que estendem a nova coleção de determinam o tipo forte. Esses tipos devem estar em conformidade com essa regra e expor os membros fortemente tipados.

## <a name="example"></a>Exemplo
 O exemplo a seguir demonstra a maneira correta de implementar <xref:System.Collections.ICollection>.

 [!code-csharp[FxCop.Design.ICollectionStrongTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ICollectionStrongTypes/cs/FxCop.Design.ICollectionStrongTypes.cs#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1038: os enumeradores devem ser fortemente tipados](../code-quality/ca1038-enumerators-should-be-strongly-typed.md)

 [CA1039: as listas são fortemente tipadas](../code-quality/ca1039-lists-are-strongly-typed.md)

## <a name="see-also"></a>Consulte também
 <xref:System.Array?displayProperty=fullName> <xref:System.Collections.IEnumerable?displayProperty=fullName>
 <xref:System.Collections.ICollection?displayProperty=fullName>
 <xref:System.Object?displayProperty=fullName>



