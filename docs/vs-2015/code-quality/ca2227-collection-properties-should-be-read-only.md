---
title: 'CA2227: Propriedades de coleção devem ser somente leitura | Microsoft Docs'
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
- CA2227
- CollectionPropertiesShouldBeReadOnly
helpviewer_keywords:
- CA2227
- CollectionPropertiesShouldBeReadOnly
ms.assetid: 26967aaf-6fbe-438a-b4d3-ac579b5dc0f9
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 1db0ab6bae6a374726e953e505247896864c7f0d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49830438"
---
# <a name="ca2227-collection-properties-should-be-read-only"></a>CA2227: as propriedades de coleção devem ser somente leitura
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|CollectionPropertiesShouldBeReadOnly|
|CheckId|CA2227|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Uma propriedade gravável visível externamente é um tipo que implementa <xref:System.Collections.ICollection?displayProperty=fullName>. Matrizes, indexadores (propriedades com o nome 'Item') e conjuntos de permissões são ignorados pela regra.

## <a name="rule-description"></a>Descrição da Regra
 Uma propriedade collection gravável permite que um usuário substituir a coleção com uma coleção completamente diferente. Uma propriedade somente leitura evita que a coleção seja substituída, mas ainda permite que membros individuais sejam definidos. Se substituir a coleção é uma meta, o padrão de design preferencial é incluir um método para remover todos os elementos da coleção e um método para preencher novamente a coleção. Consulte a <xref:System.Collections.ArrayList.Clear%2A> e <xref:System.Collections.ArrayList.AddRange%2A> métodos do <xref:System.Collections.ArrayList?displayProperty=fullName> classe para obter um exemplo desse padrão.

 Serialização XML e binária dão suporte a propriedades somente leitura que são coleções. O <xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName> classe tem requisitos específicos para os tipos que implementam <xref:System.Collections.ICollection> e <xref:System.Collections.IEnumerable?displayProperty=fullName> para ser serializável.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, verifique a propriedade somente leitura e, se o design exigir, adicione métodos para limpar e popule novamente a coleção.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo com uma propriedade collection gravável e mostra como a coleção pode ser substituída diretamente. Além disso, a maneira preferida de substituição de uma propriedade de coleção somente leitura usando `Clear` e `AddRange` métodos é mostrado.

 [!code-cpp[FxCop.Usage.PropertiesReturningCollections#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.PropertiesReturningCollections/cpp/FxCop.Usage.PropertiesReturningCollections.cpp#1)]
 [!code-csharp[FxCop.Usage.PropertiesReturningCollections#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.PropertiesReturningCollections/cs/FxCop.Usage.PropertiesReturningCollections.cs#1)]
 [!code-vb[FxCop.Usage.PropertiesReturningCollections#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.PropertiesReturningCollections/vb/FxCop.Usage.PropertiesReturningCollections.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1819: as propriedades não devem retornar matrizes](../code-quality/ca1819-properties-should-not-return-arrays.md)



