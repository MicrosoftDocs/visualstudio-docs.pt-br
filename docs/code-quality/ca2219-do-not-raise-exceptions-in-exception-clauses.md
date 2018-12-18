---
title: 'CA2219: não acione exceções em cláusulas de exceção'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 49baf6fe645df35949f47f2796197977d428427e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49885961"
---
# <a name="ca2219-do-not-raise-exceptions-in-exception-clauses"></a>CA2219: não acione exceções em cláusulas de exceção

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
 [CA1065: não acionar exceções em locais inesperados](../code-quality/ca1065-do-not-raise-exceptions-in-unexpected-locations.md)

## <a name="see-also"></a>Consulte também
 [Avisos de design](../code-quality/design-warnings.md)