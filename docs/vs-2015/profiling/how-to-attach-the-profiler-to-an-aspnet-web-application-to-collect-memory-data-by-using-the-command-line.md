---
title: Como anexar o Criador de perfil a um aplicativo Web ASP .NET para coletar dados de memória usando a linha de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d608f85a-41ae-4ca7-85e6-b96624dbc83c
caps.latest.revision: 36
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6818c7c23a1ca42fc4537e1024778cd4cab0f177
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51794563"
---
# <a name="how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-memory-data-by-using-the-command-line"></a>Como anexar o criador de perfil a um aplicativo Web ASP.NET para coletar dados de memória usando a linha de comando
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico descreve como usar as Ferramentas de linha de comando das Ferramentas de criação de perfil do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para anexar o criador de perfil a um aplicativo Web [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] e coletar dados sobre o número e o tamanho das alocações de memória do .NET Framework. Também é possível coletar dados sobre o tempo de vida de objetos de memória do .NET Framework.  

> [!NOTE]
>  As ferramentas de linha de comando das Ferramentas de Criação de Perfil ficam localizadas no subdiretório \Team Tools\Performance Tools do diretório de instalação do [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]. Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de Prompt de Comando ou adicioná-lo ao próprio comando. Para obter mais informações, consulte [Especificando o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).  

 Para coletar dados de desempenho de um aplicativo Web [!INCLUDE[vstecasp](../includes/vstecasp-md.md)], você deve usar a ferramenta [VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) para inicializar as variáveis de ambiente apropriadas no computador que hospeda o aplicativo Web [!INCLUDE[vstecasp](../includes/vstecasp-md.md)]. Em seguida, você deve reiniciar o computador para configurar o servidor Web para criação de perfil.  

 Você deverá, então, usar a ferramenta [VSPerfCmd.exe](../profiling/vsperfcmd.md) para anexar o criador de perfil ao processo de trabalho [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] que hospeda seu site da Web. Quando criador de perfil estiver anexado ao aplicativo, você poderá pausar e retomar a coleta de dados.  

 Para concluir uma sessão de criação de perfil, o Criador de perfil não pode mais estar anexado ao aplicativo e o Criador de perfil deve ser desligado explicitamente. Na maioria dos casos, recomendamos desmarcar as variáveis de ambiente de criação de perfil no final de uma sessão.  

## <a name="attaching-the-profiler"></a>Anexando o Criador de perfil  

#### <a name="to-attach-the-profiler-to-an-aspnet-web-application"></a>Para anexar o Criador de perfil a um aplicativo Web ASP .NET  

1. Abra uma janela do Prompt de Comando.  

2. Inicialize as variáveis de ambiente de criação de perfil. Tipo:  

    **VSPerfClrEnv** {**/globalsamplegc** &#124; **/globalsamplegclife**} [**/samplelineoff**]  

   -   As opções **/globalsamplegc** e **/globalsamplegclife** especificam o tipo de dados de memória a serem coletados.  

        Especifique uma e apenas uma das seguintes opções.  

       |Opção|Descrição|  
       |------------|-----------------|  
       |**/globalsamplegc**|Habilita a coleta de dados de alocação de memória.|  
       |**/globalsamplegclife**|Habilita a coleta de dados de alocação de memória e de dados de tempo de vida do objeto.|  

   -   A opção **/samplelineoff** desabilita a atribuição dos dados coletados para linhas específicas do código-fonte. Se essa opção for especificada, os dados serão atribuídos no nível da função.  

3. Reinicie o computador para definir a nova configuração do ambiente.  

4. Abra uma janela do Prompt de Comando. Se necessário, defina a variável do ambiente do criador de perfil.  

5. Inicie o criador de perfil. Tipo:  

    **VSPerfCmd**  [/start](../profiling/start.md) **:sample**  [/output](../profiling/output.md) **:** `OutputFile` [`Options`]  

   - A opção **/start:sample** inicializa o criador de perfil.  

   - A opção **/output:**`OutputFile` é necessária com **/start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).  

     É possível usar qualquer uma das opções a seguir com a opção **/start:sample**.  

   > [!NOTE]
   >  Normalmente, as opções **/user** e **/crosssession** são necessárias para aplicativos ASP.NET.  

   |                                 Opção                                  |                                                                                                                                                        Descrição                                                                                                                                                        |
   |-------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | [/user](../profiling/user-vsperfcmd.md) **:**[`Domain`**\\**]`UserName` |                   Especifica o domínio e o nome de usuário da conta proprietária do processo de trabalho ASP.NET analisado. Esta opção será necessária se o processo estiver sendo executado como um usuário diferente do usuário conectado. O proprietário do processo é listado na coluna Nome de Usuário na guia Processos do Gerenciador de Tarefas do Windows.                    |
   |              [/crosssession](../profiling/crosssession.md)              | Habilita a criação de perfil de processos em outras sessões de logon. Esta opção será necessária se o aplicativo ASP.NET estiver em execução em uma sessão diferente. O identificador da sessão é listado na coluna ID da Sessão na guia Processos do Gerenciador de Tarefas do Windows. **/CS** pode ser especificado como uma abreviação de **/crosssession**. |
   |        [/waitstart](../profiling/waitstart.md) [**:**`Interval`]        |                                                      Especifica o número de segundos para aguardar o criador de perfil inicializar antes de retornar um erro. Se `Interval` não for especificado, o criador de perfil aguardará indefinidamente. Por padrão, **/start** retorna imediatamente.                                                      |
   |    [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath`     |                                                                                                                         Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil.                                                                                                                         |
   |         [/automark](../profiling/automark.md) **:** `Interval`          |                                                                                       Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms.                                                                                       |
   |       [/events](../profiling/events-vsperfcmd.md) **:** `Config`        |                                                                                         Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Eventos de ETW são coletados em um arquivo separado (.etl).                                                                                          |


6. Inicie o aplicativo Web [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] normalmente.  

7. Anexe o criador de perfil ao processo de trabalho [!INCLUDE[vstecasp](../includes/vstecasp-md.md)]. Tipo:  

    **VSPerfCmd**  [/attach](../profiling/attach.md) **:**{`PID`&#124;`ProcName`} [[/targetclr](../profiling/targetclr.md)**:**`Version`]  

   -   A ID do processo `(PID)` especifica a ID ou o nome do processo de trabalho [!INCLUDE[vstecasp](../includes/vstecasp-md.md)]. É possível exibir as IDs de processo de todos os processos em execução no Gerenciador de Tarefas do Windows.  

   -   **/targetclr:** `Version` especifica a versão do CLR (Common Language Runtime) analisada quando mais de uma versão do tempo de execução for carregada em um aplicativo.  

## <a name="controlling-data-collection"></a>Controlando coleção de dados  
 Enquanto o aplicativo estiver em execução, você poderá controlar a coleta de dados iniciando e interrompendo a gravação dos dados no arquivo de dados do criador de perfil usando as opções de **VSPerfCmd.exe**. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como a inicialização ou o desligamento do aplicativo.  

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados  

-   Os pares de opções **VSPerfCmd** a seguir iniciam e interrompem a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.  

    |Opção|Descrição|  
    |------------|-----------------|  
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|  
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pelo `PID`.|  
    |**/attach:**{`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[**:**{`PID`&#124;:`ProcName`}]|**/attach** começa a coletar dados para o processo especificado pela ID de processo ou pelo nome de processo. **/detach** interrompe a coleta de dados para o processo especificado ou para todos os processos se nenhum processo específico for especificado.|  

## <a name="ending-the-profiling-session"></a>Encerrando a sessão de criação de perfil  
 Para terminar uma sessão de criação de perfil, o criador de perfil deve ser desanexado do aplicativo Web. É possível interromper a coleta de dados de um aplicativo analisado com o método de amostragem reiniciando o processo de trabalho [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ou invocando a opção **VSPerfCmd /detach**. Chame então a opção **VSPerfCmd** [/shutdown](../profiling/shutdown.md) para desligar o criador de perfil e fechar o arquivo de dados de criação de perfil. O comando **VSPerfClrEnv /globaloff** limpa as variáveis de ambiente de criação de perfil, mas a configuração do sistema não é redefinida até que o computador seja reiniciado.  

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil  

1. Realize uma das etapas a seguir para desanexar o criador de perfil do aplicativo de destino:  

   - Digite **VSPerfCmd** [/detach](../profiling/detach.md)  

      -ou-  

   - Feche o processo de trabalho [!INCLUDE[vstecasp](../includes/vstecasp-md.md)]. Tipo:  

     **IISReset /stop**  

2. Desligue o criador de perfil. Tipo:  

    **VSPerfCmd /shutdown**  

3. (Opcional) desmarcar as variáveis de ambiente de criação de perfil. Tipo:  

    **VSPerfCmd /globaloff**  

4. Reinicie o computador. Se necessário, reinicie o ISS (Serviços de Informações da Internet). Tipo:  

    **IISReset /start**  

## <a name="see-also"></a>Consulte também  
 [Criando perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [Exibições de dados da memória do .NET](../profiling/dotnet-memory-data-views.md)



