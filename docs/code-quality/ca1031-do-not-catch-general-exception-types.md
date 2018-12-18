---
title: 'CA1031: não capturar tipos de exceção gerais'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1031
- DoNotCatchGeneralExceptionTypes
helpviewer_keywords:
- CA1031
- DoNotCatchGeneralExceptionTypes
ms.assetid: cbc283ae-2a46-4ec0-940e-85aa189b118f
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 16b43aa25ef4e2d81b2d6f72e7e1c2bfa3e8b6f7
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45551606"
---
# <a name="ca1031-do-not-catch-general-exception-types"></a>CA1031: não capturar tipos de exceção gerais

|||
|-|-|
|NomeDoTipo|DoNotCatchGeneralExceptionTypes|
|CheckId|CA1031|
|Categoria|Microsoft.Design|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Uma exceção geral, como <xref:System.Exception?displayProperty=fullName> ou <xref:System.SystemException?displayProperty=fullName> é capturada em um `catch` instrução ou uma cláusula catch geral, como `catch()` é usado.

## <a name="rule-description"></a>Descrição da regra
 As exceções gerais não devem ser capturadas.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, capturar uma exceção mais específica ou relance a exceção geral como a última instrução no `catch` bloco.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra. Capturando tipos de exceção geral pode ocultar problemas de tempo de execução do usuário de biblioteca e pode facilitar a depuração mais difícil.

> [!NOTE]
> Começando com o [!INCLUDE[net_v40_long](../code-quality/includes/net_v40_long_md.md)], o common language runtime (CLR) não oferece mais exceções de estado corrompido que ocorrem no sistema operacional e código gerenciado, como violações de acesso em [!INCLUDE[TLA#tla_mswin](../code-quality/includes/tlasharptla_mswin_md.md)], para ser tratada pelo código gerenciado. Se você quiser compilar um aplicativo na [!INCLUDE[net_v40_short](../code-quality/includes/net_v40_short_md.md)] ou versões posteriores e manter o tratamento de exceções de estado corrompido, você pode aplicar o <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute> de atributo para o método que manipula a exceção de estado corrompido.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola essa regra e um tipo que implementa corretamente o `catch` bloco.

 [!code-cpp[FxCop.Design.ExceptionAndSystemException#1](../code-quality/codesnippet/CPP/ca1031-do-not-catch-general-exception-types_1.cpp)]
 [!code-vb[FxCop.Design.ExceptionAndSystemException#1](../code-quality/codesnippet/VisualBasic/ca1031-do-not-catch-general-exception-types_1.vb)]
 [!code-csharp[FxCop.Design.ExceptionAndSystemException#1](../code-quality/codesnippet/CSharp/ca1031-do-not-catch-general-exception-types_1.cs)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2200: relançar para preservar detalhes da pilha](../code-quality/ca2200-rethrow-to-preserve-stack-details.md)