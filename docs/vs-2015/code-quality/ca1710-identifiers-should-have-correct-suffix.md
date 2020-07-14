---
title: 'CA1710: os identificadores devem ter o sufixo correto | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1710
- IdentifiersShouldHaveCorrectSuffix
helpviewer_keywords:
- IdentifiersShouldHaveCorrectSuffix
- CA1710
ms.assetid: 2b8e6dce-b4e8-4a66-ba9a-6b79be5bfe8c
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 0ee7ce7c4e9edad9d941b4a70b2a199a37130e43
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543982"
---
# <a name="ca1710-identifiers-should-have-correct-suffix"></a>CA1710: Identificadores devem ter um sufixo correto
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|IdentifiersShouldHaveCorrectSuffix|
|CheckId|CA1710|
|Categoria|Microsoft. Naming|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um identificador não tem o sufixo correto.

## <a name="rule-description"></a>Descrição da Regra
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
|<xref:System.IO.Stream?displayProperty=fullName>|STREAM|
|<xref:System.Security.IPermission?displayProperty=fullName>|Permissão|
|<xref:System.Security.Policy.IMembershipCondition?displayProperty=fullName>|Condição|
|Um delegado de manipulador de eventos.|EventHandler|

 Os tipos que implementam <xref:System.Collections.ICollection> e são um tipo generalizado de estrutura de dados, como um dicionário, uma pilha ou uma fila, são nomes permitidos que fornecem informações significativas sobre o uso pretendido do tipo.

 Os tipos que implementam <xref:System.Collections.ICollection> e são uma coleção de itens específicos têm nomes que terminam com a palavra ' Collection '. Por exemplo, uma coleção de <xref:System.Collections.Queue> objetos teria o nome ' QueueCollection '. O sufixo ' Collection ' significa que os membros da coleção podem ser enumerados usando a `foreach` `For Each` instrução (in [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ).

 Os tipos que implementam <xref:System.Collections.IDictionary> têm nomes que terminam com a palavra ' Dictionary ', mesmo que o tipo também implemente <xref:System.Collections.IEnumerable> ou <xref:System.Collections.ICollection> . As convenções de nomenclatura de sufixo ' Collection ' e ' Dictionary ' permitem que os usuários diferenciem entre os dois padrões de enumeração a seguir.

 Os tipos com o sufixo ' Collection ' seguem esse padrão de enumeração.

```
foreach(SomeType x in SomeCollection) { }
```

 Os tipos com o sufixo ' Dictionary ' seguem esse padrão de enumeração.

```
foreach(SomeType x in SomeDictionary.Values) { }
```

 Um <xref:System.Data.DataSet> objeto consiste em uma coleção de <xref:System.Data.DataTable> objetos, que consistem em coleções <xref:System.Data.DataColumn?displayProperty=fullName> e <xref:System.Data.DataRow?displayProperty=fullName> objetos, entre outros. Essas coleções implementam <xref:System.Collections.ICollection> por meio da <xref:System.Data.InternalDataCollectionBase?displayProperty=fullName> classe base.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Renomeie o tipo para que ele seja sufixado com o termo correto.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso para usar o sufixo ' Collection ' se o tipo for uma estrutura de dados generalizada que pode ser estendida ou que conterá um conjunto arbitrário de itens diferentes. Nesse caso, um nome que fornece informações significativas sobre a implementação, o desempenho ou outras características da estrutura de dados pode fazer sentido (por exemplo, BinaryTree). Nos casos em que o tipo representa uma coleção de um tipo específico (por exemplo, StringCollection), não omita um aviso dessa regra porque o sufixo indica que o tipo pode ser enumerado usando uma `foreach` instrução.

 Para outros sufixos, não omita um aviso dessa regra. O sufixo permite que o uso pretendido seja evidente a partir do nome do tipo.

## <a name="related-rules"></a>Regras relacionadas
 [CA1711: Identificadores não devem ter um sufixo incorreto](../code-quality/ca1711-identifiers-should-not-have-incorrect-suffix.md)

## <a name="see-also"></a>Consulte Também
 [Atributos](https://msdn.microsoft.com/library/ee0038ef-b247-4747-a650-3c5c5cd58d8b) [NIB: eventos e delegados](https://msdn.microsoft.com/d98fd58b-fa4f-4598-8378-addf4355a115)
