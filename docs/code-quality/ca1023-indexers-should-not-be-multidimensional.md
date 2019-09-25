---
title: 'CA1023: Indexadores não devem ser multidimensionais'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IndexersShouldNotBeMultidimensional
- CA1023
helpviewer_keywords:
- CA1023
- IndexersShouldNotBeMultidimensional
ms.assetid: ae499879-97f6-434e-a61d-1fedd231d2fb
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: f788ded21ef5dd9c84d218cedb55ec8dcf7eff2d
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71236174"
---
# <a name="ca1023-indexers-should-not-be-multidimensional"></a>CA1023: Indexadores não devem ser multidimensionais

|||
|-|-|
|NomeDoTipo|IndexersShouldNotBeMultidimensional|
|CheckId|CA1023|
|Categoria|Microsoft.Design|
|Alteração significativa|Quebra|

## <a name="cause"></a>Causa
Um tipo público ou protegido contém um indexador público ou protegido que usa mais de um índice.

## <a name="rule-description"></a>Descrição da regra
Indexadores, ou seja, propriedades indexadas, devem usar um único índice. Indexadores multidimensionais podem reduzir significativamente a usabilidade da biblioteca. Se o design exigir vários índices, reconsidere se o tipo representa um armazenamento de dados lógico. Caso contrário, use um método.

## <a name="how-to-fix-violations"></a>Como corrigir violações
Para corrigir uma violação dessa regra, altere o design para usar um inteiro solitário ou um índice de cadeia de caracteres ou use um método em vez do indexador.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
Suprimir um aviso desta regra somente após considerar atentamente a necessidade do indexador não padrão.

## <a name="example"></a>Exemplo
O exemplo a seguir mostra um tipo `DayOfWeek03`,, com um indexador multidimensional que viola a regra. O indexador pode ser visto como um tipo de conversão e, portanto, é exposto mais adequadamente como um método. O tipo é reprojetado no `RedesignedDayOfWeek03` para satisfazer a regra.

[!code-vb[FxCop.Design.OneDimensionForIndexer#1](../code-quality/codesnippet/VisualBasic/ca1023-indexers-should-not-be-multidimensional_1.vb)]
[!code-cpp[FxCop.Design.OneDimensionForIndexer#1](../code-quality/codesnippet/CPP/ca1023-indexers-should-not-be-multidimensional_1.cpp)]
[!code-csharp[FxCop.Design.OneDimensionForIndexer#1](../code-quality/codesnippet/CSharp/ca1023-indexers-should-not-be-multidimensional_1.cs)]

## <a name="related-rules"></a>Regras relacionadas
[CA1043: Usar argumento integral ou de cadeia de caracteres para indexadores](../code-quality/ca1043-use-integral-or-string-argument-for-indexers.md)

[CA1024: Usar propriedades quando apropriado](../code-quality/ca1024-use-properties-where-appropriate.md)