---
title: 'CA1039: As listas são fortemente tipadas | Microsoft Docs'
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
- CA1039
- ListsAreStronglyTyped
helpviewer_keywords:
- CA1039
- ListsAreStronglyTyped
ms.assetid: 5ac366c4-fd87-4d5c-95d5-f755510c8e5c
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 681c1ada7600743c0a548f8a774dada6863f7d0d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49853409"
---
# <a name="ca1039-lists-are-strongly-typed"></a>CA1039: as listas são fortemente tipadas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|ListsAreStronglyTyped|
|CheckId|CA1039|
|Categoria|Microsoft.Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Tipo de público ou protegido implementa <xref:System.Collections.IList?displayProperty=fullName> , mas não fornece um método com rigidez de tipos para uma ou mais das seguintes opções:

-   IList.Item

-   IList

-   IList.Contains

-   IList.IndexOf

-   IList.Insert

-   IList.Remove

## <a name="rule-description"></a>Descrição da Regra
 Essa regra exige <xref:System.Collections.IList> implementações para fornecer fortemente tipados membros para que os usuários não sejam obrigados a converter argumentos para o <xref:System.Object?displayProperty=fullName> de tipo quando usarem a funcionalidade fornecida pela interface. O <xref:System.Collections.IList> interface é implementada por coleções de objetos que podem ser acessados por índice. Esta regra pressupõe que o tipo que implementa <xref:System.Collections.IList> faz isso para gerenciar uma coleção de instâncias de um tipo que é mais forte que <xref:System.Object>.

 <xref:System.Collections.IList> implementa o <xref:System.Collections.ICollection?displayProperty=fullName> e <xref:System.Collections.IEnumerable?displayProperty=fullName> interfaces. Se você implementar <xref:System.Collections.IList>, você deve fornecer os membros necessários com rigidez de tipos para <xref:System.Collections.ICollection>. Se os objetos na coleção estendem <xref:System.ValueType?displayProperty=fullName>, você deve fornecer um membro com rigidez de tipos para <xref:System.Collections.IEnumerable.GetEnumerator%2A> para evitar a diminuição no desempenho que é causada pela conversão boxing; isso não é necessário quando os objetos da coleção são um tipo de referência.

 Para estar em conformidade com esta regra, implemente os membros de interface explicitamente por meio de nomes no formato InterfaceName.InterfaceMemberName, tais como <xref:System.Collections.IList.Add%2A>. Os membros de interface explícita usam os tipos de dados que são declarados pela interface. Implementar os membros fortemente tipados usando o nome do membro de interface, como `Add`. Declarar os membros fortemente tipados como público e declarar parâmetros e retornar valores para ser do tipo forte que é gerenciado pela coleção. Os tipos fortes substituir tipos mais fracos, como <xref:System.Object> e <xref:System.Array> que são declaradas pela interface.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, implemente explicitamente <xref:System.Collections.IList> membros e fornecer alternativas com rigidez de tipos para os membros que foram observados anteriormente. Para o código que implementa corretamente o <xref:System.Collections.IList> de interface e fornece a membros fortemente tipados, consulte o exemplo a seguir.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Suprima um aviso nessa regra ao implementar uma nova coleção baseada em objeto, como uma lista vinculada, onde tipos que estendem a nova coleção de determinam o tipo forte. Esses tipos devem estar em conformidade com essa regra e expor os membros fortemente tipados.

## <a name="example"></a>Exemplo
 No exemplo a seguir, o tipo `YourType` estende <xref:System.Collections.CollectionBase?displayProperty=fullName>, assim como todas as coleções com rigidez de tipos. Observe que <xref:System.Collections.CollectionBase> fornece a implementação explícita do <xref:System.Collections.IList> interface para você. Portanto, você deve fornecer somente os membros fortemente tipados <xref:System.Collections.IList> e <xref:System.Collections.ICollection>.

 [!code-csharp[FxCop.Design.IListStrongTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.IListStrongTypes/cs/FxCop.Design.IListStrongTypes.cs#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1035: as implementações de ICollection têm membros fortemente tipados](../code-quality/ca1035-icollection-implementations-have-strongly-typed-members.md)

 [CA1038: os enumeradores devem ser fortemente tipados](../code-quality/ca1038-enumerators-should-be-strongly-typed.md)

## <a name="see-also"></a>Consulte também
 <xref:System.Collections.CollectionBase?displayProperty=fullName> <xref:System.Collections.ICollection?displayProperty=fullName>
 <xref:System.Collections.IEnumerable?displayProperty=fullName>
 <xref:System.Collections.IList?displayProperty=fullName>
 <xref:System.Object?displayProperty=fullName>



