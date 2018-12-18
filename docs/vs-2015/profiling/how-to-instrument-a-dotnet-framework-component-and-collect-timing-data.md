---
title: Como instrumentar um componente do .NET Framework autônomo e coletar dados de tempo com o criador de perfil por meio da linha de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b7dcc27b-45c6-4302-9552-6fa5b1e94b56
caps.latest.revision: 33
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 857818dac0b1cf1cd394d69aa322d9c2a0bbbe77
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51810138"
---
# <a name="how-to-instrument-a-stand-alone-net-framework-component-and-collect-timing-data-with-the-profiler-from-the-command-line"></a>Como instrumentar um componente do .NET Framework autônomo e coletar dados de tempo com o criador de perfil a partir da linha de comando
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico descreve como usar as ferramentas da linha de comando das Ferramentas de criação de perfil do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para instrumentar um componente do .NET Framework, como um arquivo .exe ou .dll, e coletar dados detalhados de tempo.  

> [!NOTE]
>  Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos da Windows Store também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).  
>   
>  As ferramentas de linha de comando das Ferramentas de Criação de Perfil ficam localizadas no subdiretório \Team Tools\Performance Tools do diretório de instalação do [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]. Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de Prompt de Comando ou adicioná-lo ao próprio comando. Para obter mais informações, consulte [Especificando o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).  
>   
>  Adicionar dados de interação de camada a uma execução de criação de perfil requer procedimentos específicos com ferramentas de criação de perfil de linha de comando. Consulte [Coletando dados de interação entre camadas](../profiling/adding-tier-interaction-data-from-the-command-line.md).  

 Para coletar dados detalhados de tempo de um componente do .NET Framework usando o método de instrumentação, você usa a ferramenta [VSInstr.exe](../profiling/vsinstr.md) para gerar uma versão instrumentada do componente e a ferramenta [VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) para inicializar variáveis de ambiente de criação de perfil. Em seguida, inicie o criador de perfil.  

 Quando o componente instrumentado é executado, os dados de tempo são automaticamente coletados para um arquivo de dados. Você pode pausar e retomar a coleta de dados durante a sessão de criação de perfil.  

 Para terminar uma sessão de criação de perfil, feche o aplicativo de destino e feche explicitamente o criador de perfil. Na maioria dos casos, recomendamos desmarcar as variáveis de ambiente de criação de perfil no final de uma sessão.  

## <a name="starting-the-profiling-session"></a>Iniciando a sessão de criação de perfil  

#### <a name="to-start-profiling-by-using-the-instrumentation-method"></a>Para iniciar a criação de perfil usando o método de instrumentação  

1. Abra uma janela do Prompt de Comando. Se necessário, adicione o diretório das ferramentas do criador de perfil à variável de ambiente PATH. O caminho não é adicionado na instalação.  

2. Use a ferramenta **VSInstr** para gerar uma versão instrumentada do aplicativo de destino.  

3. Inicialize as variáveis de ambiente de criação de perfil do .NET Framework. Tipo:  

    **VSPerfClrEnv /traceon**  

4. Inicie o criador de perfil. Tipo:  

    **VSPerfCmd /start:trace /output:** `OutputFile` [`Options`]  

   - A opção [/start](../profiling/start.md)**:trace** inicializa o criador de perfil.  

   - A opção [/output](../profiling/output.md)**:**`OutputFile` é necessária com **/start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).  

     É possível usar qualquer uma das opções a seguir com a opção **/start:trace**.  

   |                                 Opção                                  |                                                                                                                                                     Descrição                                                                                                                                                     |
   |-------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | [/user](../profiling/user-vsperfcmd.md) **:**[`Domain`**\\**]`UserName` |                 Especifica o domínio e o nome de usuário da conta que possui o processo analisado. Esta opção será necessária apenas se o processo estiver sendo executado como um usuário diferente do usuário conectado. O proprietário do processo é listado na coluna Nome de Usuário na guia Processos do Gerenciador de Tarefas do Windows.                 |
   |              [/crosssession](../profiling/crosssession.md)              | Habilita a criação de perfil de processos em outras sessões. Esta opção será necessária se o aplicativo ASP.NET estiver em execução em uma sessão diferente. O identificador da sessão é listado na coluna ID da Sessão na guia Processos do Gerenciador de Tarefas do Windows. **/CS** pode ser especificado como uma abreviação de **/crosssession**. |
   |          [/globaloff](../profiling/globalon-and-globaloff.md)           |                                                                                            Inicia o criador de perfil com a coleta de dados em pausa. Use [/globalon](../profiling/globalon-and-globaloff.md) para retomar a criação de perfil.                                                                                            |
   |           [/counter](../profiling/counter.md) **:** `Config`            |                                                                   Coleta informações do contador de desempenho do processador que é especificado em `Config`. As informações do contador são adicionadas aos dados que são coletados em cada evento de criação de perfil.                                                                    |
   |    [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath`     |                                                                                                                      Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil.                                                                                                                      |
   |         [/automark](../profiling/automark.md) **:** `Interval`          |                                                                                    Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms.                                                                                    |
   |       [/events](../profiling/events-vsperfcmd.md) **:** `Config`        |                                                                                      Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Eventos de ETW são coletados em um arquivo separado (.etl).                                                                                       |


5. Inicie o aplicativo de destino na janela do Prompt de Comando.  

## <a name="controlling-data-collection"></a>Controlando coleção de dados  
 Quando o aplicativo de destino estiver em execução, você pode controlar a coleta de dados iniciando e interrompendo a gravação de dados no arquivo de dados do criador de perfil usando as opções do **VSPerfCmd.exe**. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como a inicialização ou o desligamento do aplicativo.  

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados  

-   Os pares de opções a seguir iniciam e interrompem a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.  

    |Opção|Descrição|  
    |------------|-----------------|  
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|  
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pela ID de processo (`PID`).|  
    |[/threadon](../profiling/threadon-and-threadoff.md) **:** `TID` [/threadoff](../profiling/threadon-and-threadoff.md) **:** `TID`|Inicia (**/threadon**) ou interrompe (**/threadoff**) a coleta de dados para o thread especificado pela ID do thread (`TID`).|  

## <a name="ending-the-profiling-session"></a>Encerrando a sessão de criação de perfil  
 Para terminar uma sessão de criação de perfil, feche o aplicativo que está executando o componente instrumentado. Chame a opção **VSPerfCmd** [/shutdown](../profiling/shutdown.md) para desligar o criador de perfil e fechar o arquivo de dados de criação de perfil. O comando **VSPerfClrEnv /off** limpa as variáveis de ambiente da criação de perfil.  

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil  

1.  Feche o aplicativo de destino.  

2.  Desligue o criador de perfil. Tipo:  

     **VSPerfCmd /shutdown**  

3.  (Opcional) desmarcar as variáveis de ambiente de criação de perfil. Tipo:  

     **VSPerfClrEnv /off**  

## <a name="see-also"></a>Consulte também  
 [Criando perfil de aplicativos autônomos](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [Exibições de dados do método de instrumentação](../profiling/instrumentation-method-data-views.md)



