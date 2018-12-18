---
title: Como anexar o criador de perfil a um aplicativo autônomo do .NET Framework para coletar dados de simultaneidade usando a linha de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fdd41576-797e-4312-8520-fee7bb767e4a
caps.latest.revision: 34
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f0523b367ec00dd7551dcf30f5002d855a99bf79
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51790403"
---
# <a name="how-to-attach-the-profiler-to-a-net-framework-stand-alone-application-to-collect-concurrency-data-by-using-the-command-line"></a>Como anexar o criador de perfil a um aplicativo autônomo do .NET Framework para coletar dados de simultaneidade usando a linha de comando
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico descreve como usar as Ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para anexar o Criador de perfil a um aplicativo autônomo (cliente) .NET Framework em execução e coletar dados de simultaneidade de aplicativo e de thread.  
  
> [!NOTE]
>  As ferramentas de linha de comando das Ferramentas de Criação de Perfil ficam localizadas no subdiretório \Team Tools\Performance Tools do diretório de instalação do [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]. Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar as ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de prompt de comando ou adicioná-lo ao próprio comando. Para obter mais informações, consulte [Especificando o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).  
  
 Enquanto o criador de perfil estiver anexado ao aplicativo, você pode pausar e retomar a coleta de dados. Para concluir uma sessão de criação de perfil, o Criador de perfil não pode mais estar anexado ao aplicativo e o Criador de perfil deve ser desligado explicitamente.  
  
## <a name="attaching-the-profiler"></a>Anexando o Criador de perfil  
  
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
  
## <a name="controlling-data-collection"></a>Controlando coleção de dados  
 Enquanto o aplicativo de destino estiver em execução, você pode controlar a coleta de dados iniciando e parando a gravação de dados no arquivo usando as opções de VSPerfCmd.exe. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como o início ou o desligamento do aplicativo.  
  
#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados  
  
-   Os pares de opções de VSPerfCmd.exe a seguir iniciam e interrompem a coleta de dados. Especifica cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.  
  
    |Opção|Descrição|  
    |------------|-----------------|  
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|  
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pela ID de processo (`PID`).|  
    |[/attach](../profiling/attach.md) **:**{`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[**:**{`PID`&#124;`ProcName`}]|**/attach** começa a coletar dados para o processo especificado pela ID de processo (`PID`) ou pelo nome de processo (ProcName). **/detach** interrompe a coleta de dados para o processo especificado ou para todos os processos se nenhum processo específico for especificado.|  
  
## <a name="ending-the-profiling-session"></a>Encerrando a sessão de criação de perfil  
 Para encerrar uma sessão de criação de perfil, o criador de perfil não pode estar coletando dados. É possível interromper a coleta de dados de um aplicativo analisado com o método de simultaneidade fechando o aplicativo ou invocando a opção **VSPerfCmd /detach**. Depois, invoque a opção **VSPerfCmd /shutdown** para desativar o criador de perfil e fechar o arquivo de dados de criação de perfil. O comando **VSPerfClrEnv /off** limpa as variáveis de ambiente da criação de perfil.  
  
#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil  
  
1.  Siga um destes procedimentos para desanexar o criador de perfil do aplicativo de destino.  
  
    -   Digite **VSPerfCmd /detach**  
  
         -ou-  
  
    -   Feche o aplicativo de destino.  
  
2.  Desligue o criador de perfil. Tipo:  
  
     VSPerfCmd[/shutdown](../profiling/shutdown.md)



