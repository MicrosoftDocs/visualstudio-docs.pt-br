---
title: GlobalOn e GlobalOff | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 24b0ed68-d19e-473e-9af3-252c11d82bcf
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 1731c47d3de9068affd4c7561e1dae94960b2b44
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49835911"
---
# <a name="globalon-and-globaloff"></a>GlobalOn e GlobalOff
As opções *VSPerfCmd.exe* **GlobalOff** e **GlobalOn** pausam e retomam a criação de perfil de todos os processos e threads em uma sessão de criação de perfil de linha de comando.  
  
 Você pode especificar **GlobalOn** e **GlobalOff** como as únicas opções em uma linha de comando do *VSPerfCmd.exe* ou pode incluí-las nas linhas de comando que também contêm as opções **Start**, **Launch** ou **Attach**.  
  
 **GlobalOn** e **GlobalOff** também podem ser combinados com as opções **ProcessOn**, **ProcessOff**, **ThreadOn** e **ThreadOff**.  
  
 As opções **GlobalOn** e **GlobalOff** interagem com as opções **ProcessOn** e **ProcessOff** que controlam a coleta de dados para um processo especificado e com as opções **ThreadOn** e **ThreadOff** que controlam a coleta de dados para um thread especificado.  
  
 As opções **GlobalOff** e **GlobalOn** também afetam a contagem Global de Iniciar/Parar que é manipulada pelas funções de API do criador de perfil.  
  
- **GlobalOff** imediatamente define a Contagem global de iniciar/parar para 0 e, portanto, fará uma pausa de criação de perfil.  
  
- **GlobalOn** imediatamente define a Contagem global de iniciar/parar para 1 e, portanto, retomará a criação de perfil.  
  
  Confira [APIs de ferramentas de criação de perfil](../profiling/profiling-tools-apis.md) para obter mais informações.  
  
## <a name="syntax"></a>Sintaxe  
  
```cmd  
VSPerfCmd.exe /{GlobalOff|GlobalOn}  
  
VSPerfCmd.exe /Start:Method /{GlobalOff|GlobalOn} [Options]  
  
VSPerfCmd.exe {Launch:AppName|Attach:PID} /{GlobalOff|GlobalOn}[Options]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 Nenhum  
  
## <a name="valid-options"></a>Opções válidas  
 **GlobalOn** e **GlobalOff** podem ser especificados em linhas de comando que também contêm as seguintes opções.  
  
 **Iniciar:** `Method`  
 Inicializa a sessão de criador de perfil de linha de comando e define o método de criação de perfil especificado.  
  
 **Inicialize:** `AppName`  
 Inicia o aplicativo especificado e começa a criação de perfil com o método de amostragem.  
  
 **Anexar:** `PID`  
 Inicia a criação de perfil do processo especificado.  
  
 {**ProcessOff**&#124;**ProcessOn**}**:**`PID`  
 Interrompe ou inicia a criação de perfil para o processo especificado.  
  
 {**ThreadOff**&#124;**ThreadOn**}**:**`TID`  
 Interrompe ou inicia a criação de perfil para o processo especificado (somente no método de instrumentação).  
  
## <a name="example"></a>Exemplo  
 Neste exemplo, as opções **GlobalOff** e **GlobalOn** são usadas para evitar a coleta de dados de criação de perfil para inicialização e desligamento do aplicativo.  
  
```cmd  
; Initialize the profiler with profiling stopped.  
VSPerfCmd.exe /Start:Trace /Output:Instrument.vsp /GlobalOff  
; Start an instrumented application and wait for it to warm up.  
; Start profiling.  
VSPerfCmd.exe /GlobalOn  
; Exercise the application functionality that you want to profile.  
; Stop profiling.  
VSPerfCmd.exe /GlobalOff  
; Shut down the target application.  
; Close the profiler.  
VSPerfCmd /Shutdown  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [Criar perfil de aplicativos autônomos](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [Criar o perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [Profile services (Serviços de perfil)](../profiling/command-line-profiling-of-services.md)