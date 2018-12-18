---
title: 'CA1038: os enumeradores devem ser fortemente tipados'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- EnumeratorsShouldBeStronglyTyped
- CA1038
helpviewer_keywords:
- EnumeratorsShouldBeStronglyTyped
- CA1038
ms.assetid: 8919f526-d487-42a4-87dc-2b2ee25260c4
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 22cc84a0cdc8d4fdb86f6890ae0ebd25eb65beb8
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45545483"
---
# <a name="ca1038-enumerators-should-be-strongly-typed"></a>CA1038: os enumeradores devem ser fortemente tipados

|||
|-|-|
|NomeDoTipo|EnumeratorsShouldBeStronglyTyped|
|CheckId|CA1038|
|Categoria|Microsoft.Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público ou protegido implementa <xref:System.Collections.IEnumerator?displayProperty=fullName> , mas não fornece uma versão fortemente tipada do <xref:System.Collections.IEnumerator.Current%2A?displayProperty=fullName> propriedade. Tipos que são derivados dos seguintes tipos são isentos dessa regra:

- <xref:System.Collections.CollectionBase?displayProperty=fullName>

- <xref:System.Collections.DictionaryBase?displayProperty=fullName>

- <xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName>

## <a name="rule-description"></a>Descrição da regra
 Essa regra exige <xref:System.Collections.IEnumerator> implementações também forneçam uma versão fortemente tipada do <xref:System.Collections.IEnumerator.Current%2A> propriedade para que os usuários não sejam obrigados a converter o valor de retorno para o tipo forte quando usarem a funcionalidade fornecida pela interface. Esta regra pressupõe que o tipo que implementa <xref:System.Collections.IEnumerator> contém uma coleção de instâncias de um tipo que é mais forte que <xref:System.Object>.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, implemente a propriedade de interface explicitamente (declare-o como `IEnumerator.Current`). Adicionar uma versão pública fortemente tipada da propriedade, declarada como `Current`, e retornará um objeto fortemente tipado.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Suprima um aviso nessa regra ao implementar um enumerador baseado em objeto para uso com uma coleção baseada em objeto, como uma árvore binária. Tipos que estendem a nova coleção serão definir o enumerador com rigidez de tipos e expor a propriedade com rigidez de tipos.

## <a name="example"></a>Exemplo
 O exemplo a seguir demonstra a maneira correta de implementar fortemente tipado <xref:System.Collections.IEnumerator> tipo.

 [!code-csharp[FxCop.Design.IEnumeratorStrongTypes#1](../code-quality/codesnippet/CSharp/ca1038-enumerators-should-be-strongly-typed_1.cs)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1035: as implementações de ICollection têm membros fortemente tipados](../code-quality/ca1035-icollection-implementations-have-strongly-typed-members.md)

 [CA1039: as listas são fortemente tipadas](../code-quality/ca1039-lists-are-strongly-typed.md)

## <a name="see-also"></a>Consulte também

- <xref:System.Collections.IEnumerator?displayProperty=fullName>
- <xref:System.Collections.CollectionBase?displayProperty=fullName>
- <xref:System.Collections.DictionaryBase?displayProperty=fullName>
- <xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName>