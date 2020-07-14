---
title: 'CA2227: as propriedades da coleção devem ser somente leitura | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2227
- CollectionPropertiesShouldBeReadOnly
helpviewer_keywords:
- CA2227
- CollectionPropertiesShouldBeReadOnly
ms.assetid: 26967aaf-6fbe-438a-b4d3-ac579b5dc0f9
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 17c4e2336a5c8bd8905d857dc8189a11f9fb6181
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540524"
---
# <a name="ca2227-collection-properties-should-be-read-only"></a>CA2227: Propriedades de coleção devem ser somente leitura
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|CollectionPropertiesShouldBeReadOnly|
|CheckId|CA2227|
|Categoria|Microsoft. Usage|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Uma propriedade gravável externamente visível é um tipo que implementa <xref:System.Collections.ICollection?displayProperty=fullName> . Matrizes, indexadores (Propriedades com o nome ' item ') e conjuntos de permissões são ignorados pela regra.

## <a name="rule-description"></a>Descrição da Regra
 Uma propriedade de coleção gravável permite que um usuário substitua a coleção por uma coleção completamente diferente. Uma propriedade somente leitura evita que a coleção seja substituída, mas ainda permite que membros individuais sejam definidos. Se a substituição da coleção for uma meta, o padrão de design preferencial será incluir um método para remover todos os elementos da coleção e um método para preencher novamente a coleção. Consulte os <xref:System.Collections.ArrayList.Clear%2A> <xref:System.Collections.ArrayList.AddRange%2A> métodos e da <xref:System.Collections.ArrayList?displayProperty=fullName> classe para obter um exemplo desse padrão.

 A serialização binária e XML dão suporte a propriedades somente leitura que são coleções. A <xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName> classe tem requisitos específicos para tipos que implementam <xref:System.Collections.ICollection> e <xref:System.Collections.IEnumerable?displayProperty=fullName> para serem serializáveis.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, torne a propriedade somente leitura e, se o design exigir, adicione métodos para limpar e preencher novamente a coleção.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo com uma propriedade de coleção gravável e mostra como a coleção pode ser substituída diretamente. Além disso, a maneira preferida de substituir uma propriedade de coleção somente leitura usando os `Clear` `AddRange` métodos e é mostrada.

 [!code-cpp[FxCop.Usage.PropertiesReturningCollections#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.PropertiesReturningCollections/cpp/FxCop.Usage.PropertiesReturningCollections.cpp#1)]
 [!code-csharp[FxCop.Usage.PropertiesReturningCollections#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.PropertiesReturningCollections/cs/FxCop.Usage.PropertiesReturningCollections.cs#1)]
 [!code-vb[FxCop.Usage.PropertiesReturningCollections#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.PropertiesReturningCollections/vb/FxCop.Usage.PropertiesReturningCollections.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1819: Propriedades não devem retornar matrizes](../code-quality/ca1819-properties-should-not-return-arrays.md)
