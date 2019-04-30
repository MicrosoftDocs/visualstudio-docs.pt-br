---
title: 'CA1031: Não capturar tipos de exceção geral | Microsoft Docs'
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 4588a949b4b6439c3f76270b0bcdab9cd52c23d9
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63431223"
---
# <a name="ca1031-do-not-catch-general-exception-types"></a>CA1031: Não capturar tipos de exceção geral
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|DoNotCatchGeneralExceptionTypes|
|CheckId|CA1031|
|Categoria|Microsoft.Design|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Uma exceção geral, como <xref:System.Exception?displayProperty=fullName> ou <xref:System.SystemException?displayProperty=fullName> é capturada em um `catch` instrução ou uma cláusula catch geral, como `catch()` é usado.

## <a name="rule-description"></a>Descrição da Regra
 As exceções gerais não devem ser capturadas.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, capturar uma exceção mais específica ou relance a exceção geral como a última instrução no `catch` bloco.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra. Capturando tipos de exceção geral pode ocultar problemas de tempo de execução do usuário de biblioteca e pode facilitar a depuração mais difícil.

> [!NOTE]
> Começando com o [!INCLUDE[net_v40_long](../includes/net-v40-long-md.md)], o common language runtime (CLR) não oferece mais exceções de estado corrompido que ocorrem no sistema operacional e código gerenciado, como violações de acesso em [!INCLUDE[TLA#tla_mswin](../includes/tlasharptla-mswin-md.md)], para ser tratada pelo código gerenciado. Se você quiser compilar um aplicativo na [!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)] ou versões posteriores e manter o tratamento de exceções de estado corrompido, você pode aplicar o <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute> de atributo para o método que manipula a exceção de estado corrompido.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola essa regra e um tipo que implementa corretamente o `catch` bloco.

 [!code-cpp[FxCop.Design.ExceptionAndSystemException#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.ExceptionAndSystemException/cpp/FxCop.Design.ExceptionAndSystemException.cpp#1)]
 [!code-csharp[FxCop.Design.ExceptionAndSystemException#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ExceptionAndSystemException/cs/FxCop.Design.ExceptionAndSystemException.cs#1)]
 [!code-vb[FxCop.Design.ExceptionAndSystemException#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.ExceptionAndSystemException/vb/FxCop.Design.ExceptionAndSystemException.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2200: Relançar para preservar detalhes da pilha](../code-quality/ca2200-rethrow-to-preserve-stack-details.md)
