---
title: Personalização das verificações de tempo de execução nativas | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.debug.crt
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- runtime_checks pragma
- debugger, native run-time checks
- /RTC compiler option [C++], native run-time checks
- customizing CRT error checking
- native run-time checks, customizing
ms.assetid: 76a365fe-6439-49db-8603-34058b78e5a8
caps.latest.revision: 23
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 216a96a6702bfabc57d235144bf4a6cc05df4224
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51721133"
---
# <a name="native-run-time-checks-customization"></a>Personalização das verificações de tempo de execução nativas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando você compila com **/RTC** (verificações de tempo de execução) ou usar o `runtime_checks` pragma, a biblioteca de tempo de execução C fornece verificações de tempo de execução nativas. Em alguns casos, você pode personalizar a verificação de tempo de execução:  
  
- Para rotear mensagens de verificação de tempo de execução para um arquivo ou destino diferente do padrão.  
  
- Para especificar um destino de saída para mensagens de verificação de tempo de execução em um depurador de terceiros.  
  
- Para reportar mensagens de verificação de tempo de execução de um programa compilado com uma versão lançada da biblioteca em tempo de execução C. As versões de lançamento da biblioteca não usam `_CrtDbgReportW` para reportar erros em tempo de execução. Em vez disso, eles exibem um **Assert** caixa de diálogo para cada erro de tempo de execução.  
  
  Para personalizar a verificação de erro em tempo de execução, você pode:  
  
- Escreva uma função de relatório de erro de tempo de execução. Para obter mais informações, consulte [como: gravar uma função de relatório de erro de tempo de execução](../debugger/how-to-write-a-run-time-error-reporting-function.md).  
  
- Personalize o destino da mensagem de erro.  
  
- Consulte para obter informações sobre erros de verificação de tempo de execução.  
  
## <a name="customize-the-error-message-destination"></a>Personalize o destino da mensagem de erro  
 Se você usar `_CrtDbgReportW` para reportar erros, poderá usar `_CrtSetReportMode` para especificar o destino das mensagens de erro.  
  
 Se você usar uma função personalizada de relatório, use `_RTC_SetErrorType` para associar um erro com um tipo de relatório.  
  
## <a name="query-for-information-about-run-time-checks"></a>Consulte para obter informações sobre verificações de tempo de execução  
 `_RTC_NumErrors` retorna o número de tipos de erros detectados por verificações de erros de tempo de execução. Para obter uma breve descrição de cada erro, você poderá executar um loop de 0 para o valor de retorno de `_RTC_NumErrors`, passando o valor da iteração para `_RTC_GetErrDesc` em cada loop. Para obter mais informações, consulte [RTC_NumErrors](http://msdn.microsoft.com/library/7e82adae-38e2-4f8b-bc0b-37bda8109fd1) e [RTC_GetErrDesc](http://msdn.microsoft.com/library/7994ec2b-5488-4fd4-806d-a166c9a9f927).  
  
## <a name="see-also"></a>Consulte também  
 [Como: usar verificações de tempo de execução nativas](../debugger/how-to-use-native-run-time-checks.md)   
 [runtime_checks](http://msdn.microsoft.com/library/ae50b43f-f88d-47ad-a2db-3389e9e7df5b)   
 [_CrtDbgReport, _CrtDbgReportW](http://msdn.microsoft.com/library/6e581fb6-f7fb-4716-9432-f0145d639ecc)





