---
title: Personalização das verificações de tempo de execução nativas | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.crt
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- runtime_checks pragma
- debugger, native run-time checks
- /RTC compiler option [C++], native run-time checks
- customizing CRT error checking
- native run-time checks, customizing
ms.assetid: 76a365fe-6439-49db-8603-34058b78e5a8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 66591308c2b0c59cf310d3957131f80191cc51c3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62905480"
---
# <a name="native-run-time-checks-customization"></a>Personalização das verificações de tempo de execução nativas
Quando você compila com **/RTC** (verificações de tempo de execução) ou usar o `runtime_checks` pragma, a biblioteca de tempo de execução C fornece verificações de tempo de execução nativas. Em alguns casos, você pode personalizar a verificação de tempo de execução:

- Para rotear mensagens de verificação de tempo de execução para um arquivo ou destino diferente do padrão.

- Para especificar um destino de saída para mensagens de verificação de tempo de execução em um depurador de terceiros.

- Para reportar mensagens de verificação de tempo de execução de um programa compilado com uma versão lançada da biblioteca em tempo de execução C. As versões de lançamento da biblioteca não usam `_CrtDbgReportW` para reportar erros em tempo de execução. Em vez disso, elas exibem uma caixa de diálogo **Declarar** para cada erro em tempo de execução.

  Para personalizar a verificação de erro em tempo de execução, você pode:

- Escreva uma função de relatório de erro de tempo de execução. Para obter mais informações, confira [Como: Escrever uma função de relatório de erro em tempo de execução](../debugger/how-to-write-a-run-time-error-reporting-function.md).

- Personalize o destino da mensagem de erro.

- Consulte para obter informações sobre erros de verificação de tempo de execução.

## <a name="customize-the-error-message-destination"></a>Personalize o destino da mensagem de erro
 Se você usar `_CrtDbgReportW` para reportar erros, poderá usar `_CrtSetReportMode` para especificar o destino das mensagens de erro.

 Se você usar uma função personalizada de relatório, use `_RTC_SetErrorType` para associar um erro com um tipo de relatório.

## <a name="query-for-information-about-run-time-checks"></a>Consulte para obter informações sobre verificações de tempo de execução
 `_RTC_NumErrors` retorna o número de tipos de erros detectados por verificações de erros em tempo de execução. Para obter uma breve descrição de cada erro, você poderá executar um loop de 0 para o valor de retorno de `_RTC_NumErrors`, passando o valor da iteração para `_RTC_GetErrDesc` em cada loop. Para obter mais informações, consulte [RTC_NumErrors](/cpp/c-runtime-library/reference/rtc-numerrors) e [RTC_GetErrDesc](/cpp/c-runtime-library/reference/rtc-geterrdesc).

## <a name="see-also"></a>Consulte também
- [Como: Usar verificações de tempo de execução nativas](../debugger/how-to-use-native-run-time-checks.md)
- [runtime_checks](/cpp/preprocessor/runtime-checks)
- [_CrtDbgReport, _CrtDbgReportW](/cpp/c-runtime-library/reference/crtdbgreport-crtdbgreportw)