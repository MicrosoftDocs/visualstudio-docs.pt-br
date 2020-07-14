---
title: VSPerfCmd | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- performance tools, VSPerfCmd tool
- command-line tools, VSPerfCmd tool
- command line, tools
- profiling tools,VSPerfCmd
- VSPerfCmd tool
ms.assetid: 778bc105-7643-46c4-a338-f3620e31125a
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: caf145213c41215d518cf42d0a69975c8580e817
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85330012"
---
# <a name="vsperfcmd"></a>VSPerfCmd
A ferramenta *VSPerfCmd.exe* é usada para iniciar e interromper a coleta de dados de desempenho. Ela usa a seguinte sintaxe:

```cmd
VSPerfCmd [/U] [/options]
```

 As tabelas a seguir descrevem as opções da ferramenta *VSPerfCmd.exe*.

|Opção|Descrição|
|------------|-----------------|
|**U**|Saída de console redirecionada gravada como Unicode. Deve ser a primeira opção especificada.|
|[Início](../profiling/start.md) **:**`mode`|Inicia o serviço de criação de perfil no modo especificado.|
|[Saída](../profiling/output.md) **:**`filename`|Especifica o nome do arquivo de saída. Use somente com **Start**.|
|[CrossSession&#124;CS](../profiling/crosssession.md)|Habilita a criação de perfil nas sessões do Windows. Use somente com **Start**, **Attach****ou Launch**.|
|[Usuário](../profiling/user-vsperfcmd.md) **:**[ `domain\` ]`username`|Permite o acesso da conta especificada ao serviço de criador de perfil. Use somente com **Start**.|
|[WaitStart](../profiling/waitstart.md)[**:** `n` ]|Aguarda até o agente coletor de dados inicializar. Se `n` for especificado, a **VSPerfCmd** aguardará no máximo `n` segundos. Se `n` não for especificado, a **VSPerfCmd** aguardará indefinidamente. Isso facilita o uso da **VSPerfCmd** como parte de um processo em lote.|
|[Contador](../profiling/counter.md) **:**`cfg`|Quando o método de criação de perfil de exemplo é usado, ele especifica um contador de CPU e o número de eventos a serem usados como o intervalo de amostragem. Você pode usar apenas o valor de um contador como amostra.<br /><br /> Quando o método de criação de perfil de instrumentação é usado, especifica um contador de CPU a ser coletado em cada ponto de instrumentação. Use somente com **Iniciar:** `Trace` , **anexar**ou **Iniciar**.|
|[QueryCounters](../profiling/querycounters.md)|Exibe uma lista de contadores de CPU válido para a máquina atual.|
|[WinCounter](../profiling/wincounter.md) **:** *caminho*|Especifica um evento de contador de desempenho do Windows para incluir com os dados de marca. Use somente com **Start**.|
|[Automarcar](../profiling/automark.md) **:** *n*|Especifica o intervalo de tempo (em milissegundos) entre os eventos de coleta de dados do contador de desempenho do Windows. Use com **WinCounter**.|
|[Eventos](../profiling/events-vsperfcmd.md) **:**`option`|Controla a coleta de eventos especificados do ETW (Rastreamento de Eventos para Windows). Os dados do ETW são coletados em um arquivo .*itl* que não é o arquivo de dados de criação de perfil (.*vsp*).|
|[Status](../profiling/status.md)|Exibe o estado do criador de perfil, informações sobre processos que estão passando pela criação de perfil e contas que possuem autoridade para controlar o criador de perfil.|
|[Desligamento](../profiling/shutdown.md)[**:** `n` ]|Fecha o arquivo de dados de criação de perfil e desativa o criador de perfil.|
|[GlobalOn](../profiling/globalon-and-globaloff.md)|Retoma a coleta de dados após uma chamada para **VSPerfCmdGlobalOff**.|
|[GlobalOff](../profiling/globalon-and-globaloff.md)|Interrompe toda coleta de dados, mas não termina a sessão de criação de perfil.|
|[Processo](../profiling/processon-and-processoff.md) **:**`pid`|Retoma a coleta de dados para o processo especificado após a criação de perfil ser pausada por uma chamada a **VSPerfCmdProcessOff**.|
|[ProcessOff](../profiling/processon-and-processoff.md) **:**`pid`|Interrompe a coleta de dados do processo especificado.|
|[Threading e ThreadOff](../profiling/threadon-and-threadoff.md) **:** *tid*|Retoma a criação de perfil do processo especificado após a criação de perfil ser pausada por uma chamada a **VSPerfCmdThreadOff**. Use **ThreadOn** apenas ao criar um perfil com o método de instrumentação.|
|[Threading e ThreadOff](../profiling/threadon-and-threadoff.md) **:** *tid*|Pausa a criação de perfil do thread especificado. Use **ThreadOff** apenas ao criar um perfil com o método de instrumentação.|
|[Mark](../profiling/mark.md) **:** _MarkNum_[**,**_MarkText_**]**|Insere uma marca no arquivo de dados de criação de perfil, com texto opcional.|

## <a name="sample-method-options"></a>Opções do método de amostragem
 As opções a seguir só estarão disponíveis quando você estiver usando o método de criação de perfil de amostragem.

|Opção|Descrição|
|------------|-----------------|
|[Iniciar](../profiling/launch.md) **:** *executável*|Inicia o aplicativo especificado e começa a criação de perfil.|
|[Args](../profiling/args.md) **:** *argumentos*|Especifica argumentos de linha de comando a serem passados para o aplicativo iniciado.|
|[Console](../profiling/console.md)|Inicia o comando especificado em uma nova janela de prompt de comando.|
|[Anexar](../profiling/attach.md) **:** *pid*[**,**_pid_]|Inicia a criação de perfil dos processos especificados. Os processos podem ser identificados pela ID ou pelo nome do processo.|
|[Detach](../profiling/detach.md)[**:**_PID_[,_PID_]]|Para a criação de perfil dos processos especificados. Os processos podem ser identificados pela ID ou pelo nome do processo. Se nenhum processo for especificado, a criação de perfil será interrompida para todos os processos.|
|[GC](../profiling/gc-vsperfcmd.md)[**:**{**Allocation**`&#124;`**Lifetime**}]|Coleta dados de alocação de memória e de tempo de vida do objeto .NET. Use somente com a opção **VSPerfCmdLaunch**.|

### <a name="sample-interval-options"></a>Opções do intervalo de amostragem
 As opções a seguir especificam o tipo e a duração dos intervalos de amostragem. O padrão é **Timer**. Você também pode especificar um contador de CPU como o intervalo usando a opção **Counter**. Essas opções só podem ser especificadas com **Launch** ou com o primeiro **Attach** de uma sessão de criação de perfil.

|Opção|Descrição|
|------------|-----------------|
|[PF](../profiling/pf.md)[**:**_n_]|Realiza a amostragem a cada número especificado de falhas de página (padrão=10).|
|[Sys](../profiling/sys-vsperfcmd.md)[**:**_n_]|Realiza a amostragem a cada número especificado de chamada do sistema (padrão=10).|
|[Temporizador](../profiling/timer.md)[**:**_n_]|Realiza a amostragem a cada número especificado de ciclo do processador (padrão=10000000).|

## <a name="service-component-and-kernel-mode-device-options"></a>Opções de componente do serviço e do dispositivo de modo kernel
 As opções de Administração a seguir oferecem suporte aos componentes do serviço de criação de perfil ou aos drivers de dispositivo de modo kernel. As opções de Administração definem as permissões de criação de perfil e controlam o serviço com perfil criado ou driver de dispositivo.

 As opções de Administração devem ser executadas em um prompt de comando executado com credenciais administrativas.

|Opção|Descrição|
|------------|-----------------|
|**Admin: segurança**, \<**ALLOW&#124;DENY**> , *direita*[ *direita*],\<*User*&#124;*Group*>|Permite ou nega o acesso do usuário ou grupo especificado aos serviços de criação de perfil.<br /><br /> `Right` pode ser:<br /><br /> CrossSession - dá ao usuário acesso ao serviço a fim de executar a criação cruzada de perfil.<br /><br /> SampleProfiling - dá ao usuário acesso ao driver para habilitar a criação de perfil de amostragem. Também é usado para acessar informações de transição de kernel durante a criação de perfil de rastreamento.<br /><br /> FullAccess - dá ao usuário acesso ao CrossSession e ao SampleProfiling.|
|**Admin:Security, List**|Lista o estado atual dos serviços de criação de perfil e lista as permissões de usuário.|
|**Administrador:**\<*Service*&#124;*Driver*>\<**START**&#124;**STOP**&#124;**INSTALL**&#124;**UNINSTALL**>|Inicia, para, instala ou desinstala o componente de serviço de criação de perfil (serviço) ou o driver de dispositivo de modo kernel (driver).|
|**Administrador:** \<*Service*&#124;*Driver*> **Inicialização automática**\<**ON**&#124;**OFF**>|Habilita ou desabilita a inicialização automática do serviço de criação de perfil (serviço) ou driver de dispositivo de modo kernel (driver) após a reinicialização.|

## <a name="vsperfcmd-driver"></a>VSPerfCmd /Driver
 A opção **VSPerfCmd /Driver** está obsoleta. Use a opção **VsPerfCmd Admin** para essa funcionalidade.

## <a name="see-also"></a>Veja também
- [VSInstr](../profiling/vsinstr.md)
- [VSPerfMon](../profiling/vsperfmon.md)
- [VSPerfReport](../profiling/vsperfreport.md)
