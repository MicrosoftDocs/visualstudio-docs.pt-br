---
title: 'CA1064: as exceções devem ser públicas'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1064
- ExceptionsShouldBePublic
helpviewer_keywords:
- ExceptionsShouldBePublic
- CA1064
ms.assetid: 83eb224c-2456-4368-acf4-3b3378e67759
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 904aa1fe83677e2d53d2e93964619a5c2aa82625
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49816787"
---
# <a name="ca1064-exceptions-should-be-public"></a>CA1064: as exceções devem ser públicas

|||
|-|-|
|NomeDoTipo|ExceptionsShouldBePublic|
|CheckId|CA1064|
|Categoria|Microsoft.Design|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa
 Uma exceção não público deriva diretamente <xref:System.Exception>, <xref:System.SystemException>, ou <xref:System.ApplicationException>.

## <a name="rule-description"></a>Descrição da regra
 Uma exceção interna só é visível dentro de seu próprio escopo interno. Depois que a exceção falha fora do escopo interno, somente a exceção de base pode ser usada para capturar a exceção. Se a exceção interna for herdada de <xref:System.Exception>, <xref:System.SystemException>, ou <xref:System.ApplicationException>, o código externo não terá informações suficientes para saber o que fazer com a exceção.

 Mas, se o código tem uma exceção de pública que é usada posteriormente como base para uma exceção interna, é razoável pressupor que o código ainda mais out será capaz de fazer algo inteligentes com a exceção de base. A exceção pública terão mais informações do que aquelas fornecidas pelo <xref:System.Exception>, <xref:System.SystemException>, ou <xref:System.ApplicationException>.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Verifique a exceção público ou derivar a exceção interna de uma exceção de pública que não seja <xref:System.Exception>, <xref:System.SystemException>, ou <xref:System.ApplicationException>.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Suprima uma mensagem a partir dessa regra, se você tiver certeza em todos os casos que o privado exceção será capturada dentro de seu próprio escopo interno.

## <a name="example"></a>Exemplo
 Essa regra é acionada no primeiro método de exemplo, FirstCustomException porque a classe de exceção deriva diretamente da exceção e é interna. A regra não é disparado na classe SecondCustomException porque, embora a classe também deriva diretamente da exceção, a classe é declarada pública. A terceira classe também não dispara a regra porque ele não deriva diretamente <xref:System.Exception?displayProperty=fullName>, <xref:System.SystemException?displayProperty=fullName>, ou <xref:System.ApplicationException?displayProperty=fullName>.

 [!code-csharp[FxCop.Design.ExceptionsShouldBePublic.CA1064#1](../code-quality/codesnippet/CSharp/ca1064-exceptions-should-be-public_1.cs)]
