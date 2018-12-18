---
title: 'CA1058: Os tipos não devem estender determinados tipos de base | Microsoft Docs'
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
- TypesShouldNotExtendCertainBaseTypes
- CA1058
helpviewer_keywords:
- CA1058
- TypesShouldNotExtendCertainBaseTypes
ms.assetid: 8446ee40-beb1-49fa-8733-4d8e813471c0
caps.latest.revision: 26
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 0a4ffbe3b359f2c58f8e301b9176981a2037c17f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49912429"
---
# <a name="ca1058-types-should-not-extend-certain-base-types"></a>CA1058: os tipos não devem estender determinados tipos base
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|TypesShouldNotExtendCertainBaseTypes|
|CheckId|CA1058|
|Categoria|Microsoft.Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo visível externamente estende determinados tipos de base. No momento, esta regra relata tipos que derivam de tipos a seguir:

-   <xref:System.ApplicationException?displayProperty=fullName>

-   <xref:System.Xml.XmlDocument?displayProperty=fullName>

-   <xref:System.Collections.CollectionBase?displayProperty=fullName>

-   <xref:System.Collections.DictionaryBase?displayProperty=fullName>

-   <xref:System.Collections.Queue?displayProperty=fullName>

-   <xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName>

-   <xref:System.Collections.SortedList?displayProperty=fullName>

-   <xref:System.Collections.Stack?displayProperty=fullName>

## <a name="rule-description"></a>Descrição da Regra
 Para [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] versão 1, era recomendável para derivar novas exceções de <xref:System.ApplicationException>. A recomendação foi alterada e novas exceções devem derivar <xref:System.Exception?displayProperty=fullName> ou uma de suas subclasses no <xref:System> namespace.

 Não crie uma subclasse de <xref:System.Xml.XmlDocument> se você deseja criar uma exibição XML de uma fonte de dados ou modelo de objeto subjacente.

### <a name="non-generic-collections"></a>Coleções não genéricas
 Usar e/ou estender coleções genéricas, sempre que possível. Não estenda coleções não genéricas no seu código, a menos que você o enviados anteriormente.

 **Exemplos de uso incorreto**

```csharp
public class MyCollection : CollectionBase
{
}

public class MyReadOnlyCollection : ReadOnlyCollectionBase
{
}
```

 **Exemplos de uso correto**

```csharp
public class MyCollection : Collection<T>
{
}

public class MyReadOnlyCollection : ReadOnlyCollection<T>
{
}
```

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, derive o tipo de um tipo base diferente ou uma coleção genérica.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprimir um aviso nessa regra quanto a violações sobre <xref:System.ApplicationException>. É seguro suprimir um aviso nessa regra quanto a violações sobre <xref:System.Xml.XmlDocument>. É seguro suprimir um aviso sobre uma coleção não genéricas se o código foi lançado anteriormente.



