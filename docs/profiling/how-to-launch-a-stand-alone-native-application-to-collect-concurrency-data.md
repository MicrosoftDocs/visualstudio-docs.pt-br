---
title: Como iniciar um aplicativo nativo autônomo com o criador de perfil para coletar dados de simultaneidade usando a linha de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: e5aed651-afed-4b70-9a7e-1a6032cc614f
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- cplusplus
ms.openlocfilehash: 27c2969286d61738ed059e3973b09843bebc5153
ms.sourcegitcommit: 8d38d5d2f2b75fc1563952c0d6de0fe43af12766
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/26/2018
ms.locfileid: "39277695"
---
# <a name="how-to-launch-a-stand-alone-native-application-with-the-profiler-to-collect-concurrency-data-by-using-the-command-line"></a>Como iniciar um aplicativo nativo autônomo com o criador de perfil para coletar dados de simultaneidade usando a linha de comando
Este tópico descreve como usar ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para iniciar um aplicativo nativo autônomo (cliente) e coletar dados de simultaneidade de thread e processo.  
  
 Uma sessão de criação de perfil tem as seguintes partes:  
  
-   Iniciar o aplicativo com o criador de perfil  
  
-   Controlando a coleta de dados  
  
-   Encerrando a sessão de criação de perfil  
  
> [!NOTE]
>  As ferramentas de linha de comando das Ferramentas de Criação de Perfil estão localizadas no subdiretório *\Team Tools\Performance Tools* do diretório de instalação do [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)]. Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar o criador de perfil em um prompt de comando, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela **Prompt de Comando** ou adicioná-lo ao próprio comando. Para saber mais, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).  
  
## <a name="start-the-application-with-the-profiler"></a>Iniciar o aplicativo com o criador de perfil  
 Para iniciar um aplicativo de destino com o criador de perfil, use as opções [/start](../profiling/vsperfcmd.md) e **/launch** do **VSPerfCmd.exe** para inicializar o Criador de Perfil e iniciar o aplicativo. Você pode especificar **/start** e **/launch** e suas respectivas opções. Você também pode adicionar a opção **/globaloff** para pausar a coleta de dados no início do aplicativo de destino. Depois, você usa **/globalon** para começar a coletar dados.  
  
#### <a name="to-start-an-application-with-the-profiler"></a>Para iniciar um aplicativo com o criador de perfil  
  
1.  Em um prompt de comando, digite o seguinte comando:  
  
     [VSPerfCmd](../profiling/vsperfcmd.md) **/start:concurrency  /output:** `OutputFile` [`Options`]  
  
     A opção [/output](../profiling/output.md)**:**`OutputFile` é necessária com **/start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).  
  
     É possível usar qualquer uma das opções na tabela a seguir com a opção **/start:concurrency**.  
  
    |Opção|Descrição|  
    |------------|-----------------|  
    |[/wincounter](../profiling/wincounter.md) **:** `WinCounterPath`|Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil.|  
    |[/automark](../profiling/automark.md) **:** `Interval`|Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O valor padrão é 500.|  
    |[/events](../profiling/events-vsperfcmd.md) **:** `Config`|Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Eventos de ETW são coletados em um arquivo separado (.etl).|  
  
2.  Inicie o aplicativo de destino digitando:  
  
     **VSPerfCmd**  [/launch](../profiling/launch.md) **:** `AppName` [`Options`]  
  
     É possível usar qualquer uma das opções na tabela a seguir com a opção **/launch**.  
  
    |Opção|Descrição|  
    |------------|-----------------|  
    |[/args](../profiling/args.md) **:** `Arguments`|Especifica uma cadeia de caracteres que contém os argumentos de linha de comando a serem passados para o aplicativo de destino.|  
    |[/console](../profiling/console.md)|Inicia o aplicativo de destino de linha de comando em uma janela separada.|  
    |[/targetclr](../profiling/targetclr.md) **:** `CLRVersion`|Especifica a versão do CLR (Common Language Runtime) a ser analisada se o aplicativo carregar mais de uma versão do CLR.|  
  
## <a name="control-data-collection"></a>Controlar a coleta de dados  
 Durante a execução do aplicativo de destino, você pode controlar a coleta de dados iniciando e parando a gravação de dados no arquivo com opções do *VSPerfCmd.exe*. Controlando a coleta de dados, é possível coletar dados de uma parte específica da execução do programa, como o início ou o desligamento do aplicativo.  
  
#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados  
  
-   Os pares de opções na tabela a seguir iniciam e param a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.  
  
    |Opção|Descrição|  
    |------------|-----------------|  
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|  
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo que a ID de processo (`PID`) especificar.|  
    |[/attach](../profiling/attach.md) **:**{`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[**:**{`PID`&#124;`ProcName`}]|**/attach** começa a coletar dados para o processo que a ID de processo (`PID`) ou o nome de processo (*ProcName*) especificar. **/detach** interrompe a coleta de dados para o processo especificado ou para todos os processos se nenhum processo for especificado.|  
  
-   Também é possível usar a opção **VSPerfCmd.exe**[/mark](../profiling/mark.md) para inserir uma marca de criação de perfil no arquivo de dados. O comando **/mark** adiciona um identificador, um carimbo de data/hora e uma cadeia de caracteres de texto opcional definida pelo usuário. As marcas podem ser usadas para filtrar dados em exibições de dados e relatórios do criador de perfil.  
  
## <a name="end-the-profiling-session"></a>Encerrar a sessão de criação de perfil  
 Para encerrar uma sessão de criação de perfil, o criador de perfil não pode estar coletando dados. Você pode parar a coleta de dados de simultaneidade ao fechar o aplicativo analisado ou ao invocar a opção **VSPerfCmd /detach**. Depois, você invoca a opção **VSPerfCmd /shutdown** para desligar o criador de perfil e fechar o arquivo de dados de criação de perfil.  
  
#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil  
  
1.  Desanexe o criador de perfil do aplicativo de destino fechando-o ou digitando o seguinte comando no prompt de comando:  
  
     **VSPerfCmd /detach**  
  
2.  Desligue o criador de perfil digitando o seguinte comando em um prompt de comando:  
  
     **VSPerfCmd**  [/shutdown](../profiling/shutdown.md)