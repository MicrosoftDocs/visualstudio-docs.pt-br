---
title: 'CA2219: Não gerar exceções em cláusulas de exceção | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotRaiseExceptionsInExceptionClauses
- CA2219
helpviewer_keywords:
- DoNotRaiseExceptionsInExceptionClauses
- CA2219
ms.assetid: 7b9b0bee-4e8e-49a4-8c40-52142b49061f
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 506b9d243ef83242b7e17c295dfc13ef9039d1f6
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58921957"
---
# <a name="ca2219-do-not-raise-exceptions-in-exception-clauses"></a>CA2219: Não acionar exceções em cláusulas de exceção
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|DoNotRaiseExceptionsInExceptionClauses|
|CheckId|CA2219|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Não separáveis, recentes|

## <a name="cause"></a>Causa
 Uma exceção é lançada de uma `finally`, filtro ou cláusula de falha.

## <a name="rule-description"></a>Descrição da Regra
 Quando uma exceção é gerada em uma cláusula de exceção, ele aumenta muito a dificuldade de depuração.

 Quando uma exceção é acionada em um `finally` ou cláusula de falha, a nova exceção oculta a exceção ativa, se estiver presente. Isso torna o erro original difícil de detectar e depurar.

 Quando uma exceção é acionada em uma cláusula de filtro, o tempo de execução silenciosamente captura a exceção e faz com que o filtro seja avaliada como false. Não há nenhuma maneira de saber a diferença entre a avaliação de filtro como false e uma exceção que está sendo lançar de um filtro. Isso torna difícil de detectar e depurar erros na lógica do filtro.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir essa violação dessa regra, não explicitamente gere uma exceção de um `finally`, filtro ou cláusula de falha.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso para essa regra. Não há nenhum cenário em que uma exceção gerada em uma cláusula de exceção fornece um benefício ao código em execução.

## <a name="related-rules"></a>Regras relacionadas
 [CA1065: Não gerar exceções em locais inesperados](../code-quality/ca1065-do-not-raise-exceptions-in-unexpected-locations.md)

## <a name="see-also"></a>Consulte também
 [Avisos de design](../code-quality/design-warnings.md)
