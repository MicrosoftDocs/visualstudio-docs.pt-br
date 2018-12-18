---
title: 'CA1710: Os identificadores devem ter sufixo correto | Microsoft Docs'
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
- CA1710
- IdentifiersShouldHaveCorrectSuffix
helpviewer_keywords:
- IdentifiersShouldHaveCorrectSuffix
- CA1710
ms.assetid: 2b8e6dce-b4e8-4a66-ba9a-6b79be5bfe8c
caps.latest.revision: 22
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 2256e3f20dfdb4ddb8efa28d7ecdd203a139bcc5
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49940158"
---
# <a name="ca1710-identifiers-should-have-correct-suffix"></a>CA1710: os identificadores devem ter o sufixo correto
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|IdentifiersShouldHaveCorrectSuffix|
|CheckId|CA1710|
|Categoria|Microsoft.Naming|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um identificador não tem o sufixo correto.

## <a name="rule-description"></a>Descrição da Regra
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

 Tipos que implementam <xref:System.Collections.ICollection> e são uma coleção de itens específicos têm nomes que terminam com a palavra 'Collection'. Por exemplo, uma coleção de <xref:System.Collections.Queue> objetos tem o nome 'QueueCollection'. O sufixo 'Collection' significa que os membros da coleção podem ser enumerados usando o `foreach` (`For Each` em [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) instrução.

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

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Renomear o tipo, de modo que ele é sufixado com o termo correto.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso para usar o sufixo 'Collection' se o tipo é uma estrutura de dados generalizado que pode ser estendida ou que conterá um conjunto arbitrário de diversos itens. Nesse caso, um nome que forneça informações significativas sobre a implementação, desempenho ou outras características da estrutura de dados pode fazer sentido (por exemplo, BinaryTree). Em casos em que o tipo representa uma coleção de um tipo específico (por exemplo, StringCollection), não suprima um aviso nessa regra porque o sufixo indica que o tipo pode ser enumerado usando um `foreach` instrução.

 Para outros sufixos, não suprima um aviso nessa regra. O sufixo permite que o uso pretendido seja evidente, o nome de tipo.

## <a name="related-rules"></a>Regras relacionadas
 [CA1711: os identificadores não devem ter sufixo incorreto](../code-quality/ca1711-identifiers-should-not-have-incorrect-suffix.md)

## <a name="see-also"></a>Consulte também
 [Atributos](http://msdn.microsoft.com/library/ee0038ef-b247-4747-a650-3c5c5cd58d8b) [NIB: delegados e eventos](http://msdn.microsoft.com/en-us/d98fd58b-fa4f-4598-8378-addf4355a115)



