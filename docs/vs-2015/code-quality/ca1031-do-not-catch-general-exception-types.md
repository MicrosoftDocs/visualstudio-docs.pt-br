---
title: 'CA1031: não capturar tipos de exceção geral | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1031
- DoNotCatchGeneralExceptionTypes
helpviewer_keywords:
- CA1031
- DoNotCatchGeneralExceptionTypes
ms.assetid: cbc283ae-2a46-4ec0-940e-85aa189b118f
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 2696446ee2b257b78559909c0cba672cded39943
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661892"
---
# <a name="ca1031-do-not-catch-general-exception-types"></a>CA1031: não capturar tipos de exceção gerais
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|DoNotCatchGeneralExceptionTypes|
|CheckId|CA1031|
|Categoria|Microsoft. Design|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Uma exceção geral, como <xref:System.Exception?displayProperty=fullName> ou <xref:System.SystemException?displayProperty=fullName>, é capturada em uma instrução `catch` ou uma cláusula catch geral, como `catch()`, é usada.

## <a name="rule-description"></a>Descrição da Regra
 As exceções gerais não devem ser capturadas.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, Capture uma exceção mais específica ou relance a exceção geral como a última instrução no bloco `catch`.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra. A captura de tipos de exceção gerais pode ocultar os problemas de tempo de execução do usuário da biblioteca e tornar a depuração mais difícil.

> [!NOTE]
> A partir do [!INCLUDE[net_v40_long](../includes/net-v40-long-md.md)], o Common Language Runtime (CLR) não entrega mais exceções de estado corrompido que ocorrem no sistema operacional e no código gerenciado, como violações de acesso no [!INCLUDE[TLA#tla_mswin](../includes/tlasharptla-mswin-md.md)], a serem manipuladas pelo código gerenciado. Se você quiser compilar um aplicativo no [!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)] ou em versões posteriores e manter o tratamento de exceções de estado corrompidas, poderá aplicar o atributo <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute> ao método que manipula a exceção de estado corrompido.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola essa regra e um tipo que implementa corretamente o bloco `catch`.

 [!code-cpp[FxCop.Design.ExceptionAndSystemException#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.ExceptionAndSystemException/cpp/FxCop.Design.ExceptionAndSystemException.cpp#1)]
 [!code-csharp[FxCop.Design.ExceptionAndSystemException#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ExceptionAndSystemException/cs/FxCop.Design.ExceptionAndSystemException.cs#1)]
 [!code-vb[FxCop.Design.ExceptionAndSystemException#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.ExceptionAndSystemException/vb/FxCop.Design.ExceptionAndSystemException.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2200: relançar para preservar detalhes da pilha](../code-quality/ca2200-rethrow-to-preserve-stack-details.md)
