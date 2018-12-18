---
title: Sys (VSPerfCmd) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 294a6f9e-b49f-4c83-b322-5ac5411b66fb
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7968d35050c7b36957b56b9c707fe0404842a07a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51749817"
---
# <a name="sys-vsperfcmd"></a>Sys (VSPerfCmd)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A opção VSPerfCmd.exe **Sys** define o evento de criação de perfil que é amostrado aos eventos de chamada do sistema (chamadas de função do aplicativo de perfil para o sistema operacional) e, opcionalmente, altera o número de chamadas em um intervalo de amostragem do padrão de 10.  
  
 **Sys** só pode ser usada em uma linha de comando que também contém a opção de **Inicialização** ou **Anexar**.  
  
 Por padrão, o evento de amostragem do criador de perfil é definido como ciclos de relógio do processador e o intervalo de amostragem é definido como 10.000.000. As opções **Temporizador**, **PF**, **Sys** e **Contador** permitem que você defina o intervalo de amostragem e o evento de amostragem. A opção **GC** coleta dados da memória do .NET em cada alocação e evento de coleta de lixo. Apenas uma dessas opções pode ser especificada em uma linha de comando.  
  
 O evento de amostragem e o intervalo de amostragem só podem ser definidos na primeira linha de comando que contém uma opção **Inicialização** ou **Anexar**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
VSPerfCmd.exe {/Launch:AppName|Attach:PID} /Sys[:Events] [Options]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `Events`  
 Um valor inteiro que especifica o número de eventos de falha do sistema em um intervalo de amostragem. Caso `Events` não seja especificado, o intervalo é definido como 10.  
  
## <a name="required-options"></a>Opções obrigatórias  
 **Sys** requer uma das opções a seguir.  
  
 **Inicialize:** `AppName`  
 Inicia o criador de perfil e o aplicativo especificado por `AppName`.  
  
 **Anexar:** `PID`  
 Anexa o criador de perfil para o processo especificado por `PID`.  
  
## <a name="invalid-options"></a>Opções inválidas  
 As opções a seguir não podem ser especificadas na mesma linha de comando de **Sys**.  
  
 **PF**[**:**`Events`]  
 Define o evento de amostragem como falhas de página e, como opção, define o intervalo de amostragem como `Events`. O intervalo de PF padrão é 10.  
  
 **Temporizador**[**:**`Cycles`]  
 Define o evento de amostragem dos ciclos do relógio do processador e, opcionalmente, define o intervalo de amostragem para `Cycles`. O intervalo do temporizador padrão é 10.000.000.  
  
 **Contador:** `Name`[`,Reload`[`,FriendlyName`]]  
 Define o evento de amostragem como contador de desempenho da CPU especificado por `Name` e define o intervalo de amostragem como `Reload`.  
  
 **GC**[**:**{**Alocação**&#124;**Tempo de Vida**}]  
 Coleta dados da memória do .NET. Por padrão (**Alocação**), os dados são coletados em todos os eventos de alocação da memória. Quando o parâmetro **Tempo de Vida** é especificado, os dados também são coletados em todos os eventos de coleta de lixo.  
  
## <a name="example"></a>Exemplo  
 Este exemplo demonstra como configurar o criador de perfil do evento de amostragem para chamadas do sistema e como definir o intervalo de amostragem de 20 chamadas por amostra.  
  
```  
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp  
VSPerfCmd.exe /Launch:TestApp.exe /Sys:20  
```  
  
## <a name="see-also"></a>Consulte também  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [Criando perfil de aplicativos autônomos](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [Criando perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [Serviços de Criação de Perfil](../profiling/command-line-profiling-of-services.md)



