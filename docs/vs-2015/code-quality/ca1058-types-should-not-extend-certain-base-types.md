---
title: 'CA1058: tipos não devem estender determinados tipos base | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- TypesShouldNotExtendCertainBaseTypes
- CA1058
helpviewer_keywords:
- CA1058
- TypesShouldNotExtendCertainBaseTypes
ms.assetid: 8446ee40-beb1-49fa-8733-4d8e813471c0
caps.latest.revision: 26
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: d8e267b1e6203759efc91936a3b13059368a3862
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545386"
---
# <a name="ca1058-types-should-not-extend-certain-base-types"></a>CA1058: Tipos não devem estender determinados tipos base
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|TypesShouldNotExtendCertainBaseTypes|
|CheckId|CA1058|
|Categoria|Microsoft. Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo visível externamente estende determinados tipos de base. Atualmente, essa regra relata os tipos que derivam dos seguintes tipos:

- <xref:System.ApplicationException?displayProperty=fullName>

- <xref:System.Xml.XmlDocument?displayProperty=fullName>

- <xref:System.Collections.CollectionBase?displayProperty=fullName>

- <xref:System.Collections.DictionaryBase?displayProperty=fullName>

- <xref:System.Collections.Queue?displayProperty=fullName>

- <xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName>

- <xref:System.Collections.SortedList?displayProperty=fullName>

- <xref:System.Collections.Stack?displayProperty=fullName>

## <a name="rule-description"></a>Descrição da Regra
 Para [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] a versão 1, era recomendável derivar novas exceções do <xref:System.ApplicationException> . A recomendação foi alterada e as novas exceções devem derivar de <xref:System.Exception?displayProperty=fullName> ou de uma de suas subclasses no <xref:System> namespace.

 Não crie uma subclasse de <xref:System.Xml.XmlDocument> se desejar criar uma exibição XML de um modelo de objeto subjacente ou fonte de dados.

### <a name="non-generic-collections"></a>Coleções não genéricas
 Use e/ou estenda coleções genéricas sempre que possível. Não estenda coleções não genéricas em seu código, a menos que você as tenha enviado anteriormente.

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
 Não suprimir um aviso desta regra para violações <xref:System.ApplicationException> . É seguro suprimir um aviso desta regra para violações <xref:System.Xml.XmlDocument> . É seguro suprimir um aviso sobre uma coleção não genérica se o código tiver sido liberado anteriormente.
