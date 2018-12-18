---
title: Como instrumentar um serviço nativo e coletar dados de tempo detalhados usando a linha de comando do criador de perfil | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: dfe58b39-63f8-4a87-ab3a-2b5b14faa8d0
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- cplusplus
ms.openlocfilehash: dfac7f0ac4e2552974c702a8dd4426bfcdd8dc37
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49870829"
---
# <a name="how-to-instrument-a-native-service-and-collect-detailed-timing-data-by-using-the-profiler-command-line"></a>Como instrumentar um serviço nativo e coletar dados de tempo detalhados usando a linha de comando do criador de perfil
Este artigo descreve como usar as ferramentas da linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para instrumentar um serviço nativo (C/C++) e coletar dados de tempo detalhados.  

> [!NOTE]
>  Você não poderá analisar um serviço com o método de instrumentação se o serviço não puder ser reiniciado após o início do computador, um serviço que inicia somente quando o sistema operacional for iniciado.  
> 
>  As ferramentas de linha de comando das Ferramentas de Criação de Perfil estão localizadas no subdiretório *\Team Tools\Performance Tools* do diretório de instalação do [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)]. Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de prompt de comando ou adicioná-lo ao próprio comando. Para saber mais, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).  

 Para coletar dados de tempo detalhados de um serviço nativo usando o método de instrumentação, use a ferramenta [VSInstr.exe](../profiling/vsinstr.md) para gerar uma versão instrumentada do componente. Em seguida, substitua a versão do serviço não instrumentada pela versão instrumentada, certificando-se de que o serviço esteja configurado para iniciar manualmente. Em seguida, inicie o criador de perfil.  

 Quando o serviço é iniciado, os dados de tempo são automaticamente coletados para um arquivo de dados. Você pode pausar e retomar a coleta de dados durante a sessão de criação de perfil.  

 Para concluir uma sessão de criação de perfil, desligue o serviço e depois desligue explicitamente o criador de perfil.  

## <a name="start-the-application-with-the-profiler"></a>Iniciar o aplicativo com o criador de perfil  

#### <a name="to-start-profiling-a-native-service"></a>Para iniciar a criação de perfil de um serviço nativo  

1. Abra uma janela do prompt de comando.  

2. Use a ferramenta **VSInstr** para gerar uma versão instrumentada do binário.  

3. Substitua o binário original pela versão instrumentada. No Gerenciador de Controle de Serviço Windows, certifique-se de que o Tipo de inicialização do serviço esteja definido como Manual.  

4. Inicie o criador de perfil. Tipo:  

    **VSPerfCmd** [/start](../profiling/start.md) **:trace**  [/output](../profiling/output.md) **:** `OutputFile` [`Options`]  

   - A opção **/start:trace** inicializa o criador de perfil.  

   - A opção **/output:**`OutputFile` é necessária com **/start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.*vsp*).  

     É possível usar qualquer uma das opções a seguir com a opção **/start:trace**.  

   > [!NOTE]
   >  Normalmente, as opções **/user** e **/crosssession** são necessárias para aplicativos ASP.NET.  

   | Opção | Descrição |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:**[`Domain`**\\**]`UserName` | Especifica o domínio e o nome de usuário da conta proprietária do processo de trabalho ASP.NET analisado. Esta opção será necessária se o processo estiver sendo executado como um usuário diferente do usuário conectado. O proprietário do processo é listado na coluna **Nome de Usuário** na guia **Processos** do Gerenciador de Tarefas do Windows. |
   | [/crosssession](../profiling/crosssession.md) | Habilita a criação de perfil de processos em outras sessões de logon. Esta opção será necessária se o aplicativo ASP.NET estiver em execução em uma sessão diferente. A ID da sessão é listada na coluna ID da Sessão na guia Processos do Gerenciador de Tarefas do Windows. **/CS** pode ser especificado como uma abreviação de **/crosssession**. |
   | [/waitstart](../profiling/waitstart.md)[**:**`Interval`] | Especifica o número de segundos para aguardar o criador de perfil inicializar antes de retornar um erro. Se `Interval` não for especificado, o criador de perfil aguardará indefinidamente. Por padrão, **/start** retorna imediatamente. |
   | [/globaloff](../profiling/globalon-and-globaloff.md) | Para iniciar o criador de perfil com a coleta de dados em pausa, adicione a opção **/globaloff** na linha de comando **/start**. Use **/globalon** para retomar a criação de perfil. |
   | [/counter](../profiling/counter.md) **:** `Config` | Coleta informações do contador de desempenho do processador especificado em Config. As informações do contador são adicionadas aos dados coletados em cada evento de criação de perfil. |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil. |
   | [/automark](../profiling/automark.md) **:** `Interval` | Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms. |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Os eventos do ETW são coletados em um arquivo separado (.*etl*). |


5. Inicie o serviço do Gerenciador de Controle de Serviço.  

## <a name="control-data-collection"></a>Controlar a coleta de dados  
 Quando o serviço estiver em execução, você pode usar as opções *VSPerfCmd.exe* para iniciar e parar a gravação de dados no arquivo de dados do criador de perfil. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como a inicialização ou o desligamento do serviço.  

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados  

-   Os pares de opções **VSPerfCmd** a seguir iniciam e interrompem a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.  

    |Opção|Descrição|  
    |------------|-----------------|  
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|  
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pela ID de processo (`PID`).|  
    |[/threadon](../profiling/threadon-and-threadoff.md) **:** `TID` [/threadoff](../profiling/threadon-and-threadoff.md) **:** `TID`|Inicia (**/threadon**) ou interrompe (**/threadoff**) a coleta de dados para o thread especificado pela ID do thread (`TID`).|  

## <a name="end-the-profiling-session"></a>Encerrar a sessão de criação de perfil  
 Para encerrar uma sessão de criação de perfil, interrompa o serviço que está executando o componente instrumentado e, em seguida, chame a opção **VSPerfCmd** [/shutdown](../profiling/shutdown.md) para desligar o criador de perfil e fechar o arquivo de dados de criação de perfil.  

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil  

1.  Interrompa o serviço do Gerenciador de Controle de Serviço.  

2.  Desligue o criador de perfil. Tipo:  

     **VSPerfCmd /shutdown**  

3.  Substitua o módulo instrumentado pelo original. Se necessário, reconfigure o Tipo de inicialização do serviço.  

## <a name="see-also"></a>Consulte também  
 [Serviços de perfil](../profiling/command-line-profiling-of-services.md)   
 [Exibições de dados do método de instrumentação](../profiling/instrumentation-method-data-views.md)