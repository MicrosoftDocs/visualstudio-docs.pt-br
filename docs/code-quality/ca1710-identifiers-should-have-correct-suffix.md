---
title: 'CA1710: os identificadores devem ter o sufixo correto'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1710
- IdentifiersShouldHaveCorrectSuffix
helpviewer_keywords:
- IdentifiersShouldHaveCorrectSuffix
- CA1710
ms.assetid: 2b8e6dce-b4e8-4a66-ba9a-6b79be5bfe8c
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 263870511715757c8771b0b596e443d82be91525
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45549862"
---
# <a name="ca1710-identifiers-should-have-correct-suffix"></a>CA1710: os identificadores devem ter o sufixo correto

|||
|-|-|
|NomeDoTipo|IdentifiersShouldHaveCorrectSuffix|
|CheckId|CA1710|
|Categoria|Microsoft.Naming|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa

Um identificador não tem o sufixo correto.

## <a name="rule-description"></a>Descrição da regra

Por convenção, os nomes de tipos que estendem determinados tipos de base ou que implementam determinadas interfaces, ou tipos derivados desses tipos, têm um sufixo que está associado com o tipo base ou interface.

Convenções de nomenclatura de fornecem uma aparência comum para bibliotecas que direcionam o common language runtime. Isso reduz a curva de aprendizado que é necessário para novas bibliotecas de software e aumenta a confiança do cliente que a biblioteca foi desenvolvida por alguém que tenha experiência em desenvolvimento de código gerenciado.

A tabela a seguir lista os tipos base e interfaces que associaram sufixos.

|Tipo/Interface base|Sufixo|
|--------------------------|------------|
|<xref:System.Attribute?displayProperty=fullName>|Atributo|
|<xref:System.EventArgs?displayProperty=fullName>|EventArgs|
|<xref:System.Exception?displayProperty=fullName>|Exceção|
|<xref:System.Collections.ICollection?displayProperty=fullName>|Coleção|
|<xref:System.Collections.IDictionary?displayProperty=fullName>|Dicionário|
|<xref:System.Collections.IEnumerable?displayProperty=fullName>|Coleção|
|<xref:System.Collections.Queue?displayProperty=fullName>|Coleção ou fila|
|<xref:System.Collections.Stack?displayProperty=fullName>|Coleção ou pilha|
|<xref:System.Collections.Generic.ICollection%601?displayProperty=fullName>|Coleção|
|<xref:System.Collections.Generic.IDictionary%602?displayProperty=fullName>|Dicionário|
|<xref:System.Data.DataSet?displayProperty=fullName>|DataSet|
|<xref:System.Data.DataTable?displayProperty=fullName>|Coleção ou DataTable|
|<xref:System.IO.Stream?displayProperty=fullName>|Fluxo|
|<xref:System.Security.IPermission?displayProperty=fullName>|Permissão|
|<xref:System.Security.Policy.IMembershipCondition?displayProperty=fullName>|Condição|
|Um delegado de manipulador de eventos.|EventHandler|

Tipos que implementam <xref:System.Collections.ICollection> e são um tipo generalizado da estrutura de dados, como um dicionário, pilha ou fila, são permitidos nomes que fornecem informações significativas sobre o uso pretendido do tipo.

Tipos que implementam <xref:System.Collections.ICollection> e são uma coleção de itens específicos têm nomes que terminam com a palavra 'Collection'. Por exemplo, uma coleção de <xref:System.Collections.Queue> objetos tem o nome 'QueueCollection'. O sufixo 'Collection' significa que os membros da coleção podem ser enumerados usando o `foreach` (`For Each` em [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]) instrução.

Tipos que implementam <xref:System.Collections.IDictionary> têm nomes que terminam com a palavra 'Dicionário', mesmo se o tipo também implementa <xref:System.Collections.IEnumerable> ou <xref:System.Collections.ICollection>. As convenções de nomenclatura de sufixo 'Collection' e 'Dicionário' permitem que os usuários distinguir entre os seguintes padrões de enumeração de dois.

Tipos com o sufixo 'Collection' seguem esse padrão de enumeração.

```
foreach(SomeType x in SomeCollection) { }
```

Tipos com o sufixo 'Dicionário' seguem esse padrão de enumeração.

```
foreach(SomeType x in SomeDictionary.Values) { }
```

Um <xref:System.Data.DataSet> objeto consiste em uma coleção de <xref:System.Data.DataTable> objetos, que consistem em coleções de <xref:System.Data.DataColumn?displayProperty=fullName> e <xref:System.Data.DataRow?displayProperty=fullName> objects, entre outros. Essas coleções implementam <xref:System.Collections.ICollection> por meio de base de <xref:System.Data.InternalDataCollectionBase?displayProperty=fullName> classe.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Renomear o tipo, de modo que ele é sufixado com o termo correto.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

É seguro suprimir um aviso para usar o sufixo 'Collection' se o tipo é uma estrutura de dados generalizado que pode ser estendida ou que conterá um conjunto arbitrário de diversos itens. Nesse caso, um nome que forneça informações significativas sobre a implementação, desempenho ou outras características da estrutura de dados pode fazer sentido (por exemplo, BinaryTree). Em casos em que o tipo representa uma coleção de um tipo específico (por exemplo, StringCollection), não suprima um aviso nessa regra porque o sufixo indica que o tipo pode ser enumerado usando um `foreach` instrução.

Para outros sufixos, não suprima um aviso nessa regra. O sufixo permite que o uso pretendido seja evidente, o nome de tipo.

## <a name="related-rules"></a>Regras relacionadas

[CA1711: os identificadores não devem ter sufixo incorreto](../code-quality/ca1711-identifiers-should-not-have-incorrect-suffix.md)

## <a name="see-also"></a>Consulte também

- [Atributos](/dotnet/standard/design-guidelines/attributes)
- [Manipulando e acionando eventos](/dotnet/standard/events/index)