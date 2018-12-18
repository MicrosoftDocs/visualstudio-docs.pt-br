---
title: Temporizador | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 1971868e-89fa-4452-8ee7-76e4daf31b66
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 914b0c3e493e8486247704ef22967c8ccd511ed2
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/01/2018
ms.locfileid: "50744997"
---
# <a name="timer"></a>Temporizador
A opção **Timer** do *VSPerfCmd.exe* define o evento de criação de perfil com amostragem para ciclos de relógio do processador e, como opção, altera o número de ciclos em um intervalo de amostragem do padrão de 10.000.000. Em um processador de 1 GHz (um gigahertz), 10.000.000 ciclos de relógio são aproximadamente 100 amostras por segundo. O número mínimo de ciclos que pode ser especificado é 50.000.  
  
 O **Temporizador** só pode ser usado quando você utiliza o método de criação de perfil de amostragem e em uma linha de comando que também contenha a opção **Inicialização** ou **Anexar**.  
  
 Por padrão, o evento de amostragem do criador de perfil é definido como ciclos de relógio do processador e o intervalo de amostragem é definido como 10.000.000. As opções **Temporizador**, **PF**, **Sys** e **Contador** permitem que você defina o intervalo de amostragem e o evento de amostragem. A opção **GC** coleta dados da memória do .NET em cada alocação e evento de coleta de lixo. Apenas uma dessas opções pode ser especificada em uma linha de comando.  
  
 O evento de amostragem e o intervalo de amostragem só podem ser definidos na primeira linha de comando que contém uma opção **Inicialização** ou **Anexar**.  
  
## <a name="syntax"></a>Sintaxe  
  
```cmd  
VSPerfCmd.exe {/Launch:AppName|/Attach:PID} /Timer[:Cycles] [Options]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `Cycles`  
 Um valor inteiro que especifica o número de ciclos de relógio do processador em um intervalo de amostragem. Caso `Cycles` não seja especificado, o intervalo é definido como 10.000.000. Especifique o valor sem vírgulas.  
  
## <a name="required-options"></a>Opções obrigatórias  
 O **Temporizador** só pode ser especificado em uma linha de comando que contenha uma das opções a seguir.  
  
 **Inicialize:** `AppName`  
 Inicia o criador de perfil e o aplicativo especificado por `AppName`.  
  
 **Anexar:** `PID`  
 Anexa o criador de perfil ao processo especificado pela ID de processo (`PID`).  
  
## <a name="invalid-options"></a>Opções inválidas  
 As opções a seguir não podem ser especificadas na mesma linha de comando do **Temporizador**.  
  
 **PF**[**:**`Events`]  
 Define o evento de amostragem como falhas de página e, como opção, define o intervalo de amostragem como `Events`. O intervalo de PF padrão é 10.  
  
 **Sys**[**:**`Events`]  
 Define o evento de amostragem como chamadas do sistema operacional e, como opção, define o intervalo de amostragem como `Events`. O intervalo de Sys padrão é 10.  
  
 **Contador**[**:**`Name,Reload,FriendlyName`]  
 Define o evento de amostragem como contador de desempenho da CPU especificado por `Name` e define o intervalo de amostragem como `Reload`.  
  
 **GC**[**:**{**Alocação**&#124;**Tempo de Vida**}]  
 Coleta dados da memória do .NET. Por padrão (**Alocação**), os dados são coletados em todos os eventos de alocação da memória. Quando o parâmetro **Tempo de Vida** é especificado, os dados também são coletados em todos os eventos de coleta de lixo.  
  
## <a name="example"></a>Exemplo  
 Esse exemplo demonstra como definir o intervalo de amostragem da criação de perfil como 1.000.000 ciclos de processador.  
  
```cmd  
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp  
VSPerfCmd.exe /Launch:TestApp.exe /Timer:1000000  
```  
  
## <a name="see-also"></a>Consulte também  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [Criar perfil de aplicativos autônomos](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [Criar o perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [Profile services (Serviços de perfil)](../profiling/command-line-profiling-of-services.md)