---
title: 'CA2219: Não acionar exceções em cláusulas de exceção'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.topic: reference
f1_keywords:
- DoNotRaiseExceptionsInExceptionClauses
- CA2219
helpviewer_keywords:
- DoNotRaiseExceptionsInExceptionClauses
- CA2219
ms.assetid: 7b9b0bee-4e8e-49a4-8c40-52142b49061f
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f4159dd1b7ff7ba878e851649597d8d3a8908783
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54934004"
---
# <a name="ca2219-do-not-raise-exceptions-in-exception-clauses"></a>CA2219: Não acionar exceções em cláusulas de exceção

|||
|-|-|
|NomeDoTipo|DoNotRaiseExceptionsInExceptionClauses|
|CheckId|CA2219|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Não separáveis, recentes|

## <a name="cause"></a>Causa
 Uma exceção é lançada de uma `finally`, filtro ou cláusula de falha.

## <a name="rule-description"></a>Descrição da regra
 Quando uma exceção é gerada em uma cláusula de exceção, ele aumenta muito a dificuldade de depuração.

 Quando uma exceção é acionada em um `finally` ou cláusula de falha, a nova exceção oculta a exceção ativa, se estiver presente. Isso torna o erro original difícil de detectar e depurar.

 Quando uma exceção é acionada em uma cláusula de filtro, o tempo de execução silenciosamente captura a exceção e faz com que o filtro seja avaliada como false. Não há nenhuma maneira de saber a diferença entre a avaliação de filtro como false e uma exceção que está sendo lançar de um filtro. Isso torna difícil de detectar e depurar erros na lógica do filtro.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir essa violação dessa regra, não explicitamente gere uma exceção de um `finally`, filtro ou cláusula de falha.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso para essa regra. Não há nenhum cenário em que uma exceção gerada em uma cláusula de exceção fornece um benefício ao código em execução.

## <a name="related-rules"></a>Regras relacionadas
 [CA1065: Não gerar exceções em locais inesperados](../code-quality/ca1065-do-not-raise-exceptions-in-unexpected-locations.md)

## <a name="see-also"></a>Consulte também
 [Avisos de design](../code-quality/design-warnings.md)