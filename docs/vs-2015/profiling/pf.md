---
title: PF | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cdc0a094-a986-4629-bd1c-dd5fdca323dc
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 67663c067188a703ff6228a703a71ac8a1a0b355
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51757088"
---
# <a name="pf"></a>PF
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A opção de **PF** VSPerfCmd.exe define o evento de criação de perfil com amostragem para falhas da página e pode alterar o número de falhas da página em um intervalo de amostragem do padrão de 10.  
  
> [!NOTE]
>  A PF não pode ser usada em sistemas de 64 bits.  
  
 **Observe que a PF** não tem suporte em computadores de 64 bits. A **PF** só pode ser usada em uma linha de comando que também contenha a opção **Iniciar** ou **Anexar**.  
  
 Por padrão, o evento de amostragem é definido como ciclos de relógio do processador não interrompidos e o intervalo de amostragem é definido como 10.000.000. As opções **Temporizador**, **PF**, **Sys** e **Contador** permitem que você defina o intervalo de amostragem e o evento de amostragem. A opção **GC** coleta dados da memória do .NET em cada alocação e evento de coleta de lixo. Apenas uma dessas opções pode ser especificada em uma linha de comando.  
  
 O evento de amostragem e o intervalo de amostragem só podem ser definidos na primeira linha de comando que contém uma opção **Inicialização** ou **Anexar**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
VSPerfCmd.exe {/Launch:AppName|/Attach:PID} /PF[:Events] [Options]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `Events`  
 Um valor inteiro que especifica o número de eventos de falha de página em um intervalo de amostragem. Caso `Events` não seja especificado, o intervalo é definido como 10.  
  
## <a name="required-options"></a>Opções obrigatórias  
 A **PF** só pode ser especificada em uma linha de comando que contenha uma das opções a seguir.  
  
 **Inicialize:** `AppName`  
 Inicia o criador de perfil e o aplicativo especificado por AppName.  
  
 **Anexar:** `PID`  
 Anexa o criador de perfil ao processo especificado por AppName.  
  
## <a name="invalid-options"></a>Opções inválidas  
 As opções a seguir não podem ser especificadas na mesma linha de comando de **PF**.  
  
 **Temporizador**[**:**`Cycles`]  
 Define o evento de amostragem dos ciclos do relógio do processador e, opcionalmente, define o intervalo de amostragem para `Cycles`. O intervalo do temporizador padrão é 10.000.000.  
  
 **Sys**[**:**`Events`]  
 Define o evento de amostragem para chamadas do aplicativo com perfil ao kernel do sistema operacional (syscalls) e, opcionalmente, define o intervalo de amostragem para `Events`. O intervalo de Sys padrão é 10.  
  
 **Contador:** `Name`[`,Reload`[`,FriendlyName`]]  
 Define o evento de amostragem como contador de desempenho da CPU especificado por `Name` e define o intervalo de amostragem como `Reload`.  
  
 **GC**[**:**{**Alocação**&#124;**Tempo de Vida**}]  
 Coleta dados da memória do .NET. Por padrão (**Alocação**), os dados são coletados em todos os eventos de alocação da memória. Quando o parâmetro **Tempo de Vida** é especificado, os dados também são coletados em todos os eventos de coleta de lixo.  
  
## <a name="example"></a>Exemplo  
 Este exemplo demonstra como definir o evento de amostragem de criação de perfil como falhas de página e definir o intervalo de amostragem para 20 falhas de página.  
  
```  
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp  
VSPerfCmd.exe /Launch:TestApp.exe /PF:20  
```  
  
## <a name="see-also"></a>Consulte também  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [Criando perfil de aplicativos autônomos](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [Criando perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [Serviços de Criação de Perfil](../profiling/command-line-profiling-of-services.md)



