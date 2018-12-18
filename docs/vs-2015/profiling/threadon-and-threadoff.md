---
title: ThreadOn e ThreadOff | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5cd5a695-0a14-484a-8952-ed47e13d8e92
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4e908da955258bfef5d66187bc974b6e051a48ad
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51789160"
---
# <a name="threadon-and-threadoff"></a>ThreadOn e ThreadOff
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Os subcomandos **ThreadOff** e **ThreadOn** do VSPerfCmd.exe só estão disponíveis em sessões de criação de perfil de linha de comando que usam o método de instrumentação. **ThreadOff** e **ThreadOn** pausam e retomam a criação de perfil para o thread especificado. O **ThreadOff** para a criação de perfil do thread e o **ThreadOn** inicia a criação de perfil do thread.  
  
 Na maioria dos casos, você deve especificar **ThreadOn** ou **ThreadOff** como a única opção em uma linha de comando VSPerfCmd.exe, mas eles também podem ser combinados com os subcomandos **GlobalOn**, **GlobalOff**, **ProcessOn** e **ProcessOff**.  
  
 Os subcomandos **ThreadOn** e **ThreadOff** interagem com os subcomandos **GlobalOn** e **GlobalOff**, que controlam a coleta de dados para todos os processos em uma sessão de criação de perfil de linha de comando, e os subcomandos **ProcessOn** e **ProcessOff**, que controlam a coleta de dados para um processo especificado.  
  
 Os subcomandos **ThreadOff** e **ThreadOn** também afetam a contagem de início/parada de thread que é manipulada por funções da API do criador de perfil.  
  
- O **ThreadOff** define imediatamente a contagem de início/parada de thread para 0 e, portanto, faz uma pausa de criação de perfil.  
  
- O **ThreadOn** define imediatamente a contagem de início/parada de thread para 1 e, portanto, retoma de criação de perfil.  
  
  Confira [APIs de ferramentas de criação de perfil](../profiling/profiling-tools-apis.md) para obter mais informações.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
VSPerfCmd.exe /{ThreadOff|ThreadOn}:TID [Options]  
  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `TID`  
 O identificador inteiro do thread para iniciar ou parar.  
  
## <a name="valid-options"></a>Opções válidas  
 O **ThreadOn** e **ThreadOff** podem ser especificados em linhas de comando que também contêm os subcomandos a seguir.  
  
 **Iniciar:** `Method`  
 Inicializa a sessão de criação de perfil de linha de comando e define o método de criação de perfil especificado.  
  
 **GlobalOff**&#124;**GlobalOn**  
 Interrompe ou inicia a criação de perfil para todos os processos em uma sessão de criação de perfil de linha de comando.  
  
 {**ProcessOff**&#124;**ProcessOn**}**:**`TID`  
 Interrompe ou inicia a criação de perfil para o processo especificado.  
  
## <a name="example"></a>Exemplo  
 Neste exemplo, o subcomando **ThreadOff** é usado para interromper a coleta de dados de criação de perfil para coletar apenas os dados de inicialização do aplicativo.  
  
```  
; Initialize the profiler.  
VSPerfCmd.exe /Start:Trace /Output:Instrument.vsp   
; Start the instrumented application.  
; Stop profiling the thread after startup.  
VSPerfCmd.exe /ThreadOff:12345  
; Shut down the target application.  
; Close the profiler.  
VSPerfCmd /Shutdown  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [Criando perfil de aplicativos autônomos](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [Criando perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [Serviços de Criação de Perfil](../profiling/command-line-profiling-of-services.md)



