---
title: Como anexar o Criador de perfil a um serviço .NET para coletar dados de memória usando a linha de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: aeac39af-ad99-479f-aa36-4104356ca512
caps.latest.revision: 33
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 93809264569065d1b13fd08b89f91a9335576413
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51763691"
---
# <a name="how-to-attach-the-profiler-to-a-net-service-to-collect-memory-data-by-using-the-command-line"></a>Como anexar o criador de perfil a um serviço do .NET para coletar dados de memória usando a linha de comando
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico descreve como usar as Ferramentas de linha de comando das Ferramentas de criação de perfil do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para anexar o criador de perfil a um serviço [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] e coletar dados da memória. É possível coletar dados sobre o número e tamanho das alocações de memória, bem como sobre o tempo de vida de objetos de memória.  

> [!NOTE]
>  Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos da Windows Store também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).  

> [!NOTE]
>  As ferramentas de linha de comando das Ferramentas de Criação de Perfil ficam localizadas no subdiretório \Team Tools\Performance Tools do diretório de instalação do [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]. Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de prompt de comando ou adicioná-lo ao próprio comando. Para obter mais informações, consulte [Especificando o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).  

 Para coletar dados de memória de um serviço [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)], você deve usar a ferramenta [VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) para inicializar as variáveis de ambiente apropriadas no computador que hospeda o serviço. O computador deve ser reiniciado para configurá-lo para a criação de perfil.  

 Você usar a ferramenta [VSPerfCmd](../profiling/vsperfcmd.md) para anexar o criador de perfil ao processo do serviço. Enquanto o criador de perfil estiver anexado ao serviço, você pode pausar e retomar a coleta de dados.  

 Para concluir uma sessão de criador de perfil, o criador de perfil deve ser desanexado do serviço e desligado explicitamente. Na maioria dos casos, recomendamos desmarcar as variáveis de ambiente de criação de perfil no final de uma sessão.  

## <a name="attaching-the-profiler"></a>Anexando o Criador de perfil  

#### <a name="to-attach-the-profiler-to-a-net-framework-service"></a>Para anexar o Criador de perfil a um serviço do .NET Framework  

1. Se necessário, instale o serviço.  

2. Abra uma janela do prompt de comando.  

3. Inicialize as variáveis de ambiente de criação de perfil. Tipo:  

    **VSPerfClrEnv** {**/globalsamplegc /globalsamplegclife**}[**/samplelineoff**]  

   - As opções **/globalsamplegclife** e **/globalsamplegclife** especificam o tipo de dados de memória a serem coletados. Especifique uma e apenas uma das seguintes opções.  

     **/globalsamplegc**  
     Habilita a coleta de dados de alocação de memória.  

     **/globalsamplegclife**  
     Habilita a coleta de dados de alocação de memória e de dados de tempo de vida do objeto.  

   - A opção **/samplelineoff** desabilita a coleta de dados do número de linha do código-fonte.  

4. Reinicie o computador para definir a nova configuração do ambiente.  

5. Se necessário, inicie o serviço.  

6. Abra uma janela do prompt de comando. Se necessário, adicione o caminho do criador de perfil à variável de ambiente PATH.  

7. Inicie o criador de perfil. Tipo:  

    **VSPerfCmd**  [/start](../profiling/start.md) **:sample**  [/output](../profiling/output.md) **:** `OutputFile` [`Options`]  

   - A opção **/start:sample** inicializa o criador de perfil.  

   - A opção **/output:**`OutputFile` é necessária com **/start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).  

     É possível usar uma ou várias opções a seguir com a opção **/start:sample**.  

   > [!NOTE]
   >  Normalmente, as opções **/user** e **/crosssession** são necessárias para serviços.  

   |                                 Opção                                  |                                                                                                                                                   Descrição                                                                                                                                                    |
   |-------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | [/user](../profiling/user-vsperfcmd.md) **:**[`Domain`**\\**]`UserName` |                      Especifica o domínio e o nome de usuário da conta que possui o processo. Esta opção será necessária se o processo estiver sendo executado como um usuário diferente do usuário conectado. O proprietário do processo é listado na coluna Nome de Usuário na guia Processos do Gerenciador de Tarefas do Windows.                       |
   |              [/crosssession](../profiling/crosssession.md)              | Habilita a criação de perfil de processos em outras sessões de logon. Esta opção será necessária se o aplicativo ASP.NET estiver em execução em uma sessão diferente. A ID da sessão é listada na coluna ID da Sessão na guia Processos do Gerenciador de Tarefas do Windows. **/CS** pode ser especificado como uma abreviação de **/crosssession**. |
   | [/user](../profiling/user-vsperfcmd.md) **:**[`Domain`**\\**]`UserName` |                                                    Especifica o domínio e o nome de usuário opcionais da conta de logon na qual o serviço é executado. A conta de logon é listada na coluna Fazer logon como do serviço no Gerenciador de Controle de Serviço Windows.                                                     |
   |          [/crosssession&#124;cs](../profiling/crosssession.md)          |                                                                                                                             Habilita a criação de perfil de processos em outras sessões de logon.                                                                                                                              |
   |    [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath`     |                                                                                                                    Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil.                                                                                                                     |
   |         [/automark](../profiling/automark.md) **:** `Interval`          |                                                                                  Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms.                                                                                   |
   |       [/events](../profiling/events-vsperfcmd.md) **:** `Config`        |                                                                                     Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Eventos de ETW são coletados em um arquivo separado (.etl).                                                                                     |


8. Anexe o criador de perfil ao serviço. Tipo:  

    **VSPerfCmd**  [/attach](../profiling/attach.md) **:**{`PID`&#124;`ProcName`} [[/targetclr](../profiling/targetclr.md)**:**`Version`]  

   -   Especifica a ID ou o nome do processo do serviço. É possível exibir as IDs de processo e nomes de todos os processos em execução no Gerenciador de Tarefas do Windows.  

   -   **targetclr:** `Version` especifica a versão do CLR (Common Language Runtime) cujo perfil deverá ser criado quando mais de uma versão do tempo de execução for carregada em um aplicativo. Opcional.  

## <a name="controlling-data-collection"></a>Controlando coleção de dados  
 Enquanto o serviço estiver em execução, você pode usar as opções **VSPerfCmd.exe** para interromper e iniciar a gravação de dados no arquivo de dados do criador de perfil. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como a inicialização ou o desligamento do aplicativo.  

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados  

-   Os pares de opções **VSPerfCmd** a seguir iniciam e interrompem a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.  

    |Opção|Descrição|  
    |------------|-----------------|  
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|  
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pela ID de processo (`PID`).|  
    |**/attach:**{`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[:{`PID`&#124;`ProcName`}]|**/attach** começa a coletar dados para o processo especificado pela ID de processo ou pelo nome de processo. **/detach** interrompe a coleta de dados para o processo especificado ou para todos os processos se nenhum processo específico for definido.|  

## <a name="ending-the-profiling-session"></a>Encerrando a sessão de criação de perfil  
 Para encerrar uma sessão de criação de perfil, o criador de perfil não pode estar coletando dados. É possível interromper a coleta de dados de um aplicativo analisado com o método de amostragem interrompendo o serviço ou chamando a opção **VSPerfCmd /detach**. Em seguida, chame a opção **VSPerfCmd** [/shutdown](../profiling/shutdown.md) para desativar o criador de perfil e fechar o arquivo de dados de criação de perfil. O comando **VSPerfClrEnv /globaloff** limpa as variáveis de ambiente de criação de perfil, mas a configuração do sistema não é redefinida até que o computador seja reiniciado.  

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil  

1.  Siga um destes procedimentos para desanexar o criador de perfil do aplicativo de destino:  

    -   Pare o serviço.  

         -ou-  

    -   Digite **VSPerfCmd /detach**  

2.  Desligue o criador de perfil. Tipo:  

     **VSPerfCmd /shutdown**  

3.  (Opcional) desmarcar as variáveis de ambiente de criação de perfil. Tipo:  

     **VSPerfClrEnv /globaloff**  

4.  Reinicie o computador.  

## <a name="see-also"></a>Consulte também  
 [Serviços de Criação de Perfil](../profiling/command-line-profiling-of-services.md)   
 [Exibições de dados da memória do .NET](../profiling/dotnet-memory-data-views.md)



