---
title: Como anexar o Criador de perfil a um serviço nativo para coletar estatísticas do aplicativo usando a linha de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f783817f-77a0-4eb8-985b-ec3b77eadc42
caps.latest.revision: 30
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3677f252fc4c7b415173bf7e1c39c459b7c00b9c
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51740932"
---
# <a name="how-to-attach-the-profiler-to-a-native-service-to-collect-application-statistics-by-using-the-command-line"></a>Como anexar o criador de perfil a um serviço nativo para coletar estatísticas do aplicativo usando a linha de comando
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico descreve como usar as Ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para anexar o criador de perfil a um serviço nativo e coletar estatísticas de desempenho usando o método de amostragem.  

> [!NOTE]
>  Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos da Windows Store também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).  

> [!NOTE]
>  As ferramentas de linha de comando das Ferramentas de Criação de Perfil ficam localizadas no subdiretório \Team Tools\Performance Tools do diretório de instalação do [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]. Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de prompt de comando ou adicioná-lo ao próprio comando. Para obter mais informações, consulte [Especificando o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).  

 Enquanto o criador de perfil estiver anexado ao serviço, você pode pausar e retomar a coleta de dados.  

 Para concluir uma sessão de criador de perfil, o criador de perfil deve ser desanexado do serviço e desligado explicitamente.  

## <a name="starting-the-application-with-the-profiler"></a>Iniciar o Aplicativo com o Criador de Perfil  
 Para anexar o criador de perfil a um serviço nativo, use as opções **VSPerfCmd.exe**[/start](../profiling/start.md) e [/attach](../profiling/attach.md) para inicializar o criador de perfil e anexá-lo ao aplicativo de destino. Você pode especificar **/start** e **/attach** e suas opções respectivas em uma única linha de comando. Você também pode adicionar a opção [/globaloff](../profiling/globalon-and-globaloff.md) para pausar a coleta de dados no início do aplicativo de destino. Use [/globalon](../profiling/globalon-and-globaloff.md) para começar a coletar os dados.  

#### <a name="to-attach-the-profiler-to-a-native-service"></a>Para anexar o Criador de perfil a um serviço nativo  

1. Se necessário, inicie o serviço.  

2. Abra uma janela do prompt de comando.  

3. Inicie o criador de perfil. Tipo:  

    **VSPerfCmd /start:sample**  [/output](../profiling/output.md) **:** `OutputFile` [`Options`]  

   - A opção **/start:sample** inicializa o criador de perfil.  

   - A opção **/output:**`OutputFile` é necessária com **/start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).  

     É possível usar qualquer uma das opções a seguir com a opção **/start:sample**.  

   > [!NOTE]
   >  Normalmente, as opções **/user** e **/crosssession** são necessárias para serviços.  

   |                                 Opção                                  |                                                                                                                                            Descrição                                                                                                                                             |
   |-------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | [/user](../profiling/user-vsperfcmd.md) **:**[`Domain`**\\**]`UserName` |        Especifica o domínio e o nome de usuário da conta que possui o processo analisado. Esta opção é necessária apenas se o processo estiver sendo executado como um usuário diferente do usuário conectado. O proprietário do processo é listado na coluna Nome de Usuário na guia Processos do Gerenciador de Tarefas do Windows.         |
   |              [/crosssession](../profiling/crosssession.md)              | Habilita a criação de perfil de processos em outras sessões. Esta opção será necessária se o aplicativo estiver em execução em uma sessão diferente. A ID da sessão é listada na coluna ID da Sessão na guia Processos do Gerenciador de Tarefas do Windows. **/CS** pode ser especificado como uma abreviação de **/crosssession**. |
   |    [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath`     |                                                                                                             Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil.                                                                                                              |
   |         [/automark](../profiling/automark.md) **:** `Interval`          |                                                                           Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms.                                                                            |
   |       [/events](../profiling/events-vsperfcmd.md) **:** `Config`        |                                                                              Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Eventos de ETW são coletados em um arquivo separado (.etl).                                                                              |


4. Anexe o criador de perfil ao serviço. Tipo:  

    **VSPerfCmd /attach:** `PID` [`Sample Event`]  

    `PID` especifica a ID do processo ou o nome do aplicativo de destino. É possível exibir as IDs de processo de todos os processos em execução no Gerenciador de Tarefas do Windows.  

    Por padrão, os dados de desempenho têm amostra obtida a cada 10.000.000 ciclos de relógio de processador não interrompidos. Significa aproximadamente uma vez a cada 10 segundos em um processador de 1GH. Você pode especificar uma das opções a seguir para alterar o intervalo de ciclo de relógio ou especificar um evento de amostragem diferente.  

   |Evento de Amostra|Descrição|  
   |------------------|-----------------|  
   |[/timer](../profiling/timer.md) **:** `Interval`|Altera o intervalo de amostragem para o número de ciclos de relógio não interrompidos especificados por `Interval`.|  
   |[/pf](../profiling/pf.md)[**:**`Interval`]|Altera o evento de amostragem para falhas de página. Se `Interval` for especificado, define o número de falhas de página entre as amostras. O padrão é 10.|  
   |[/sys](../profiling/sys-vsperfcmd.md) [**:**`Interval`]|Altera o evento de amostragem para chamadas do sistema do processo para o kernel do sistema operacional (syscalls). Se `Interval` for especificado, define o número de chamadas entre as amostras. O padrão é 10.|  
   |[/counter](../profiling/counter.md) **:** `Config`|Altera o evento de amostragem e o intervalo para o contador de desempenho do processador e o intervalo especificado em `Config`.|  

## <a name="controlling-data-collection"></a>Controlando coleção de dados  
 Quando o serviço estiver em execução, você poderá usar as opções **VSPerfCmd.exe** para iniciar e parar a gravação de dados para o arquivo de dados do criador de perfil. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como a inicialização ou o desligamento do aplicativo.  

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados  

-   Os pares de opções **VSPerfCmd** a seguir iniciam e interrompem a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.  

    |Opção|Descrição|  
    |------------|-----------------|  
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|  
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pela ID de processo (`PID`).|  
    |**/attach:** {`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[:{`PID`&#124;`ProcName`}]|**/attach** começa a coletar dados para o processo especificado pela ID de processo ou pelo nome de processo. **/detach** interrompe a coleta de dados para o processo especificado ou para todos os processos se nenhum processo for especificado.|  

## <a name="ending-the-profiling-session"></a>Encerrando a sessão de criação de perfil  
 Para concluir uma sessão de criação de perfil, o criador de perfil deve ser desanexado do serviço e desligado explicitamente. É possível desanexar o serviço nativo analisado com o método de amostragem interrompendo o serviço ou chamando a opção **VSPerfCmd /detach**. Em seguida, chame a opção **VSPerfCmd** [/shutdown](../profiling/shutdown.md) para desativar o criador de perfil e fechar o arquivo de dados de criação de perfil.  

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil  

1.  Siga um destes procedimentos para desanexar o criador de perfil do aplicativo de destino:  

    -   Pare o serviço.  

         -ou-  

    -   Digite **VSPerfCmd /detach**  

2.  Desligue o criador de perfil. Tipo:  

     **VSPerfCmd /shutdown**  

## <a name="see-also"></a>Consulte também  
 [Serviços de Criação de Perfil](../profiling/command-line-profiling-of-services.md)   
 [Exibições de dados do método de amostragem](../profiling/profiler-sampling-method-data-views.md)



