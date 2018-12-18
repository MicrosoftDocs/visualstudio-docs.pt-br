---
title: Anexar | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 79614283-6733-4592-a53a-d428052271ad
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 136ee79c8fc7a3c6d627d186cb2f0dd0266b7a42
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51727333"
---
# <a name="attach"></a>Attach
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A opção **Anexar** do VSPerfCmd.exe inicia a criação de perfil de exemplo do processo em execução especificado pela PID (ID do processo).  
  
 Para usar a opção **Anexar**, você deve especificar o método de **exemplo** na opção de início.  
  
> [!NOTE]
>  Se a opção **Iniciar** foi especificada com a opção **Crosssession**, todas as chamadas para **VSPerfCmd /Attach** ou **VSPerfCmd /Detach** também deverão especificar **Crosssession**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
VSPerfCmd.exe /Attach:ProcessID [Options]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `ProcessID`  
 A PID do processo em execução. A PID de um processo em execução é listada na guia Processos do Gerenciador de Tarefas do Windows.  
  
## <a name="valid-options"></a>Opções válidas  
 As seguintes opções **VSPerfCmd** podem ser combinadas com a opção **Anexar** em uma única linha de comando.  
  
 **Crosssession**  
 Permite aplicativos de criação de perfil em sessões que não seja a sessão de logon. Necessário se a opção **Iniciar** foi especificada com a opção **Crosssession**.  
  
 **Iniciar:** `Method`  
 Inicializa a sessão de criador de perfil de linha de comando e define o método de criação de perfil especificado.  
  
 **TargetCLR**  
 Especifica a versão do CLR (Common Language Runtime) do .NET Framework a ser analisada quando mais de uma versão for carregada em uma sessão de criação de perfil. Por padrão, a primeira versão carregada é analisada.  
  
 **GlobalOn GlobalOff**  
 Retoma (**GlobalOn**) ou pausa (**GlobalOff**) a criação de perfil, mas não termina a sessão de criação de perfil.  
  
 **ProcessOn:** `PID` **ProcessOff:** `PID`  
 Retoma (**ProcessOn**) ou pausa (**ProcessOff**) a criação de perfil para o processo especificado.  
  
## <a name="interval-options"></a>Opções de intervalo  
 Uma das seguintes opções de intervalo de amostragem pode ser especificada na linha de comando Anexar. O intervalo de amostragem padrão é 10.000.000 ciclos de relógio do processador.  
  
 **Temporizador**[**:**`Cycles`]**PF**[**:**`Events`]**Sys**[<strong>:</strong>Eventos]**Contador**[**:**`Name`,`Reload`,`FriendlyName`]  
 Especifica o número e o tipo do intervalo de amostragem.  
  
-   **Temporizador** – exemplifica cada `Cycles` ciclo de relógio do processador. Se `Cycles` não for especificado, os 10.000.000 ciclos serão usados.  
  
-   **PF** – exemplifica cada `Events` falha de página. Se `Events` não for especificado, 10 falhas de página serão usadas.  
  
-   **Sys** – exemplifica cada `Events` chamadas para o sistema operacional. Se `Events` não for especificado, 10 chamadas do sistema serão usadas.  
  
-   **Contador** – exemplifica cada número `Reload` do contador de desempenho de CPU especificado por `Name`. Opcionalmente, `FriendlyName` pode especificar uma cadeia de caracteres para usar como o cabeçalho de coluna nos relatórios do criador de perfil.  
  
## <a name="example"></a>Exemplo  
 Este exemplo demonstra como anexar a uma instância em execução de um aplicativo com a ID de processo 12345.  
  
```  
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp  
VSPerfCmd.exe /Attach:12345  
```  
  
## <a name="see-also"></a>Consulte também  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [Criando perfil de aplicativos autônomos](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [Criando perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [Serviços de Criação de Perfil](../profiling/command-line-profiling-of-services.md)



