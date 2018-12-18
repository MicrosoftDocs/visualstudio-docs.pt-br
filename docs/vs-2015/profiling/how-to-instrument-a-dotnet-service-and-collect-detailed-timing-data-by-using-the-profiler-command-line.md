---
title: Como instrumentar um serviço do .NET e coletar dados de tempo detalhados usando a linha de comando do criador de perfil | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9f73593a-69a7-41b7-a21c-81d3ab0eb8fe
caps.latest.revision: 32
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: dc95a776713876f559bf3d72b50dc6f24e055dc8
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51737651"
---
# <a name="how-to-instrument-a-net-service-and-collect-detailed-timing-data-by-using-the-profiler-command-line"></a>Como instrumentar um serviço do .NET e coletar dados de tempo detalhados usando a linha de comando do criador de perfil
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico descreve como usar as ferramentas da linha de comando das Ferramentas de criação de perfil do [!INCLUDE[vsPreShort](../includes/vspreshort-md.md)] para instrumentar um serviço do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] e coletar dados detalhados de tempo.  

> [!NOTE]
>  Você não pode analisar um serviço com o método de instrumentação se o serviço não puder ser reiniciado após o início do computador, um serviço que inicia somente quando o sistema operacional for iniciado.  
>   
>  As ferramentas de linha de comando das Ferramentas de Criação de Perfil ficam localizadas no subdiretório \Team Tools\Performance Tools do diretório de instalação do [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]. Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de prompt de comando ou adicioná-lo ao próprio comando. Para obter mais informações, consulte [Especificando o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).  
>   
>  Adicionar dados de interação de camada a uma execução de criação de perfil requer procedimentos específicos com ferramentas de criação de perfil de linha de comando. Consulte [Coletando dados de interação entre camadas](../profiling/adding-tier-interaction-data-from-the-command-line.md).  

 Para coletar dados de tempo detalhados de um serviço de [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] usando o método de instrumentação, use a ferramenta [VSInstr.exe](../profiling/vsinstr.md) para gerar uma versão instrumentada do componente. Em seguida, substitua a versão do serviço não instrumentada pela versão instrumentada, certificando-se de que o serviço esteja configurado para iniciar manualmente. Depois, use a ferramenta [VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) para inicializar as variáveis de ambiente de criação de perfil global e reinicie o computador host. Em seguida, inicie o criador de perfil.  

 Quando o serviço é iniciado, os dados de tempo são automaticamente coletados para um arquivo de dados. Você pode pausar e retomar a coleta de dados durante a sessão de criação de perfil.  

 Para concluir uma sessão de criação de perfil, desligue o serviço e depois desligue explicitamente o criador de perfil. Na maioria dos casos, recomendamos desmarcar as variáveis de ambiente de criação de perfil no final de uma sessão.  

## <a name="starting-the-application-with-the-profiler"></a>Iniciar o Aplicativo com o Criador de Perfil  

#### <a name="to-start-profiling-a-net-framework-service"></a>Para iniciar a criação de perfil de um serviço do .NET Framework  

1. Abra uma janela do prompt de comando.  

2. Use a ferramenta **VSInstr** para gerar uma versão instrumentada do binário.  

3. Substitua o binário original pela versão instrumentada. No Gerenciador de Controle de Serviço Windows, certifique-se de que o Tipo de inicialização do serviço esteja definido como Manual.  

4. Inicialize as variáveis de ambiente de criação de perfil de [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]. Tipo:  

    **VSPerfClrEnv /globaltraceon**  

5. Reinicie o computador.  

6. Abra uma janela do prompt de comando.  

7. Inicie o criador de perfil. Tipo:  

    **VSPerfCmd /start:trace /output:** `OutputFile` [`Options`]  

   - A opção [/start](../profiling/start.md)**:trace** inicializa o criador de perfil.  

   - A opção [/output](../profiling/output.md)**:**`OutputFile` é necessária com **/start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).  

     É possível usar qualquer uma das opções a seguir com a opção **/start:trace**.  

   > [!NOTE]
   >  Normalmente, as opções **/user** e **/crosssession** são necessárias para serviços de criação de perfil.  

   |                                 Opção                                  |                                                                                                                                            Descrição                                                                                                                                             |
   |-------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | [/user](../profiling/user-vsperfcmd.md) **:**[`Domain`**\\**]`UserName` |        Especifica o domínio e o nome de usuário da conta que possui o processo analisado. Esta opção é necessária apenas se o processo estiver sendo executado como um usuário diferente do usuário conectado. O proprietário do processo é listado na coluna Nome de Usuário na guia Processos do Gerenciador de Tarefas do Windows.         |
   |              [/crosssession](../profiling/crosssession.md)              | Habilita a criação de perfil de processos em outras sessões. Esta opção será necessária se o aplicativo estiver em execução em uma sessão diferente. A ID da sessão é listada na coluna ID da Sessão na guia Processos do Gerenciador de Tarefas do Windows. **/CS** pode ser especificado como uma abreviação de **/crosssession**. |
   |        [/waitstart](../profiling/waitstart.md)[**:**`Interval`]         |                                          Especifica o número de segundos para aguardar o criador de perfil inicializar antes de retornar um erro. Se `Interval` não for especificado, o criador de perfil aguardará indefinidamente. Por padrão, **/start** retorna imediatamente.                                           |
   |          [/globaloff](../profiling/globalon-and-globaloff.md)           |                                                                      Para iniciar o criador de perfil com a coleta de dados em pausa, adicione a opção **/globaloff** na linha de comando **/start**. Use **/globalon** para retomar a criação de perfil.                                                                       |
   |           [/counter](../profiling/counter.md) **:** `Config`            |                                                                    Coleta informações do contador de desempenho do processador especificado em Config. As informações do contador são adicionadas aos dados coletados em cada evento de criação de perfil.                                                                    |
   |    [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath`     |                                                                                                             Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil.                                                                                                              |
   |         [/automark](../profiling/automark.md) **:** `Interval`          |                                                                           Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms.                                                                            |
   |       [/events](../profiling/events-vsperfcmd.md) **:** `Config`        |                                                                              Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Eventos de ETW são coletados em um arquivo separado (.etl).                                                                              |


8. Inicie o serviço do Gerenciador de Controle de Serviço Windows.  

## <a name="controlling-data-collection"></a>Controlando coleção de dados  
 Quando o serviço estiver em execução, você pode usar as opções **VSPerfCmd.exe** para iniciar e parar a gravação de dados no arquivo de dados do criador de perfil. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como a inicialização ou o desligamento do serviço.  

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados  

-   Os pares de opções **VSPerfCmd** a seguir iniciam e interrompem a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.  

    |Opção|Descrição|  
    |------------|-----------------|  
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|  
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pela ID de processo (`PID`).|  
    |[/threadon](../profiling/threadon-and-threadoff.md) **:** `TID` [/threadoff](../profiling/threadon-and-threadoff.md) **:** `TID`|Inicia (**/threadon**) ou interrompe (**/threadoff**) a coleta de dados para o thread especificado pela ID do thread (`TID`).|  

## <a name="ending-the-profiling-session"></a>Encerrando a sessão de criação de perfil  
 Para encerrar uma sessão de criação de perfil, pare o serviço que está executando o componente instrumentado e, em seguida, chame a opção **VSPerfCmd** [/shutdown](../profiling/shutdown.md) para desligar o criador de perfil e fechar o arquivo de dados de criação de perfil. O comando **VSPerfClrEnv /globaloff** limpa as variáveis de ambiente da criação de perfil.  

 Você deve reiniciar o computador para que as novas configurações de ambiente sejam aplicadas.  

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil  

1.  Interrompa o serviço do Gerenciador de Controle de Serviço.  

2.  Desligue o criador de perfil. Tipo:  

     **VSPerfCmd /shutdown**  

3.  Quando você tiver concluído a criação de todos os perfis, desmarque as variáveis de ambiente de criação de perfil. Tipo:  

     **VSPerfClrEnv /globaloff**  

4.  Substitua o módulo instrumentado pelo original. Se necessário, reconfigure o Tipo de inicialização do serviço.  

5.  Reinicie o computador.  

## <a name="see-also"></a>Consulte também  
 [Serviços de Criação de Perfil](../profiling/command-line-profiling-of-services.md)   
 [Exibições de dados do método de instrumentação](../profiling/instrumentation-method-data-views.md)



