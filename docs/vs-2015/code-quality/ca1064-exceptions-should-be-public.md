---
title: 'CA1064: as exceções devem ser públicas | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1064
- ExceptionsShouldBePublic
helpviewer_keywords:
- ExceptionsShouldBePublic
- CA1064
ms.assetid: 83eb224c-2456-4368-acf4-3b3378e67759
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: fc78c4eaacc3ef0a480b913d20537aeebe5bfc01
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539263"
---
# <a name="ca1064-exceptions-should-be-public"></a>CA1064: Exceções devem ser públicas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|ExceptionsShouldBePublic|
|CheckId|CA1064|
|Categoria|Microsoft. Design|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Uma exceção não pública deriva diretamente de <xref:System.Exception> , <xref:System.SystemException> ou <xref:System.ApplicationException> .

## <a name="rule-description"></a>Descrição da Regra
 Uma exceção interna só é visível dentro de seu próprio escopo interno. Depois que a exceção falha fora do escopo interno, somente a exceção de base pode ser usada para capturar a exceção. Se a exceção interna for herdada de <xref:System.Exception> , <xref:System.SystemException> ou <xref:System.ApplicationException> , o código externo não terá informações suficientes para saber o que fazer com a exceção.

 Mas, se o código tiver uma exceção pública que, posteriormente, é usada como base para uma exceção interna, é razoável assumir que o código ainda será capaz de fazer algo inteligente com a exceção base. A exceção pública terá mais informações do que o fornecido pelo T:System.Exception, T:System.SystemException ou T:System.ApplicationException.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Torne a exceção pública ou derive a exceção interna de uma exceção pública que não seja <xref:System.Exception> , <xref:System.SystemException> ou <xref:System.ApplicationException> .

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Suprimir uma mensagem dessa regra se você tiver certeza de que, em todos os casos, a exceção particular será detectada em seu próprio escopo interno.

## <a name="example"></a>Exemplo
 Essa regra é acionada no primeiro método de exemplo, FirstCustomException porque a classe de exceção deriva diretamente da exceção e é interna. A regra não é acionada na classe SecondCustomException porque, embora a classe também derive diretamente da exceção, a classe é declarada pública. A terceira classe também não aciona a regra porque ela não deriva diretamente de <xref:System.Exception?displayProperty=fullName> , <xref:System.SystemException?displayProperty=fullName> ou <xref:System.ApplicationException?displayProperty=fullName> .

 [!code-csharp[FxCop.Design.ExceptionsShouldBePublic.CA1064#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.design.exceptionsshouldbepublic.ca1064/cs/ca1064 - exceptionsshouldbepublic.cs#1)]
