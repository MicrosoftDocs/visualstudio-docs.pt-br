---
title: Como instrumentar um componente do .NET Framework autônomo e coletar dados de memória com o criador de perfil usando a linha de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d09cc46a-70f5-48f9-aa24-89913e67b359
caps.latest.revision: 32
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: febdaf1396755a05acce2bb8d82cb4af69ed46bc
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51753783"
---
# <a name="how-to-instrument-a-stand-alone-net-framework-component-and-collect-memory-data-with-the-profiler-by-using-the-command-line"></a>Como instrumentar um componente do .NET Framework autônomo e coletar dados de memória com o criador de perfil usando a linha de comando
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico descreve como usar as ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para instrumentar um componente do .NET Framework de um aplicativo autônomo, como um arquivo .exe ou .dll, e coletar informações de memória usando o criador de perfil.  

> [!NOTE]
>  As ferramentas de linha de comando das Ferramentas de Criação de Perfil ficam localizadas no subdiretório \Team Tools\Performance Tools do diretório de instalação do Visual Studio. Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de Prompt de Comando ou adicioná-lo ao próprio comando. Para obter mais informações, consulte [Especificando o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).  

 Para coletar dados de memória de um componente do .NET Framework usando o método de instrumentação, você usa a ferramenta [VSInstr.exe](../profiling/vsinstr.md) para gerar uma versão instrumentada do componente e a ferramenta [VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) para inicializar variáveis de ambiente de criação de perfil. Você inicia o criador de perfil usando a ferramenta **VSPerfCmd.exe**.  

 Quando o componente instrumentado é executado, os dados de memória são automaticamente coletados para um arquivo de dados. Você pode pausar e retomar a coleta de dados durante a sessão de criação de perfil.  

 Para terminar uma sessão de criação de perfil, feche o aplicativo de destino e feche explicitamente o criador de perfil. Na maioria dos casos, recomendamos desmarcar as variáveis de ambiente de criação de perfil no final de uma sessão.  

## <a name="starting-the-application-with-the-profiler"></a>Iniciar o Aplicativo com o Criador de Perfil  

#### <a name="to-attach-the-profiler-to-a-running-net-framework-application"></a>Para anexar o Criador de Perfil a um aplicativo do .NET Framework em execução  

1. Abra uma janela do Prompt de Comando.  

2. Use a ferramenta **VSInstr** para gerar uma versão instrumentada do aplicativo de destino.  

3. Inicialize as variáveis de ambiente de criação de perfil do .NET Framework. Tipo:  

    **VSPerfClrEnv** {**/tracegc** &#124; **/tracegclife**}  

   -   As opções **/tracegc** e **/tracegclife** inicializam as variáveis de ambiente para coletar apenas os dados de alocação de memória ou para coletar os dados de alocação de memória e de tempo de vida do objeto.  

       |Opção|Descrição|  
       |------------|-----------------|  
       |**/tracegc**|Habilita a coleta somente de dados de alocação de memória.|  
       |**/tracegclife**|Habilita a coleta de dados de alocação de memória e de tempo de vida do objeto.|  

4. Inicie o criador de perfil. Tipo:  

    **VSPerfCmd /start:trace /output:** `OutputFile` [`Options`]  

   - A opção [/start](../profiling/start.md)**:trace** inicializa o criador de perfil.  

   - A opção [/output](../profiling/output.md)**:**`OutputFile` é necessária com **/start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).  

     É possível usar qualquer uma das opções a seguir com a opção **/start:trace**.  

   |                                 Opção                                  |                                                                                                                                                Descrição                                                                                                                                                 |
   |-------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | [/user](../profiling/user-vsperfcmd.md) **:**[`Domain`**\\**]`UserName` |            Especifica o domínio e o nome de usuário da conta que possui o processo analisado. Esta opção será necessária apenas se o processo estiver sendo executado como um usuário diferente do usuário conectado. O proprietário do processo é listado na coluna Nome de Usuário na guia Processos do Gerenciador de Tarefas do Windows.             |
   |              [/crosssession](../profiling/crosssession.md)              | Habilita a criação de perfil de processos em outras sessões. Esta opção será necessária se o aplicativo estiver em execução em uma sessão diferente. O identificador da sessão é listado na coluna ID da Sessão na guia Processos do Gerenciador de Tarefas do Windows. **/CS** pode ser especificado como uma abreviação de **/crosssession**. |
   |          [/globaloff](../profiling/globalon-and-globaloff.md)           |                                                                          Para iniciar o criador de perfil com a coleta de dados em pausa, adicione a opção **/globaloff** na linha de comando **/start**. Use **/globalon** para retomar a criação de perfil.                                                                           |
   |    [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath`     |                                                                                                                 Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil.                                                                                                                  |
   |         [/automark](../profiling/automark.md) **:** `Interval`          |                                                                               Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms.                                                                                |
   |           [/counter](../profiling/counter.md) **:** `Config`            |                                                                Coleta informações do contador de desempenho do processador que é especificado na configuração. As informações do contador são adicionadas aos dados que são coletados em cada evento de criação de perfil.                                                                |
   |        [events](../profiling/events-vsperfcmd.md) **:** `Config`        |                                                                                  Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Eventos de ETW são coletados em um arquivo separado (.etl).                                                                                  |


5. Inicie o aplicativo de destino na janela do Prompt de Comando.  

## <a name="controlling-data-collection"></a>Controlando coleção de dados  
 Enquanto o aplicativo de destino estiver em execução, você pode controlar a coleta de dados iniciando e parando a gravação de dados no arquivo usando as opções de **VSPerfCmd.exe**. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como a inicialização ou o desligamento do aplicativo.  

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados  

-   Os pares de opções **VSPerfCmd** a seguir iniciam e interrompem a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.  

    |Opção|Descrição|  
    |------------|-----------------|  
    |[/globalon](../profiling/globalon-and-globaloff.md) [/globaloff](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|  
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pela ID de processo (`PID`).|  
    |[/threadon](../profiling/threadon-and-threadoff.md) **:** `TID` [/threadoff](../profiling/threadon-and-threadoff.md) **:** `TID`|Inicia (**/threadon**) ou interrompe (**/threadoff**) a coleta de dados para o thread especificado pela ID do thread (`TID`).|  

## <a name="ending-the-profiling-session"></a>Encerrando a sessão de criação de perfil  
 Para encerrar uma sessão de criação de perfil, feche o aplicativo que está executando o componente instrumentado e, em seguida, chame a opção **VSPerfCmd** [/shutdown](../profiling/shutdown.md) para desligar o criador de perfil e fechar o arquivo de dados de criação de perfil. O comando **VSPerfClrEnv /off** limpa as variáveis de ambiente da criação de perfil.  

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil  

1.  Feche o aplicativo de destino.  

2.  Desligue o criador de perfil. Tipo:  

     **VSPerfCmd /shutdown**  

3.  (Opcional) desmarcar as variáveis de ambiente de criação de perfil. Tipo:  

     **VSPerfCmd /off**  

## <a name="see-also"></a>Consulte também  
 [Criando perfil de aplicativos autônomos](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [Exibições de dados da memória do .NET](../profiling/dotnet-memory-data-views.md)



