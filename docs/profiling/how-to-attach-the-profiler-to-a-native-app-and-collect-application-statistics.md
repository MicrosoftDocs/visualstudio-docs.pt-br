---
title: Como anexar o criador de perfil a um aplicativo autônomo nativo e coletar estatísticas do aplicativo usando a linha de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: df44fe42-281b-4398-b3fc-277b62ae41f1
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- cplusplus
ms.openlocfilehash: cfe5e6f0bcdf84d3ef91933ff2c754cf0fc52bdf
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49842034"
---
# <a name="how-to-attach-the-profiler-to-a-native-stand-alone-application-and-collect-application-statistics-by-using-the-command-line"></a>Como anexar o criador de perfil a um aplicativo independente nativo e coletar estatísticas do aplicativo usando a linha de comando
Este artigo descreve como usar as ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para anexar o criador de perfil a um aplicativo (cliente) independente nativo em execução e coletar estatísticas de desempenho usando o método de amostragem.  

> [!NOTE]
>  Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos UWP também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).  
> 
> [!NOTE]
>  As ferramentas de linha de comando das Ferramentas de Criação de Perfil estão localizadas no subdiretório *\Team Tools\Performance Tools* do diretório de instalação do [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)]. Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de Prompt de Comando ou adicioná-lo ao próprio comando. Para obter mais informações, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).  

 Quando criador de perfil estiver anexado ao aplicativo, você poderá pausar e retomar a coleta de dados. Para concluir uma sessão de criação de perfil, o Criador de perfil não pode mais estar anexado ao aplicativo e o Criador de perfil deve ser desligado explicitamente.  

## <a name="attach-the-profiler"></a>Anexar o criador de perfil  
 Para anexar o criador de perfil a um aplicativo de destino usando o criador de perfil, use as opções **VSPerfCmd/start** e **/attach** para inicializar o criador de perfil e anexá-lo ao aplicativo de destino. Você pode especificar **/start** e **/attach** e suas opções respectivas em uma única linha de comando. Você também pode adicionar a opção **/globaloff** para pausar a coleta de dados no início do aplicativo de destino. Depois, você usa **/globalon** para começar a coletar dados.  

#### <a name="to-attach-the-profiler-to-a-running-net-framework-application"></a>Para anexar o Criador de Perfil a um aplicativo do .NET Framework em execução  

1. Abra uma janela do Prompt de Comando.  

2. Inicie o criador de perfil. Tipo:  

    **VSPerfCmd /start:sample /output:** `OutputFile` [`Options`]  

   - A opção [/start](../profiling/start.md)**:sample** inicializa o criador de perfil.  

   - A opção [/output](../profiling/output.md)**:**`OutputFile` é necessária com **/start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).  

     É possível usar qualquer uma das opções a seguir com a opção **/start:sample**.  

   | Opção | Descrição |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:**[`Domain`**\\**]`UserName` | Especifica o domínio e o nome de usuário da conta que possui o processo analisado. Esta opção será necessária apenas se o processo estiver sendo executado como um usuário diferente do usuário conectado. O proprietário do processo é listado na coluna Nome de Usuário na guia Processos do Gerenciador de Tarefas do Windows. |
   | [/crosssession](../profiling/crosssession.md) | Habilita a criação de perfil de processos em outras sessões. Esta opção será necessária se o aplicativo ASP.NET estiver em execução em uma sessão diferente. O identificador da sessão é listado na coluna ID da Sessão na guia Processos do Gerenciador de Tarefas do Windows. **/CS** pode ser especificado como uma abreviação de **/crosssession**. |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil. |
   | [/automark](../profiling/automark.md) **:** `Interval` | Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms. |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Os eventos do ETW são coletados em um arquivo separado (.*etl*). |


3. Anexe o criador de perfil ao aplicativo de destino. Tipo:  

    **VSPerfCmd**  [/attach](../profiling/attach.md) **:**{`PID`&#124;`ProcName`} [`Sample Event`]  

    `PID` especifica a ID do processo ou o nome do aplicativo de destino. `ProcessName` especifica o nome do processo. Observe que, se você especificar `ProcessName` e vários processos que têm o mesmo nome estiverem em execução, os resultados serão imprevisíveis. É possível exibir as IDs de processo de todos os processos em execução no Gerenciador de Tarefas do Windows.  

    Por padrão, os dados de desempenho têm amostra obtida a cada 10.000.000 ciclos de relógio de processador não interrompidos. Significa aproximadamente 100 vezes por segundo em um processador 1GH. Você pode especificar uma das opções a seguir para alterar o intervalo de ciclo de relógio ou especificar um evento de amostragem diferente.  

   |Evento de amostra|Descrição|  
   |------------------|-----------------|  
   |[/timer](../profiling/timer.md) **:** `Interval`|Altera o intervalo de amostragem para o número de ciclos de relógio não interrompidos especificados pelo `Interval`.|  
   |[/pf](../profiling/pf.md)[**:**`Interval`]|Altera o evento de amostragem para falhas de página. Se `Interval` for especificado, define o número de falhas de página entre as amostras. O padrão é 10.|  
   |[/sys](../profiling/sys-vsperfcmd.md) [**:**`Interval`]|Altera o evento de amostragem para chamadas do sistema do processo para o kernel do sistema operacional (syscalls). Se `Interval` for especificado, define o número de chamadas entre as amostras. O padrão é 10.|  
   |[/counter](../profiling/counter.md) **:** `Config`|Altera o evento de amostragem e o intervalo para o contador de desempenho do processador e o intervalo especificado em `Config`.|  

## <a name="control-data-collection"></a>Controlar a coleta de dados  
 Durante a execução do aplicativo de destino, use as opções do *VSPerfCmd.exe* para iniciar e parar a gravação de dados no arquivo de dados do criador de perfil. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como o início ou o desligamento do aplicativo.  

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados  

-   Os pares de opções **VSPerfCmd** a seguir iniciam e interrompem a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.  

    |Opção|Descrição|  
    |------------|-----------------|  
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|  
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado por `PID`.|  
    |[/attach](../profiling/attach.md) **:** `PID` [/detach](../profiling/detach.md)|**/attach** começa a coletar dados do processo especificado por `PID`. **/detach** interrompe a coleta de dados para todos os processos.|  

## <a name="end-the-profiling-session"></a>Encerrar a sessão de criação de perfil  
 Para concluir uma sessão de criação de perfil, o criador de perfil deve ser desanexado de todos os processos analisados e o criador de perfil deve ser desligado explicitamente. É possível desanexar o criador de perfil de um aplicativo que foi analisado usando o método de amostragem ao fechar o aplicativo ou chamar a opção **VSPerfCmd /detach**. Depois, chame a opção **VSPerfCmd /shutdown** para desativar o criador de perfil e fechar o arquivo de dados de criação de perfil. O comando **VSPerfClrEnv /off** limpa as variáveis de ambiente da criação de perfil.  

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil  

1.  Execute uma das etapas a seguir para desanexar o criador de perfil do aplicativo de destino.  

    -   Digite **VSPerfCmd /detach**  

         -ou-  

    -   Feche o aplicativo de destino.  

2.  Desligue o criador de perfil. Tipo:  

     **VSPerfCmd**  [/shutdown](../profiling/shutdown.md)  

3.  (Opcional) desmarcar as variáveis de ambiente de criação de perfil. Tipo:  

     **VSPerfClrEnv /off**  

## <a name="see-also"></a>Consulte também  
 [Criar perfil de aplicativos autônomos](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [Exibições de dados do método de amostragem](../profiling/profiler-sampling-method-data-views.md)