---
title: 'CA1043: usar argumento integral ou da cadeia de caracteres para indexadores'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1043
- UseIntegralOrStringArgumentForIndexers
helpviewer_keywords:
- CA1043
- UseIntegralOrStringArgumentForIndexers
ms.assetid: d7f14b9e-2220-4f80-b6b8-48c655a05701
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: bb8781b205da07c1c075e2638716cfc139491d07
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45550577"
---
# <a name="ca1043-use-integral-or-string-argument-for-indexers"></a>CA1043: usar argumento integral ou da cadeia de caracteres para indexadores

|||
|-|-|
|NomeDoTipo|UseIntegralOrStringArgumentForIndexers|
|CheckId|CA1043|
|Categoria|Microsoft.Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público ou protegido contém um indexador público ou protegido que usa um tipo de índice diferente de <xref:System.Int32?displayProperty=fullName>, <xref:System.Int64?displayProperty=fullName>, <xref:System.Object?displayProperty=fullName>, ou <xref:System.String?displayProperty=fullName>.

## <a name="rule-description"></a>Descrição da regra
 Indexadores, ou seja, propriedades indexadas, devem usar tipos de inteiro ou cadeia de caracteres para o índice. Esses tipos são normalmente usados para indexar estruturas de dados e aumentam a usabilidade da biblioteca. Usar o <xref:System.Object> tipo deve ser restrito a esses casos em que o tipo de inteiro ou cadeia de caracteres específico não pode ser especificado em tempo de design. Se o projeto requer outros tipos para o índice, reconsidere se o tipo representa um armazenamento de dados lógicos. Se ele não representa um repositório de dados lógicos, use um método.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, alterar o índice para um tipo de inteiro ou cadeia de caracteres ou usar um método em vez do indexador.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Suprima um aviso nessa regra somente após considerar cuidadosamente a necessidade do indexador não padrão.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um indexador que usa um <xref:System.Int32> índice.

 [!code-csharp[FxCop.Design.IntegralOrStringIndexers#1](../code-quality/codesnippet/CSharp/ca1043-use-integral-or-string-argument-for-indexers_1.cs)]
 [!code-cpp[FxCop.Design.IntegralOrStringIndexers#1](../code-quality/codesnippet/CPP/ca1043-use-integral-or-string-argument-for-indexers_1.cpp)]
 [!code-vb[FxCop.Design.IntegralOrStringIndexers#1](../code-quality/codesnippet/VisualBasic/ca1043-use-integral-or-string-argument-for-indexers_1.vb)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1023: os indexadores não devem ser multidimensionais](../code-quality/ca1023-indexers-should-not-be-multidimensional.md)

 [CA1024: usar propriedades quando apropriado](../code-quality/ca1024-use-properties-where-appropriate.md)