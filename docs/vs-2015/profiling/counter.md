---
title: Counter | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: aa4b4cdb-e6ea-433a-9579-56f3785e1385
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4d0d15c404284dfb40105f7a52cb23aef132f3a9
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51764943"
---
# <a name="counter"></a>Contador
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A opção **Counter** coleta dados de contadores de desempenho do processador (hardware).  
  
- Quando você está usando o método de criação de perfil de amostragem, **Counter** especifica o contador de desempenho on-chip e o número de eventos do contador a ser usado como o intervalo de amostragem. Você pode especificar apenas um contador quando você está usando amostragem.  
  
- Quando você está usando a método de criação de perfil de instrumentação, o número de eventos do contador que ocorreram no intervalo entre os eventos da coleção anterior e os da atual é listado como campos separados em relatórios do criador de perfil. Várias opções de **Counter** podem ser especificadas quando você usa instrumentação.  
  
  Cada tipo de processador tem seu próprio conjunto de contadores de desempenho de hardware. O criador de perfil define um conjunto de contadores de desempenho que são comuns a quase todos os processadores. Para listar os contadores genéricos e específicos do processador no computador, use o comando VSPerfCmd **QueryCounters**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
VSPerfCmd.exe {/Launch:AppName | /Attach PID} /Counter:Name[,Reload[,FriendlyName]][Options]  
```  
  
```  
VSPerfCmd.exe /Start:Method /Counter:Name[,Reload[,FriendlyName]][/Counter:Name[,Reload[,FriendlyName]]][Options]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `Name`  
 O nome do contador. Use a opção VSPerfCmd.exe **/QueryCounters** para listar os nomes de contadores disponíveis no computador.  
  
 `Reload`  
 O número de eventos de contador no intervalo de amostragem. Não use com o método de instrumentação.  
  
 `FriendlyName`  
 (Opcional) A cadeia de caracteres para usar no lugar de `Name` nos cabeçalhos de coluna de exibições e relatórios do criador de perfil.  
  
## <a name="required-options"></a>Opções obrigatórias  
 A opção Counter só pode ser usada com uma das seguintes opções:  
  
 **Iniciar:** `Trace`  
 Inicializa o criador de perfil para usar o método de instrumentação.  
  
 **Inicialize:** `AppName`  
 Inicia o aplicativo especificado e o criador de perfil. O criador de perfil deve ser inicializado para usar o método de amostragem.  
  
 **Anexar:** `PID`  
 Inicia o criador de perfil e anexa-o ao processo especificado pela ID de processo. O criador de perfil deve ser inicializado para usar o método de amostragem.  
  
## <a name="example"></a>Exemplo  
 A amostra de método de amostragem demonstra como realizar a amostragem de um aplicativo a cada 1.000 ocorrências de NonHaltedCycles do contador genérico do criador de perfil.  
  
 A amostra do método de instrumentação demonstra como inicializar o criador de perfil para coletar eventos do contador L2InstructionFetches. O nome do contador L2InstructionFetches é específico do processador.  
  
```  
; Sample Method Example  
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp  
VSPerfCmd.exe /Launch:TestApp.exe /Counter:NonHaltedCycles,1000,"Non-Halted Cycles"  
  
;INSTRUMENTATION METHOD EXAMPLE  
VSPerfCmd.exe /Start:Trace /Output:TestApp.exe.vsp /Counter:L2InstructionFetches,,"L2 Cache Instruction Fetches"  
```  
  
## <a name="see-also"></a>Consulte também  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [Criando perfil de aplicativos autônomos](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [Criando perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [Serviços de Criação de Perfil](../profiling/command-line-profiling-of-services.md)



