---
title: Como anexar o criador de perfil a um serviço do .NET para coletar dados de simultaneidade usando a linha de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ffbdfe37-8325-44be-bd36-2c8aab2dec7b
caps.latest.revision: 29
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b4f4d940f2bb65fe27c826e4ce06d1ead6626d37
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51756423"
---
# <a name="how-to-attach-the-profiler-to-a-net-service-to-collect-concurrency-data-by-using-the-command-line"></a>Como anexar o criador de perfil a um serviço do .NET para coletar dados de simultaneidade usando a linha de comando
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico descreve como usar as ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para anexar o criador de perfil a um serviço [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] e coletar dados de simultaneidade de thread e processo usando o método de amostragem.  
  
> [!NOTE]
>  Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos da Windows Store também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).  
  
> [!NOTE]
>  As ferramentas de linha de comando das Ferramentas de Criação de Perfil ficam localizadas no subdiretório \Team Tools\Performance Tools do diretório de instalação do Visual Studio. Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de prompt de comando ou adicioná-lo ao próprio comando. Para obter mais informações, consulte [Especificando o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).  
  
 Para coletar dados de simultaneidade, anexe o criador de perfil ao processo do serviço. Enquanto o criador de perfil estiver anexado ao serviço, você pode pausar e retomar a coleta de dados. Para concluir uma sessão de criação de perfil, o Criador de perfil não pode mais estar anexado ao serviço e o Criador de perfil deve ser desligado explicitamente. Na maioria dos casos, recomendamos desmarcar as variáveis de ambiente de criação de perfil no final de uma sessão.  
  
## <a name="attaching-the-profiler"></a>Anexando o Criador de perfil  
  
#### <a name="to-attach-the-profiler-to-a-net-framework-service"></a>Para anexar o Criador de perfil a um serviço do .NET Framework  
  
1.  Instale o serviço.  
  
2.  Abra uma janela de comando.  
  
3.  Inicialize as variáveis de ambiente de criação de perfil. Tipo:  
  
     [VSPerfClrEnv](../profiling/vsperfclrenv.md) **/globalsampleon** [**/samplelineoff**]  
  
    -   **/globalsampleon** habilita a amostragem.  
  
    -   **/samplelineoff** desabilita a atribuição de dados coletados a linhas específicas do código-fonte. Quando essa opção for especificada, os dados serão atribuídos somente a funções.  
  
4.  Reinicie o computador.  
  
5.  Inicie o criador de perfil. Tipo:  
  
     [VSPerfCmd](../profiling/vsperfcmd.md) **/start:concurrency  /output:** `OutputFile` [`Options`]  
  
     A opção [/output](../profiling/output.md)**:**`OutputFile` é necessária com **/start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).  
  
     É possível usar qualquer uma das opções a seguir com a opção **/start**.  
  
    > [!NOTE]
    >  Normalmente, as opções **/user** e **/crosssession** são necessárias para serviços.  
  
    |Opção|Descrição|  
    |------------|-----------------|  
    |[/user](../profiling/user-vsperfcmd.md) **:**[`Domain`**\\**]`UserName`|Especifica o domínio e o nome de usuário da conta que possui o processo analisado. Esta opção é necessária apenas se o processo estiver sendo executado como um usuário diferente do usuário conectado. O proprietário do processo é listado na coluna Nome de Usuário na guia Processos do Gerenciador de Tarefas do Windows.|  
    |[/crosssession](../profiling/crosssession.md)|Habilita a criação de perfil de processos em outras sessões. Esta opção é necessária se o serviço estiver em execução em uma sessão diferente. A ID da sessão é listada na coluna ID da Sessão na guia Processos do Gerenciador de Tarefas do Windows. **/CS** pode ser especificado como uma abreviação de **/crosssession**.|  
    |[/wincounter](../profiling/wincounter.md) **:** `WinCounterPath`|Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil.|  
    |[/automark](../profiling/automark.md) **:** `Interval`|Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms.|  
    |[/events](../profiling/events-vsperfcmd.md) **:** `Config`|Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Eventos de ETW são coletados em um arquivo separado (.etl).|  
  
6.  Se necessário, inicie o serviço.  
  
7.  Anexe o criador de perfil ao serviço. Tipo:  
  
     **VSPerfCmd /attach:** `PID` [[/targetclr](../profiling/targetclr.md)**:**`Version`]  
  
    -   `PID` especifica a ID do processo ou o nome do processo do serviço. É possível exibir as IDs de processo de todos os processos em execução no Gerenciador de Tarefas do Windows.  
  
    -   **targetclr:** `Version` especifica a versão do CLR (Common Language Runtime) cujo perfil deverá ser criado quando mais de uma versão do tempo de execução for carregada em um aplicativo. Opcional.  
  
## <a name="controlling-data-collection"></a>Controlando coleção de dados  
 Enquanto o serviço estiver em execução, você pode controlar a coleta de dados iniciando e parando a gravação de dados no arquivo usando as opções de VSPerfCmd.exe. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como o início ou o desligamento do aplicativo.  
  
#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados  
  
-   Os pares de opções **VSPerfCmd** a seguir iniciam e interrompem a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.  
  
    |Opção|Descrição|  
    |------------|-----------------|  
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|  
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pela ID de processo (`PID`).|  
    |**/attach:**{`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[:{`PID`&#124;`ProcName`}]|**/attach** começa a coletar dados para o processo especificado pela ID de processo ou pelo nome de processo. **/detach** interrompe a coleta de dados para o processo especificado ou para todos os processos se nenhum processo específico for especificado.|  
  
-   Também é possível usar a opção **VSPerfCmd.exe**[/mark](../profiling/mark.md) para inserir uma marca de criação de perfil no arquivo de dados. O comando **/mark** adiciona um identificador, um carimbo de data/hora e uma cadeia de caracteres de texto opcional definida pelo usuário. As marcas podem ser usadas para filtrar dados em exibições de dados e relatórios do criador de perfil. Os pares de opções VSPerfCmd a seguir iniciam e interrompem a coleta de dados. Especifica cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.  
  
## <a name="ending-the-profiling-session"></a>Encerrando a sessão de criação de perfil  
 Para encerrar uma sessão de criação de perfil, o criador de perfil não pode estar coletando dados. É possível interromper a coleta de dados de um aplicativo cujo perfil foi criado com o método de simultaneidade interrompendo o serviço ou invocando a opção **VSPerfCmd /detach**. Depois, invoque a opção **VSPerfCmd /shutdown** para desativar o criador de perfil e fechar o arquivo de dados de criação de perfil. O comando **VSPerfClrEnv /globaloff** limpa as variáveis de ambiente de criação de perfil, mas a configuração do sistema não é redefinida até que o computador seja reiniciado.  
  
#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil  
  
1.  Siga um destes procedimentos para desanexar o criador de perfil do aplicativo de destino.  
  
    -   Pare o serviço.  
  
         -ou-  
  
    -   Digite **VSPerfCmd /detach.**  
  
2.  Desligue o criador de perfil. Tipo:  
  
     **VSPerfCmd**  [Shutdown](../profiling/shutdown.md)



