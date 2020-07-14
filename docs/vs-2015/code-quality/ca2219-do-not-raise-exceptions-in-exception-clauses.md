---
title: 'CA2219: não gerar exceções nas cláusulas de exceção | Microsoft Docs'
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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 960c74625a04b209dc9aa251256e994517a3a52f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85538522"
---
# <a name="ca2219-do-not-raise-exceptions-in-exception-clauses"></a>CA2219: Não acionar exceções em cláusulas de exceção
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DoNotRaiseExceptionsInExceptionClauses|
|CheckId|CA2219|
|Categoria|Microsoft. Usage|
|Alteração Significativa|Sem interrupção, quebra|

## <a name="cause"></a>Causa
 Uma exceção é lançada de uma `finally` cláusula, filtro ou falha.

## <a name="rule-description"></a>Descrição da Regra
 Quando uma exceção é gerada em uma cláusula de exceção, aumenta muito a dificuldade de depuração.

 Quando uma exceção é gerada em uma `finally` cláusula ou falha, a nova exceção oculta a exceção ativa, se presente. Isso torna o erro original difícil de detectar e depurar.

 Quando uma exceção é gerada em uma cláusula de filtro, o tempo de execução captura silenciosamente a exceção e faz com que o filtro seja avaliado como falso. Não há como dizer a diferença entre o filtro avaliando como falso e uma exceção sendo emitida de um filtro. Isso torna difícil detectar e depurar erros na lógica do filtro.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir essa violação dessa regra, não gere explicitamente uma exceção de uma `finally` cláusula, filtro ou falha.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprimir um aviso para esta regra. Não há cenários sob os quais uma exceção gerada em uma cláusula de exceção fornece um benefício para o código em execução.

## <a name="related-rules"></a>Regras relacionadas
 [CA1065: Não acionar exceções em locais inesperados](../code-quality/ca1065-do-not-raise-exceptions-in-unexpected-locations.md)

## <a name="see-also"></a>Consulte Também
 [Avisos de design](../code-quality/design-warnings.md)
