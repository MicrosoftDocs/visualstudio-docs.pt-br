---
title: VSPerfCmd | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- performance tools, VSPerfCmd tool
- command-line tools, VSPerfCmd tool
- command line, tools
- profiling tools,VSPerfCmd
- VSPerfCmd tool
ms.assetid: 778bc105-7643-46c4-a338-f3620e31125a
caps.latest.revision: 54
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e8cd602a005026c8dec4bf5a309d6f04044b960d
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51766660"
---
# <a name="vsperfcmd"></a>VSPerfCmd
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A ferramenta **VSPerfCmd.exe** é usada para iniciar e interromper a coleta de dados de desempenho. Ela usa a seguinte sintaxe:  
  
```  
VSPerfCmd [/U] [/options]  
```  
  
 As tabelas a seguir descrevem as opções da ferramenta **VSPerfCmd.exe**.  
  
|Opção|Descrição|  
|------------|-----------------|  
|**U**|Saída de console redirecionada gravada como Unicode. Deve ser a primeira opção especificada.|  
|[Start](../profiling/start.md) **:** `mode`|Inicia o serviço de criação de perfil no modo especificado.|  
|[Output](../profiling/output.md) **:** `filename`|Especifica o nome do arquivo de saída. Use somente com **Start**.|  
|[CrossSession&#124;CS](../profiling/crosssession.md)|Habilita a criação de perfil nas sessões do Windows. Use somente com **Start**, **Attach** **ou Launch**.|  
|[User](../profiling/user-vsperfcmd.md) **:**[`domain\`]`username`|Permite o acesso da conta especificada ao serviço de criador de perfil. Use somente com **Start**.|  
|[WaitStart](../profiling/waitstart.md)[**:**`n`]|Aguarda até o agente coletor de dados inicializar. Se `n` for especificado, a **VSPerfCmd** aguardará no máximo `n` segundos. Se `n` não for especificado, a **VSPerfCmd** aguardará indefinidamente. Isso facilita o uso da **VSPerfCmd** como parte de um processo em lote.|  
|[Counter](../profiling/counter.md) **:** `cfg`|Quando o método de criação de perfil de exemplo é usado, ele especifica um contador de CPU e o número de eventos a serem usados como o intervalo de amostragem. Você pode usar apenas o valor de um contador como amostra.<br /><br /> Quando o método de criação de perfil de instrumentação é usado, especifica um contador de CPU a ser coletado em cada ponto de instrumentação. Use somente com **Start:**`Trace`, **Attach** ou **Launch**.|  
|[QueryCounters](../profiling/querycounters.md)|Exibe uma lista de contadores de CPU válido para a máquina atual.|  
|[WinCounter](../profiling/wincounter.md) **:** *path*|Especifica um evento de contador de desempenho do Windows para incluir com os dados de marca. Use somente com **Start**.|  
|[AutoMark](../profiling/automark.md) **:** *n*|Especifica o intervalo de tempo (em milissegundos) entre os eventos de coleta de dados do contador de desempenho do Windows. Use com **WinCounter**.|  
|[Events](../profiling/events-vsperfcmd.md) **:** `option`|Controla a coleta de eventos especificados do ETW (Rastreamento de Eventos para Windows). Os dados de ETW são coletados em um arquivo .itl que não é o arquivo de dados de criação de perfil (.vsp).|  
|[Status](../profiling/status.md)|Exibe o estado do criador de perfil, informações sobre processos que estão passando pela criação de perfil e contas que possuem autoridade para controlar o criador de perfil.|  
|[Shutdown](../profiling/shutdown.md)[**:**`n`]|Fecha o arquivo de dados de criação de perfil e desativa o criador de perfil.|  
|[GlobalOn](../profiling/globalon-and-globaloff.md)|Retoma a coleta de dados após uma chamada para **VSPerfCmdGlobalOff**.|  
|[GlobalOff](../profiling/globalon-and-globaloff.md)|Interrompe toda coleta de dados, mas não termina a sessão de criação de perfil.|  
|[ProcessOn](../profiling/processon-and-processoff.md) **:** `pid`|Retoma a coleta de dados para o processo especificado após a criação de perfil ser pausada por uma chamada a **VSPerfCmdProcessOff**.|  
|[ProcessOff](../profiling/processon-and-processoff.md) **:** `pid`|Interrompe a coleta de dados do processo especificado.|  
|[ThreadOn e ThreadOff](../profiling/threadon-and-threadoff.md) **:** *tid*|Retoma a criação de perfil do processo especificado após a criação de perfil ser pausada por uma chamada a **VSPerfCmdThreadOff**. Use **ThreadOn** apenas ao criar um perfil com o método de instrumentação.|  
|[ThreadOn e ThreadOff](../profiling/threadon-and-threadoff.md) **:** *tid*|Pausa a criação de perfil do thread especificado. Use **ThreadOff** apenas ao criar um perfil com o método de instrumentação.|  
|[Mark](../profiling/mark.md) **:** _MarkNum_[**,**_MarkText_**]**|Insere uma marca no arquivo de dados de criação de perfil, com texto opcional.|  
  
## <a name="sampling-method-options"></a>Opções do método de amostragem  
 As opções a seguir só estarão disponíveis quando você estiver usando o método de criação de perfil de amostragem.  
  
|Opção|Descrição|  
|------------|-----------------|  
|[Launch](../profiling/launch.md) **:** *Executable*|Inicia o aplicativo especificado e começa a criação de perfil.|  
|[Args](../profiling/args.md) **:** *Arguments*|Especifica argumentos de linha de comando a serem passados para o aplicativo iniciado.|  
|[Console](../profiling/console.md)|Inicia o comando especificado em uma nova janela de prompt de comando.|  
|[Attach](../profiling/attach.md) **:** *PID*[**,**_PID_]|Inicia a criação de perfil dos processos especificados. Os processos podem ser identificados pela id do processo ou pelo nome do processo.|  
|[Detach](../profiling/detach.md)[**:**_PID_[,_PID_]]|Para a criação de perfil dos processos especificados. Os processos podem ser identificados pela id do processo ou pelo nome do processo. Se nenhum processo for especificado, a criação de perfil será interrompida para todos os processos.|  
|[GC](../profiling/gc-vsperfcmd.md)[**:**{**Allocation**`&#124;`**Lifetime**}]|Coleta dados de alocação de memória e de tempo de vida do objeto .NET. Use somente com a opção **VSPerfCmdLaunch**.|  
  
### <a name="sampling-interval-options"></a>Opções do intervalo de amostragem  
 As opções a seguir especificam o tipo e a duração dos intervalos de amostragem. O padrão é **Timer**. Você também pode especificar um contador de CPU como o intervalo usando a opção **Counter**. Essas opções só podem ser especificadas com **Launch** ou com o primeiro **Attach** de uma sessão de criação de perfil.  
  
|Opção|Descrição|  
|------------|-----------------|  
|[PF](../profiling/pf.md)[**:**_n_]|Realiza a amostragem a cada número especificado de falhas de página (padrão=10).|  
|[Sys](../profiling/sys-vsperfcmd.md)[**:**_n_]|Realiza a amostragem a cada número especificado de chamada do sistema (padrão=10).|  
|[Timer](../profiling/timer.md)[**:**_n_]|Realiza a amostragem a cada número especificado de ciclo do processador (padrão=10000000).|  
  
## <a name="service-component-and-kernel-mode-device-options"></a>Opções de componente do serviço e do dispositivo de modo kernel  
 As opções de Administração a seguir oferecem suporte aos componentes do serviço de criação de perfil ou aos drivers de dispositivo de modo kernel. As opções de Administração definem as permissões de criação de perfil e controlam o serviço com perfil criado ou driver de dispositivo.  
  
 As opções de Administração devem ser executadas em um prompt de comando executado com credenciais administrativas.  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Admin:Security** \<**ALLOW&#124;DENY**> *Right*[ *Right*] \<*User*&#124;*Group*>|Permite ou nega o acesso do usuário ou grupo especificado aos serviços de criação de perfil.<br /><br /> `Right` pode ser:<br /><br /> CrossSession - dá ao usuário acesso ao serviço a fim de executar a criação cruzada de perfil.<br /><br /> SampleProfiling - dá ao usuário acesso ao driver para habilitar a criação de perfil de amostragem. Também é usado para acessar informações de transição de kernel durante a criação de perfil de rastreamento.<br /><br /> FullAccess - dá ao usuário acesso ao CrossSession e ao SampleProfiling.|  
|**Admin:Security, List**|Lista o estado atual dos serviços de criação de perfil e lista as permissões de usuário.|  
|**Admin:** \<*Service*&#124;*Driver*>\<**START**&#124;**STOP**&#124;**INSTALL**&#124;**UNINSTALL**>|Inicia, para, instala ou desinstala o componente de serviço de criação de perfil (serviço) ou o driver de dispositivo de modo kernel (driver).|  
|**Admin:** \<*Service*&#124;*Driver*>**AutoStart**\<**ON**&#124;**OFF**>|Habilita ou desabilita a inicialização automática do serviço de criação de perfil (serviço) ou driver de dispositivo de modo kernel (driver) após a reinicialização.|  
  
## <a name="vsperfcmd-driver"></a>VSPerfCmd /Driver  
 A opção **VSPerfCmd /Driver** está obsoleta. Use a opção **VsPerfCmdAdmin** para essa funcionalidade.  
  
## <a name="see-also"></a>Consulte também  
 [VSInstr](../profiling/vsinstr.md)   
 [VSPerfMon](../profiling/vsperfmon.md)   
 [VSPerfReport](../profiling/vsperfreport.md)



