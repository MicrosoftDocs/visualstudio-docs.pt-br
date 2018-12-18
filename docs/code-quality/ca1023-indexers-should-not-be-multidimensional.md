---
title: 'CA1023: os indexadores não devem ser multidimensionais'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
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
manager: douge
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 96b769aa8cc009f122d4cef4ca8d270c6b3fced5
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45547683"
---
# <a name="ca1023-indexers-should-not-be-multidimensional"></a>CA1023: os indexadores não devem ser multidimensionais

|||
|-|-|
|NomeDoTipo|IndexersShouldNotBeMultidimensional|
|CheckId|CA1023|
|Categoria|Microsoft.Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público ou protegido contém um indexador público ou protegido que usa mais de um índice.

## <a name="rule-description"></a>Descrição da regra
 Indexadores, ou seja, propriedades indexadas, devem usar um único índice. Indexadores multidimensionais podem reduzir significativamente a usabilidade da biblioteca. Se o projeto requer vários índices, reconsidere se o tipo representa um armazenamento de dados lógicos. Caso contrário, use um método.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, alterar o design para usar um índice de cadeia de caracteres ou inteiro solitário ou usar um método em vez do indexador.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Suprima um aviso nessa regra somente após considerar cuidadosamente a necessidade do indexador não padrão.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo, `DayOfWeek03`, com um indexador multidimensional que viola a regra. O indexador pode ser visto como um tipo de conversão e, portanto, mais apropriado é exposto como um método. O tipo é reprojetado no `RedesignedDayOfWeek03` para satisfazer a regra.

 [!code-vb[FxCop.Design.OneDimensionForIndexer#1](../code-quality/codesnippet/VisualBasic/ca1023-indexers-should-not-be-multidimensional_1.vb)]
 [!code-cpp[FxCop.Design.OneDimensionForIndexer#1](../code-quality/codesnippet/CPP/ca1023-indexers-should-not-be-multidimensional_1.cpp)]
 [!code-csharp[FxCop.Design.OneDimensionForIndexer#1](../code-quality/codesnippet/CSharp/ca1023-indexers-should-not-be-multidimensional_1.cs)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1043: usar argumento integral ou de cadeia de caracteres para indexadores](../code-quality/ca1043-use-integral-or-string-argument-for-indexers.md)

 [CA1024: usar propriedades quando apropriado](../code-quality/ca1024-use-properties-where-appropriate.md)