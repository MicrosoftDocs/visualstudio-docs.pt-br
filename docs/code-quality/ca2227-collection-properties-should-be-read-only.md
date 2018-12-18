---
title: 'CA2227: as propriedades de coleção devem ser somente leitura'
ms.date: 09/28/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2227
- CollectionPropertiesShouldBeReadOnly
helpviewer_keywords:
- CA2227
- CollectionPropertiesShouldBeReadOnly
ms.assetid: 26967aaf-6fbe-438a-b4d3-ac579b5dc0f9
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
- CPP
ms.workload:
- multiple
ms.openlocfilehash: f1bbd3e6ba97d969694e7d2142978c12552b3c50
ms.sourcegitcommit: ad5fb20f18b23eb8bd2568717f61edc6b7eee5e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47860245"
---
# <a name="ca2227-collection-properties-should-be-read-only"></a>CA2227: as propriedades de coleção devem ser somente leitura

|||
|-|-|
|NomeDoTipo|CollectionPropertiesShouldBeReadOnly|
|CheckId|CA2227|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa

Uma propriedade visível externamente de gravável é de um tipo que implementa <xref:System.Collections.ICollection?displayProperty=fullName>. Essa regra ignora matrizes, indexadores (propriedades com o nome 'Item') e conjuntos de permissões.

## <a name="rule-description"></a>Descrição da regra

Uma propriedade collection gravável permite que um usuário substituir a coleção com uma coleção completamente diferente. Uma propriedade somente leitura interrompe a coleção seja substituída, mas ainda permite que os membros individuais a ser definido. Se substituir a coleção é uma meta, o padrão de design preferencial é incluir um método para remover todos os elementos da coleção e um método para preencher novamente a coleção. Consulte a <xref:System.Collections.ArrayList.Clear%2A> e <xref:System.Collections.ArrayList.AddRange%2A> métodos do <xref:System.Collections.ArrayList?displayProperty=fullName> classe para obter um exemplo desse padrão.

Serialização XML e binária dão suporte a propriedades somente leitura que são coleções. O <xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName> classe tem requisitos específicos para os tipos que implementam <xref:System.Collections.ICollection> e <xref:System.Collections.IEnumerable?displayProperty=fullName> para ser serializável.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra, verifique a propriedade somente leitura. Se o design exigir, adicione métodos para limpar e preencher novamente a coleção.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Você pode suprimir o aviso se a propriedade for parte de um [o objeto de transferência de dados (DTO)](/previous-versions/msp-n-p/ff649585(v=pandp.10)) classe.

Caso contrário, não suprima avisos dessa regra.

## <a name="example"></a>Exemplo

O exemplo a seguir mostra um tipo com uma propriedade collection gravável e mostra como a coleção pode ser substituída diretamente. Além disso, ele mostra a maneira preferida de substituição de uma propriedade de coleção somente leitura usando `Clear` e `AddRange` métodos.

[!code-csharp[FxCop.Usage.PropertiesReturningCollections#1](../code-quality/codesnippet/CSharp/ca2227-collection-properties-should-be-read-only_1.cs)]
[!code-vb[FxCop.Usage.PropertiesReturningCollections#1](../code-quality/codesnippet/VisualBasic/ca2227-collection-properties-should-be-read-only_1.vb)]
[!code-cpp[FxCop.Usage.PropertiesReturningCollections#1](../code-quality/codesnippet/CPP/ca2227-collection-properties-should-be-read-only_1.cpp)]

## <a name="related-rules"></a>Regras relacionadas

- [CA1819: as propriedades não devem retornar matrizes](../code-quality/ca1819-properties-should-not-return-arrays.md)