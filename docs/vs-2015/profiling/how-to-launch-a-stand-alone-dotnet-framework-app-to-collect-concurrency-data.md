---
title: Como iniciar um aplicativo do .NET Framework autônomo com o criador de perfil para coletar dados de simultaneidade usando a linha de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 17a48848-bd3e-44ef-9971-e39836ff1df2
caps.latest.revision: 33
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: caed852f51b6e3442274452564f1ef6807d1adec
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51803130"
---
# <a name="how-to-launch-a-stand-alone-net-framework-application-with-the-profiler-to-collect-concurrency-data-by-using-the-command-line"></a>Como iniciar um aplicativo do .NET Framework autônomo com o criador de perfil para coletar dados de simultaneidade usando a linha de comando
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico descreve como usar ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para iniciar um aplicativo autônomo (cliente) do .NET Framework e coletar dados de simultaneidade de thread e processo  

> [!NOTE]
>  As ferramentas de linha de comando das Ferramentas de Criação de Perfil ficam localizadas no subdiretório \Team Tools\Performance Tools do diretório de instalação do [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]. Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de prompt de comando ou adicioná-lo ao próprio comando. Para obter mais informações, consulte [Especificando o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).  

 Enquanto o criador de perfil estiver anexado ao aplicativo, você pode pausar e retomar a coleta de dados. Para concluir uma sessão de criação de perfil, o Criador de perfil não pode mais estar anexado ao aplicativo e o Criador de perfil deve ser desligado explicitamente.  

## <a name="starting-the-application-with-the-profiler"></a>Iniciar o Aplicativo com o Criador de Perfil  
 Para iniciar um aplicativo de destino do .NET Framework com o criador de perfil, use VSPerfClrEnv.exe para definir as variáveis de criação de perfil do .NET Framework. Use as opções **/start** e **/launch** do VSPerfCmd para inicializar o criador de perfil e iniciar o aplicativo. Você pode especificar **/start** e **/launch** e suas opções respectivas em uma única linha de comando. Você também pode adicionar a opção **/globaloff** à linha de comando para pausar a coleta de dados no início do aplicativo de destino. Use **/globalon** em uma linha de comando separada para começar a coletar dados.  

#### <a name="to-start-an-application-with-the-profiler"></a>Para iniciar um aplicativo com o Criador de Perfil  

1. Abra uma janela do prompt de comando.  

2. Inicie o criador de perfil. Tipo:  

    [VSPerfCmd](../profiling/vsperfcmd.md) **/start:concurrency**[**,**{**ResourceOnly**&#124;**ThreadOnly**}] **/output:**`OutputFile` [`Options`]  

   - A opção [/start](../profiling/start.md) inicializa o criador de perfil.  


     |                                     |                                                                        |
     |-------------------------------------|------------------------------------------------------------------------|
     |       **/start:concurrency**        | Permite a coleta de dados de contenção de recursos e de execução do thread. |
     | **/start:concurrency,resourceonly** |           Habilita apenas a coleta de dados de contenção de recursos.            |
     |  **/start:concurrency,threadonly**  |             Habilita apenas a coleta de dados de execução de thread.             |


   - A opção [/output](../profiling/output.md)**:**`OutputFile` é necessária com **/start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).  

     É possível usar qualquer uma das opções a seguir com a opção **/start:concurrency**.  

   |                               Opção                               |                                                                  Descrição                                                                  |
   |--------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
   | [/user](../profiling/user-vsperfcmd.md) **:**[`domain\`]`username` |                       Especifica o domínio e o nome de usuário opcional da conta que receberá acesso ao criador de perfil.                        |
   |           [/crosssession](../profiling/crosssession.md)            |                                            Habilita a criação de perfil de processos em outras sessões de logon.                                            |
   |  [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath`  |                                   Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil.                                   |
   |       [/automark](../profiling/automark.md) **:** `Interval`       | Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms. |
   |     [/events](../profiling/events-vsperfcmd.md) **:** `Config`     |   Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Eventos de ETW são coletados em um arquivo separado (.etl).    |


3. Inicie o aplicativo de destino. Tipo:  

    **VSPerfCmd**  [/launch](../profiling/launch.md) **:** `AppName` [`Options`] [`Sample Event`]  

    É possível usar qualquer uma das opções a seguir com a opção **/launch**.  

   |Opção|Descrição|  
   |------------|-----------------|  
   |[/args](../profiling/args.md) **:** `Arguments`|Especifica uma cadeia de caracteres que contém os argumentos de linha de comando a serem passados para o aplicativo de destino.|  
   |[/console](../profiling/console.md)|Inicia o aplicativo de destino de linha de comando em uma janela separada.|  
   |[/targetclr](../profiling/targetclr.md) **:** `Version`|Especifica a versão do CLR (Common Language Runtime) a ser analisada quando mais de uma versão de tempo de execução for carregada em um aplicativo.|  

## <a name="controlling-data-collection"></a>Controlando coleção de dados  
 Enquanto o aplicativo de destino estiver em execução, você pode controlar a coleta de dados iniciando e parando a gravação de dados no arquivo usando as opções de VSPerfCmd.exe. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como o início ou o desligamento do aplicativo.  

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados  

1.  Os pares de opções de VSPerfCmd.exe a seguir iniciam e interrompem a coleta de dados. Especifica cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.  

    |Opção|Descrição|  
    |------------|-----------------|  
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|  
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pela ID de processo (`PID`).|  
    |[/attach](../profiling/attach.md) **:**{`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[**:**{`PID`&#124;`ProcName`}]|**/attach** começa a coletar dados para o processo especificado pela ID de processo (`PID`) ou pelo nome de processo (ProcName). **/detach** interrompe a coleta de dados para o processo especificado ou para todos os processos se nenhum processo específico for especificado.|  

## <a name="ending-the-profiling-session"></a>Encerrando a sessão de criação de perfil  
 Para encerrar uma sessão de criação de perfil, o criador de perfil não pode estar coletando dados. Você pode parar a coleta de dados de simultaneidade ao fechar o aplicativo analisado ou ao invocar a opção **VSPerfCmd /detach**. Depois, você invoca a opção **VSPerfCmd /shutdown** para desligar o criador de perfil e fechar o arquivo de dados de criação de perfil. O comando **VSPerfClrEnv /off** limpa as variáveis de ambiente da criação de perfil.  

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil  

1.  Siga um destes procedimentos para desanexar o criador de perfil do aplicativo de destino.  

    -   Feche o aplicativo de destino.  

         -ou-  

    -   Digite **VSPerfCmd /detach**  

2.  Desligue o criador de perfil  

     **VSPerfCmd**  [/shutdown](../profiling/shutdown.md)  

## <a name="see-also"></a>Consulte também  
 [Coleta de Dados de Simultaneidade](../profiling/collecting-concurrency-data-for-stand-alone-applications-by-using-the-profiler-command-line.md)



