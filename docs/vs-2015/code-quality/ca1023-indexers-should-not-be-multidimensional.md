---
title: 'CA1023: Os indexadores não devem ser multidimensionais | Microsoft Docs'
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
- IndexersShouldNotBeMultidimensional
- CA1023
helpviewer_keywords:
- CA1023
- IndexersShouldNotBeMultidimensional
ms.assetid: ae499879-97f6-434e-a61d-1fedd231d2fb
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: b97e84e7460699c64e32fd6db3f899f4f5c0e3d1
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49900027"
---
# <a name="ca1023-indexers-should-not-be-multidimensional"></a>CA1023: os indexadores não devem ser multidimensionais
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|IndexersShouldNotBeMultidimensional|
|CheckId|CA1023|
|Categoria|Microsoft.Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público ou protegido contém um indexador público ou protegido que usa mais de um índice.

## <a name="rule-description"></a>Descrição da Regra
 Indexadores, ou seja, propriedades indexadas, devem usar um único índice. Indexadores multidimensionais podem reduzir significativamente a usabilidade da biblioteca. Se o projeto requer vários índices, reconsidere se o tipo representa um armazenamento de dados lógicos. Caso contrário, use um método.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, alterar o design para usar um índice de cadeia de caracteres ou inteiro solitário ou usar um método em vez do indexador.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Suprima um aviso nessa regra somente após considerar cuidadosamente a necessidade do indexador não padrão.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo, `DayOfWeek03`, com um indexador multidimensional que viola a regra. O indexador pode ser visto como um tipo de conversão e, portanto, mais apropriado é exposto como um método. O tipo é reprojetado no `RedesignedDayOfWeek03` para satisfazer a regra.

 [!code-cpp[FxCop.Design.OneDimensionForIndexer#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.OneDimensionForIndexer/cpp/FxCop.Design.OneDimensionForIndexer.cpp#1)]
 [!code-csharp[FxCop.Design.OneDimensionForIndexer#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.OneDimensionForIndexer/cs/FxCop.Design.OneDimensionForIndexer.cs#1)]
 [!code-vb[FxCop.Design.OneDimensionForIndexer#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.OneDimensionForIndexer/vb/FxCop.Design.OneDimensionForIndexer.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1043: usar argumento integral ou de cadeia de caracteres para indexadores](../code-quality/ca1043-use-integral-or-string-argument-for-indexers.md)

 [CA1024: usar propriedades quando apropriado](../code-quality/ca1024-use-properties-where-appropriate.md)



