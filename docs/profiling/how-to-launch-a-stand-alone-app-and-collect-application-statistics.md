---
title: Como inicializar um aplicativo autônomo com o criador de perfil e coletar estatísticas de aplicativo usando a linha de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 52dcee2b-f178-4a76-bddc-e36c50bfcb78
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: a57d56564b7be9051efb1a5d153a2a797fcc2211
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49819999"
---
# <a name="how-to-launch-a-stand-alone-application-with-the-profiler-and-collect-application-statistics-by-using-the-command-line"></a>Como iniciar um aplicativo autônomo com o criador de perfil e coletar estatísticas do aplicativo usando a linha de comando
Este tópico descreve como usar as ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para iniciar um aplicativo autônomo (cliente) e coletar estatísticas de desempenho usando o método de amostragem.  

> [!NOTE]
>  Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos UWP também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).  
>   
>  A adição de dados de interação de camada a uma execução de criação de perfil requer procedimentos específicos com ferramentas de criação de perfil de linha de comando. Confira [Coletar dados de interação de camada](../profiling/adding-tier-interaction-data-from-the-command-line.md)  

 Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho à variável de ambiente PATH da janela de Prompt de Comando ou adicioná-lo ao próprio comando. Você pode executar as ferramentas de criação de perfil em um computador em que o Visual Studio está instalado de uma janela Comando do Visual Studio.  

1.  Se você estiver executando as ferramentas de criação de perfil em um computador no qual o Visual Studio está instalado, uma janela Comando do Visual Studio definirá os caminhos corretos. No menu **Ferramentas**, escolha **Prompt de comando do VS**  

> [!NOTE]
>  As ferramentas de linha de comando das Ferramentas de Criação de Perfil estão localizadas no subdiretório *\Team Tools\Performance Tools* do diretório de instalação do Visual Studio. Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho à variável de ambiente PATH da janela de Prompt de Comando ou adicioná-lo ao próprio comando. Para saber mais, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).  

## <a name="start-the-application-with-the-profiler"></a>Iniciar o aplicativo com o criador de perfil  
 Para iniciar um aplicativo de destino usando o criador de perfil, use as opções **/start** e **/launch** do VSPerfCmd para inicializar o criador de perfil e iniciar o aplicativo. Você pode especificar **/start** e **/launch** e suas opções respectivas em uma única linha de comando.  

 Você também pode adicionar a opção **/globaloff** para pausar a coleta de dados no início do aplicativo de destino. Depois, você usa **/globalon** para começar a coletar dados.  

#### <a name="to-start-an-application-by-using-the-profiler"></a>Para iniciar um aplicativo usando o criador de perfil  

1. Abra uma janela do Prompt de Comando.  

2. Inicie o criador de perfil. Tipo:  

    **VSPerfCmd /start:sample /output:** `OutputFile` [`Options`]  

   - A opção [/start](../profiling/start.md)**:sample** inicializa o criador de perfil.  

   - A opção [/output](../profiling/output.md)**:**`OutputFile` é necessária com **/start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).  

     É possível usar qualquer uma das opções a seguir com a opção **/start:sample**.  

   | Opção | Descrição |
   | - | - |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil. |
   | [/automark](../profiling/automark.md) **:** `Interval` | Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms. |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Os eventos do ETW são coletados em um arquivo separado (.*etl*). |


3. Inicie o aplicativo de destino. Type:**VSPerfCmd /launch:**`appName` [`Options`] [`Sample Event`]  

    Você pode usar uma ou mais das opções a seguir com a opção **/launch**.  

   |Opção|Descrição|  
   |------------|-----------------|  
   |[/args](../profiling/args.md) **:** `Arguments`|Especifica uma cadeia de caracteres que contém os argumentos de linha de comando a serem passados para o aplicativo de destino.|  
   |[/console](../profiling/console.md)|Inicia o aplicativo de destino de linha de comando em uma janela separada.|  

    Por padrão, os dados de desempenho têm amostra obtida a cada 10.000.000 ciclos de relógio de processador não interrompidos. Isso é aproximadamente uma vez a cada 10 segundos em um processador de 1 GHz. Você pode especificar uma das opções a seguir para alterar o intervalo de ciclo de relógio ou especificar um evento de amostragem diferente.  

   |Evento de amostra|Descrição|  
   |------------------|-----------------|  
   |[/timer](../profiling/timer.md) **:** `Interval`|Altera o intervalo de amostragem para o número de ciclos de relógio não interrompidos especificados pelo `Interval`.|  
   |[/pf](../profiling/pf.md)[**:**`Interval`]|Altera o evento de amostragem para falhas de página. Se `Interval` for especificado, define o número de falhas de página entre as amostras. O padrão é 10.|  
   |[/sys](../profiling/sys-vsperfcmd.md)[**:**`Interval`]|Altera o evento de amostragem para chamadas do sistema do processo para o kernel do sistema operacional (syscalls). Se `Interval` for especificado, define o número de chamadas entre as amostras. O padrão é 10.|  
   |[/counter](../profiling/counter.md) **:** `Config`|Altera o evento de amostragem e o intervalo para o contador de desempenho do processador e o intervalo especificado em `Config`.|  

## <a name="control-data-collection"></a>Controlar a coleta de dados  
 Quando o aplicativo de destino estiver em execução, você pode controlar a coleta de dados iniciando e interrompendo a gravação de dados no arquivo de dados do criador de perfil usando as opções do *VSPerfCmd.exe*. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como a inicialização ou o desligamento do aplicativo.  

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados  

-   Os pares de opções a seguir iniciam e interrompem a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.  

    |Opção|Descrição|  
    |------------|-----------------|  
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|  
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID`  [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pela ID de processo (`PID`).|  
    |[/attach](../profiling/attach.md) **:**{`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[**:**{`PID`&#124;`ProcName`}]|**/attach** começa a coletar dados para o processo especificado por `PID` ou pelo nome de processo (ProcName). **/detach** interrompe a coleta de dados para o processo especificado ou para todos os processos se nenhum processo específico for especificado.|  

## <a name="end-the-profiling-session"></a>Encerrar a sessão de criação de perfil  
 Para concluir uma sessão de criação de perfil, o criador de perfil não deve estar anexado a nenhum processo analisado e o criador de perfil deve ser desligado explicitamente. É possível desanexar o criador de perfil de um aplicativo que foi analisado usando o método de amostragem ao fechar o aplicativo ou chamar a opção **VSPerfCmd /detach**. Depois, chame a opção **VSPerfCmd /shutdown** para desativar o criador de perfil e fechar o arquivo de dados de criação de perfil. O comando **VSPerfClrEnv /off** limpa as variáveis de ambiente da criação de perfil.  

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil  

1.  Realize uma das etapas a seguir para desanexar o criador de perfil do aplicativo de destino:  

    -   Feche o aplicativo de destino.  

         -ou-  

    -   Digite **VSPerfCmd /detach**  

2.  Desligue o criador de perfil. Tipo:  

     **VSPerfCmd**  [/shutdown](../profiling/shutdown.md)  

## <a name="see-also"></a>Consulte também  
 [Criar perfil de aplicativos autônomos](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [Exibições de dados do método de amostragem](../profiling/profiler-sampling-method-data-views.md)