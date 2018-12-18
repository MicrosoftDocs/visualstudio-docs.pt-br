---
title: Como anexar o criador de perfil a um aplicativo autônomo do .NET Framework para coletar dados de simultaneidade usando a linha de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: fdd41576-797e-4312-8520-fee7bb767e4a
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: f727e2a06fa2e5798de84c7b6ee6d97bfb2a4558
ms.sourcegitcommit: 1b9c1e333c2f096d35cfc77e846116f8e5054557
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34815279"
---
# <a name="how-to-attach-the-profiler-to-a-net-framework-stand-alone-application-to-collect-concurrency-data-by-using-the-command-line"></a>Como anexar o criador de perfil a um aplicativo .NET Framework independente para coletar dados de simultaneidade usando a linha de comando
Este artigo descreve como usar as ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para anexar o criador de perfil a um aplicativo (cliente) .NET Framework independente em execução e coletar dados de simultaneidade de thread e do processo.  
  
> [!NOTE]
>  As ferramentas de linha de comando das Ferramentas de Criação de Perfil estão localizadas no subdiretório *\Team Tools\Performance Tools* do diretório de instalação do [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)]. Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar as ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de prompt de comando ou adicioná-lo ao próprio comando. Para saber mais, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).  
  
 Enquanto o criador de perfil estiver anexado ao aplicativo, você pode pausar e retomar a coleta de dados. Para encerrar uma sessão de criação de perfil, o criador de perfil não deve mais estar anexado ao aplicativo e precisa ser desligado explicitamente.  
  
## <a name="attach-the-profiler"></a>Anexar o criador de perfil  
  
#### <a name="to-attach-the-profiler-to-a-running-net-framework-application"></a>Para anexar o Criador de Perfil a um aplicativo do .NET Framework em execução  
  
1.  Abra uma janela do prompt de comando.  
  
2.  Inicie o criador de perfil. Tipo:  
  
     [VSPerfCmd](../profiling/vsperfcmd.md) **/start:concurrency  /output:** `OutputFile` [`Options`]  
  
     A opção [/output](../profiling/output.md)**:**`OutputFile` é necessária com **/start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).  
  
     É possível usar qualquer uma das opções a seguir com a opção **/start:concurrency**.  
  
    |Opção|Descrição|  
    |------------|-----------------|  
    |[/wincounter](../profiling/wincounter.md) **:** `WinCounterPath`|Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil.|  
    |[/automark](../profiling/automark.md) **:** `Interval`|Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms.|  
    |[/events](../profiling/events-vsperfcmd.md) **:** `Config`|Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Eventos de ETW são coletados em um arquivo separado (.etl).|  
  
3.  Inicie o aplicativo de destino normalmente.  
  
4.  Anexe o criador de perfil ao aplicativo de destino. Tipo:  
  
     **VSPerfCmd /attach:** `PID` [**/lineoff**] [**/targetclr:**`Version`]  
  
    -   `PID` especifica a ID do processo ou o nome do aplicativo de destino. É possível exibir as IDs de processo de todos os processos em execução no Gerenciador de Tarefas do Windows.  
  
    -   [/lineoff](../profiling/lineoff.md) desabilita a coleta de dados de número de linha.  
  
    -   [/targetclr](../profiling/targetclr.md) **:** `Version` especifica a versão do CLR (Common Language Runtime) cujo perfil deverá ser criado quando mais de uma versão do tempo de execução for carregada em um aplicativo. Opcional.  
  
## <a name="control-data-collection"></a>Controlar a coleta de dados  
 Enquanto o aplicativo de destino estiver em execução, você pode controlar a coleta de dados iniciando e parando a gravação de dados no arquivo usando as opções de *VSPerfCmd.exe*. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como o início ou o desligamento do aplicativo.  
  
#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados  
  
-   Os pares de opções do *VSPerfCmd.exe* a seguir iniciam e interrompem a coleta de dados. Especifica cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.  
  
    |Opção|Descrição|  
    |------------|-----------------|  
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|  
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pela ID de processo (`PID`).|  
    |[/attach](../profiling/attach.md) **:**{`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[**:**{`PID`&#124;`ProcName`}]|**/attach** começa a coletar dados para o processo especificado pela ID de processo (`PID`) ou pelo nome de processo (ProcName). **/detach** interrompe a coleta de dados para o processo especificado ou para todos os processos se nenhum processo específico for especificado.|  
  
## <a name="end-the-profiling-session"></a>Encerrar a sessão de criação de perfil  
 Para encerrar uma sessão de criação de perfil, o criador de perfil não pode estar coletando dados. É possível interromper a coleta de dados de um aplicativo analisado com o método de simultaneidade fechando o aplicativo ou invocando a opção **VSPerfCmd /detach**. Depois, invoque a opção **VSPerfCmd /shutdown** para desativar o criador de perfil e fechar o arquivo de dados de criação de perfil. O comando **VSPerfClrEnv /off** limpa as variáveis de ambiente da criação de perfil.  
  
#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil  
  
1.  Siga um destes procedimentos para desanexar o criador de perfil do aplicativo de destino.  
  
    -   Digite **VSPerfCmd /detach**  
  
         -ou-  
  
    -   Feche o aplicativo de destino.  
  
2.  Desligue o criador de perfil. Tipo:  
  
     VSPerfCmd[/shutdown](../profiling/shutdown.md)
