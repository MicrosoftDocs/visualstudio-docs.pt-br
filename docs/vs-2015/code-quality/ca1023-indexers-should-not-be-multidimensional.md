---
title: 'CA1023: os indexadores não devem ser multidimensionais | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- IndexersShouldNotBeMultidimensional
- CA1023
helpviewer_keywords:
- CA1023
- IndexersShouldNotBeMultidimensional
ms.assetid: ae499879-97f6-434e-a61d-1fedd231d2fb
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 30eee67d54e4fc3c73b265240fff82b0729e1cfc
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546635"
---
# <a name="ca1023-indexers-should-not-be-multidimensional"></a>CA1023: Indexadores não devem ser multidimensionais
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|IndexersShouldNotBeMultidimensional|
|CheckId|CA1023|
|Categoria|Microsoft. Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público ou protegido contém um indexador público ou protegido que usa mais de um índice.

## <a name="rule-description"></a>Descrição da Regra
 Indexadores, ou seja, propriedades indexadas, devem usar um único índice. Indexadores multidimensionais podem reduzir significativamente a usabilidade da biblioteca. Se o design exigir vários índices, reconsidere se o tipo representa um armazenamento de dados lógico. Caso contrário, use um método.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, altere o design para usar um inteiro solitário ou um índice de cadeia de caracteres ou use um método em vez do indexador.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Suprimir um aviso desta regra somente após considerar atentamente a necessidade do indexador não padrão.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo, `DayOfWeek03` , com um indexador multidimensional que viola a regra. O indexador pode ser visto como um tipo de conversão e, portanto, é exposto mais adequadamente como um método. O tipo é reprojetado no `RedesignedDayOfWeek03` para satisfazer a regra.

 [!code-cpp[FxCop.Design.OneDimensionForIndexer#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.OneDimensionForIndexer/cpp/FxCop.Design.OneDimensionForIndexer.cpp#1)]
 [!code-csharp[FxCop.Design.OneDimensionForIndexer#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.OneDimensionForIndexer/cs/FxCop.Design.OneDimensionForIndexer.cs#1)]
 [!code-vb[FxCop.Design.OneDimensionForIndexer#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.OneDimensionForIndexer/vb/FxCop.Design.OneDimensionForIndexer.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1043: Usar argumento integral ou de cadeia de caracteres para indexadores](../code-quality/ca1043-use-integral-or-string-argument-for-indexers.md)

 [CA1024: Usar propriedades quando apropriado](../code-quality/ca1024-use-properties-where-appropriate.md)
