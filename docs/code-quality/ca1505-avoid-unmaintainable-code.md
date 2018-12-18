---
title: 'CA1505: evitar código que não possa ser mantido'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AvoidUnmaintainableCode
- CA1505
helpviewer_keywords:
- AvoidUnmaintainableCode
- CA1505
ms.assetid: 8292b268-5929-4221-b699-f9c414bcec5d
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 9aae34f6e999bcf74fdfbae4597b22529863e34f
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45546909"
---
# <a name="ca1505-avoid-unmaintainable-code"></a>CA1505: evitar código que não possa ser mantido

|||
|-|-|
|NomeDoTipo|AvoidUnmantainableCode|
|CheckId|CA1505|
|Categoria|Microsoft.Maintainability|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Um tipo ou um método tem um baixo valor de índice de facilidade de manutenção.

## <a name="rule-description"></a>Descrição da regra
 O índice de facilidade de manutenção é calculado usando as seguintes métricas: linhas de código, o volume de programa e a complexidade ciclomática. Volume do programa é uma medida da dificuldade de compreensão de um tipo ou método que se baseia no número de operadores e operandos no código. A complexidade ciclomática é uma medida da complexidade estrutural do tipo ou método. Você pode aprender mais sobre as métricas de código em [medindo complexidade e facilidade de manutenção do código gerenciado](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md).

 Um índice de facilidade de manutenção baixa indica que um tipo ou método é provavelmente difícil de manter e seria um bom candidato para refazer o design.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir essa violação, recriar o tipo ou método e tente dividi-lo em menores e mais concentrados tipos ou métodos.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Exclua esse aviso quando um tipo ou método ainda é considerado sustentável, apesar de seu tamanho grande ou quando o tipo ou método não pode ser dividido.

## <a name="see-also"></a>Consulte também

- [Avisos de facilidade de manutenção](../code-quality/maintainability-warnings.md)
- [Medindo complexidade e facilidade de manutenção do código gerenciado](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)