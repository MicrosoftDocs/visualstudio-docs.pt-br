---
title: Como iniciar um aplicativo do .NET Framework autônomo com o criador de perfil para coletar dados de memória usando a linha de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3bc53041-91b7-4ad0-8413-f8bf2c4b3f5e
caps.latest.revision: 33
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 207fc9a02be3557341bfad95d6fd32943557478a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51757436"
---
# <a name="how-to-launch-a-stand-alone-net-framework-application-with-the-profiler-to-collect-memory-data-by-using-the-command-line"></a>Como iniciar um aplicativo do .NET Framework autônomo com o criador de perfil para coletar dados de memória usando a linha de comando
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico descreve como usar as ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para iniciar um aplicativo autônomo (cliente) do .NET Framework e coletar dados de memória.  

 Uma sessão de criação de perfil tem três partes:  

-   Iniciar o aplicativo usando o criador de perfil.  

-   Coletar dados de criação de perfil.  

-   Encerrar a sessão de criação de perfil.  

> [!NOTE]
>  As ferramentas de linha de comando das Ferramentas de Criação de Perfil ficam localizadas no subdiretório \Team Tools\Performance Tools do diretório de instalação do [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]. Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de Prompt de Comando ou adicioná-lo ao próprio comando. Para obter mais informações, consulte [Especificando o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).  

## <a name="starting-the-application-with-the-profiler"></a>Iniciar o Aplicativo com o Criador de Perfil  
 Para iniciar um aplicativo de destino usando o criador de perfil, use as opções **VSPerfCmd.exe/start** e **/launch** para inicializar o criador de perfil e iniciar o aplicativo. Você pode especificar **/start** e **/launch** e suas opções respectivas em uma linha de comando.  

 Você também pode adicionar a opções de **/globaloff** para pausar a coleta de dados no início do aplicativo de destino. Depois, você usa **/globalon** para começar a coletar dados.  

#### <a name="to-start-an-application-by-using-the-profiler"></a>Para iniciar um aplicativo usando o Criador de Perfil  

1. Abra uma janela do Prompt de Comando.  

2. Inicie o criador de perfil. Tipo:  

    **VSPerfCmd /start:sample /output:** `OutputFile` [`Options`]  

   - A opção [/start](../profiling/start.md)**:sample** inicializa o criador de perfil.  

   - A opção [/output](../profiling/output.md)**:**`OutputFile` é necessária com **/start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).  

     É possível usar qualquer uma das opções a seguir com a opção **/start:sample**.  

   |                              Opção                              |                                                                  Descrição                                                                  |
   |------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` |                                   Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil.                                   |
   |      [/automark](../profiling/automark.md) **:** `Interval`      | Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms. |


3. Inicie o aplicativo de destino. Tipo:  

    **VSPerfCmd**  [/launch](../profiling/launch.md) **:** `appName` **/gc:**{**allocation**&#124;**lifetime**}[`Options`]  

   - A opção [/gc](../profiling/gc-vsperfcmd.md)**:**`Keyword` é necessária para coletar dados de memória do .NET Framework. O parâmetro de palavra-chave especifica se serão coletados dados de alocação de memória ou se serão coletados dados de alocação de memória e dados de tempo de vida do objeto.  

     |Palavra-chave|Descrição|  
     |-------------|-----------------|  
     |**alocação**|Coleta somente dados de alocação de memória.|  
     |**lifetime**|Coleta de dados de alocação de memória e de tempo de vida do objeto.|  

     É possível usar qualquer uma das opções a seguir com a opção **/launch**.  

   |Opção|Descrição|  
   |------------|-----------------|  
   |[/args](../profiling/args.md) **:** `Arguments`|Especifica uma cadeia de caracteres que contém os argumentos de linha de comando a serem passados para o aplicativo de destino.|  
   |[/console](../profiling/console.md)|Inicia o aplicativo de destino de linha de comando em uma janela separada.|  
   |[/events](../profiling/events-vsperfcmd.md) **:** `Config`|Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Eventos de ETW são coletados em um arquivo separado (.etl).|  
   |[/targetclr](../profiling/targetclr.md) **:** `Version`|Especifica a versão do CLR (Common Language Runtime) a ser analisada quando mais de uma versão de tempo de execução for carregada em um aplicativo.|  

## <a name="controlling-data-collection"></a>Controlando coleção de dados  
 Quando o aplicativo de destino estiver em execução, você pode controlar a coleta de dados iniciando e interrompendo a gravação de dados no arquivo usando as opções de **VSPerfCmd.exe**. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como a inicialização ou o desligamento do aplicativo.  

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados  

-   Os pares de opções a seguir iniciam e interrompem a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.  

    |Opção|Descrição|  
    |------------|-----------------|  
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|  
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [processoff](../profiling/processon-and-processoff.md) **:** `PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pela ID de processo (`PID`).|  
    |[/attach](../profiling/attach.md) **:** `PID` [/detach](../profiling/detach.md)|**/attach** começa a coletar dados para o processo que é especificado pela `PID` (a ID do processo). **/detach** interrompe a coleta de dados para todos os processos.|  

-   Também é possível usar a opção **VSPerfCmd.exe**[/mark](../profiling/mark.md) para inserir uma marca de criação de perfil no arquivo de dados. O comando **/mark** adiciona um identificador, um carimbo de data/hora e uma cadeia de caracteres de texto opcional definida pelo usuário. As marcas podem ser usadas para filtrar os dados.  

## <a name="ending-the-profiling-session"></a>Encerrando a sessão de criação de perfil  
 Para concluir uma sessão de criação de perfil, o criador de perfil deve ser desanexado de todos os processos analisados e o criador de perfil deve ser desligado explicitamente. É possível desanexar o criador de perfil de um aplicativo que foi analisado usando o método de amostragem ao fechar o aplicativo ou chamar a opção **VSPerfCmd /detach**. Depois, você chama a opção **VSPerfCmd /shutdown** para desligar o criador de perfil e fechar o arquivo de dados de criação de perfil. O comando **VSPerfClrEnv /off** limpa as variáveis de ambiente da criação de perfil.  

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil  

1.  Realize uma das etapas a seguir para desanexar o criador de perfil do aplicativo de destino:  

    -   Feche o aplicativo de destino.  

         -ou-  

    -   Digite **VSPerfCmd /detach**  

2.  Desligue o criador de perfil. Tipo:  

     **VSPerfCmd**  [/shutdown](../profiling/shutdown.md)  

## <a name="see-also"></a>Consulte também  
 [Criando perfil de aplicativos autônomos](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [Exibições de dados da memória do .NET](../profiling/dotnet-memory-data-views.md)



