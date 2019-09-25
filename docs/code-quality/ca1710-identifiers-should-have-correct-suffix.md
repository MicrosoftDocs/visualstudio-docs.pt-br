---
title: 'CA1710: Identificadores devem ter um sufixo correto'
ms.date: 03/11/2019
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 50c67c614c4ece8f1925f4133f749a1c5747fe31
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71234163"
---
# <a name="ca1710-identifiers-should-have-correct-suffix"></a>CA1710: Identificadores devem ter um sufixo correto

|||
|-|-|
|NomeDoTipo|IdentifiersShouldHaveCorrectSuffix|
|CheckId|CA1710|
|Categoria|Microsoft.Naming|
|Alteração significativa|Quebra|

## <a name="cause"></a>Causa

Um identificador não tem o sufixo correto.

Por padrão, essa regra só examina identificadores visíveis externamente, mas isso é [configurável](#configurability).

## <a name="rule-description"></a>Descrição da regra

Por convenção, os nomes de tipos que estendem determinados tipos de base ou que implementam determinadas interfaces, ou tipos derivados desses tipos, têm um sufixo associado ao tipo ou interface base.

As convenções de nomenclatura fornecem uma aparência comum para as bibliotecas direcionadas ao Common Language Runtime. Isso reduz a curva de aprendizado necessária para novas bibliotecas de software e aumenta a confiança do cliente de que a biblioteca foi desenvolvida por alguém que tenha experiência no desenvolvimento de código gerenciado.

A tabela a seguir lista os tipos de base e as interfaces que têm sufixos associados.

|Tipo/interface base|Sufixo|
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

Os tipos que <xref:System.Collections.ICollection> implementam e são um tipo generalizado de estrutura de dados, como um dicionário, uma pilha ou uma fila, são nomes permitidos que fornecem informações significativas sobre o uso pretendido do tipo.

Os tipos que <xref:System.Collections.ICollection> implementam e são uma coleção de itens específicos têm nomes que terminam com a palavra ' Collection '. Por exemplo, uma coleção de <xref:System.Collections.Queue> objetos teria o nome ' QueueCollection '. O sufixo ' Collection ' significa que os membros da coleção podem ser enumerados usando a `foreach` instrução (`For Each` in [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]).

Os tipos que <xref:System.Collections.IDictionary> implementam têm nomes que terminam com a palavra ' Dictionary ', mesmo que <xref:System.Collections.IEnumerable> o <xref:System.Collections.ICollection>tipo também implemente ou. As convenções de nomenclatura de sufixo ' Collection ' e ' Dictionary ' permitem que os usuários diferenciem entre os dois padrões de enumeração a seguir.

Os tipos com o sufixo ' Collection ' seguem esse padrão de enumeração.

```
foreach(SomeType x in SomeCollection) { }
```

Os tipos com o sufixo ' Dictionary ' seguem esse padrão de enumeração.

```
foreach(SomeType x in SomeDictionary.Values) { }
```

Um <xref:System.Data.DataSet> objeto consiste em uma coleção de <xref:System.Data.DataTable> objetos, <xref:System.Data.DataColumn?displayProperty=fullName> que consistem em coleções e <xref:System.Data.DataRow?displayProperty=fullName> objetos, entre outros. Essas coleções implementam <xref:System.Collections.ICollection> por meio <xref:System.Data.InternalDataCollectionBase?displayProperty=fullName> da classe base.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Renomeie o tipo para que ele seja sufixado com o termo correto.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

É seguro suprimir um aviso para usar o sufixo ' Collection ' se o tipo for uma estrutura de dados generalizada que pode ser estendida ou que conterá um conjunto arbitrário de itens diferentes. Nesse caso, um nome que fornece informações significativas sobre a implementação, o desempenho ou outras características da estrutura de dados pode fazer sentido (por exemplo, BinaryTree). Nos casos em que o tipo representa uma coleção de um tipo específico (por exemplo, StringCollection), não omita um aviso dessa regra porque o sufixo indica que o tipo pode ser enumerado usando uma `foreach` instrução.

Para outros sufixos, não omita um aviso dessa regra. O sufixo permite que o uso pretendido seja evidente a partir do nome do tipo.

## <a name="configurability"></a>Configurabilidade

Se você estiver executando essa regra por meio de [analisadores do FxCop](install-fxcop-analyzers.md) (e não com a análise herdada), poderá configurar em quais partes de sua base de código executar essa regra, com base em sua acessibilidade. Por exemplo, para especificar que a regra deve ser executada somente na superfície da API não pública, adicione o seguinte par chave-valor a um arquivo. editorconfig em seu projeto:

```ini
dotnet_code_quality.ca1710.api_surface = private, internal
```

Você pode configurar essa opção apenas para essa regra, para todas as regras ou para todas as regras nesta categoria (nomenclatura). Para obter mais informações, consulte [Configurar analisadores de FxCop](configure-fxcop-analyzers.md).

## <a name="related-rules"></a>Regras relacionadas

[CA1711: Os identificadores não devem ter um sufixo incorreto](../code-quality/ca1711-identifiers-should-not-have-incorrect-suffix.md)

## <a name="see-also"></a>Consulte também

- [Atributos](/dotnet/standard/design-guidelines/attributes)
- [Manipulando e gerando eventos](/dotnet/standard/events/index)