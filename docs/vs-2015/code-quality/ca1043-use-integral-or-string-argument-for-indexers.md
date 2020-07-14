---
title: 'CA1043: usar argumento integral ou de cadeia de caracteres para indexadores | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1043
- UseIntegralOrStringArgumentForIndexers
helpviewer_keywords:
- CA1043
- UseIntegralOrStringArgumentForIndexers
ms.assetid: d7f14b9e-2220-4f80-b6b8-48c655a05701
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 03d21a824d2d3a9151dad139575f32e3417cbd39
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546829"
---
# <a name="ca1043-use-integral-or-string-argument-for-indexers"></a>CA1043: Usar argumento integral ou de cadeia de caracteres para indexadores
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|UseIntegralOrStringArgumentForIndexers|
|CheckId|CA1043|
|Categoria|Microsoft. Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público ou protegido contém um indexador público ou protegido que usa um tipo de índice diferente de <xref:System.Int32?displayProperty=fullName> , <xref:System.Int64?displayProperty=fullName> , <xref:System.Object?displayProperty=fullName> ou <xref:System.String?displayProperty=fullName> .

## <a name="rule-description"></a>Descrição da Regra
 Indexadores, ou seja, propriedades indexadas, devem usar tipos inteiros ou de cadeia de caracteres para o índice. Esses tipos são normalmente usados para indexar estruturas de dados e aumentar a usabilidade da biblioteca. O uso do <xref:System.Object> tipo deve ser restrito a esses casos em que o inteiro ou o tipo de cadeia de caracteres específico não pode ser especificado em tempo de design. Se o design exigir outros tipos para o índice, reconsidere se o tipo representa um armazenamento de dados lógico. Se não representar um armazenamento de dados lógico, use um método.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, altere o índice para um tipo inteiro ou de cadeia de caracteres, ou use um método em vez do indexador.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Suprimir um aviso desta regra somente após considerar atentamente a necessidade do indexador não padrão.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um indexador que usa um <xref:System.Int32> índice.

 [!code-cpp[FxCop.Design.IntegralOrStringIndexers#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.IntegralOrStringIndexers/cpp/FxCop.Design.IntegralOrStringIndexers.cpp#1)]
 [!code-csharp[FxCop.Design.IntegralOrStringIndexers#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.IntegralOrStringIndexers/cs/FxCop.Design.IntegralOrStringIndexers.cs#1)]
 [!code-vb[FxCop.Design.IntegralOrStringIndexers#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.IntegralOrStringIndexers/vb/FxCop.Design.IntegralOrStringIndexers.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1023: Indexadores não devem ser multidimensionais](../code-quality/ca1023-indexers-should-not-be-multidimensional.md)

 [CA1024: Usar propriedades quando apropriado](../code-quality/ca1024-use-properties-where-appropriate.md)
