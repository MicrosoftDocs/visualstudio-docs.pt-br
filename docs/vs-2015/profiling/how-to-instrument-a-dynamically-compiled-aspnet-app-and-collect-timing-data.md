---
title: Como instrumentar um aplicativo Web ASP .NET compilado dinamicamente e coletar dados de tempo detalhados com o criador de perfil usando a linha de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6c140ae2-ecdd-48c7-bd89-3dc1b88e19b0
caps.latest.revision: 24
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 041385fcda5aa587647752c3e32f933a5674b8aa
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51757111"
---
# <a name="how-to-instrument-a-dynamically-compiled-aspnet-web-application-and-collect-detailed-timing-data-with-the-profiler-by-using-the-command-line"></a>Como instrumentar um aplicativo Web do ASP.NET compilado dinamicamente e coletar dados de tempo detalhados com o criador de perfil usando a linha de comando
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico descreve como usar as ferramentas de linha de comando de Ferramentas de Criação de Perfil de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para coletar dados de tempo detalhados para um aplicativo [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] compilado dinamicamente usando o método de criação de perfil por instrumentação.  

> [!NOTE]
>  As ferramentas de linha de comando das Ferramentas de Criação de Perfil ficam localizadas no subdiretório \Team Tools\Performance Tools do diretório de instalação do [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]. Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de Prompt de Comando ou adicioná-lo ao próprio comando. Para obter mais informações, consulte [Especificando o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).  

 Para coletar dados de desempenho de um aplicativo Web [!INCLUDE[vstecasp](../includes/vstecasp-md.md)], modifique o arquivo web.config do aplicativo de destino para habilitar a ferramenta [VSInstr.exe](../profiling/vsinstr.md) para instrumentar os arquivos do aplicativo compilado dinamicamente. Em seguida, você usa a ferramenta [VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) para definir as variáveis de ambiente adequadas no servidor Web para habilitar a criação de perfil e então reinicia o computador.  

 Inicie o criador de perfil e, em seguida, execute o aplicativo de destino. Enquanto o criador de perfil estiver anexado ao aplicativo, você pode pausar e retomar a coleta de dados. Quando você terminar a criação de perfil, feche o aplicativo, feche o processo de trabalho dos IIS (Serviços de Informações da Internet) e, em seguida, desligue o criador de perfil. Quando você tiver concluído o trabalho de criação de perfil, restaure o arquivo web.config e o servidor Web para seus respectivos estados originais.  

## <a name="configuring-the-aspnet-web-application-and-the-web-server"></a>Configurando o Aplicativo Web ASP .NET e o servidor Web  

#### <a name="to-configure-the-aspnet-web-application-and-the-web-server"></a>Para configurar o aplicativo Web ASP .NET e o servidor Web  

1.  Modifique o arquivo web.config do aplicativo de destino. Consulte [Como Modificar Arquivos Web.Config para Instrumentar e Criar Perfil de Aplicativos Web ASP.NET Compilados Dinamicamente](../profiling/how-to-modify-web-config-files-to-instrument-and-profile-dynamically-compiled-aspnet-web-applications.md).  

2.  Abra uma janela do Prompt de Comando.  

3.  Inicialize as variáveis de ambiente de criação de perfil. Tipo:  

     **VSPerfClrEnv /globaltraceon**  

    -   **/globaltraceon** habilita a criação de perfil usando o método de instrumentação.  

4.  Reinicie o computador.  

## <a name="running-the-profiling-session"></a>Executando a sessão de criação de perfil  

#### <a name="to-profile-the-web-application"></a>Para criar o perfil do aplicativo Web  

1. Abra uma janela do Prompt de Comando.  

2. Inicie o criador de perfil. Tipo:  

    **VSPerfCmd**  [/start](../profiling/start.md) **:trace**  [/output](../profiling/output.md) **:** `OutputFile` [`Options`]  

   - A opção **/start:trace** inicializa o criador de perfil.  

   - A opção **/output:**`OutputFile` é necessária com **/start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).  

     É possível usar qualquer uma das opções a seguir com a opção **/start:trace**.  

   > [!NOTE]
   >  Normalmente, as opções **/user** e **/crosssession** são necessárias para aplicativos ASP.NET.  

   |                                 Opção                                  |                                                                                                                                                       Descrição                                                                                                                                                        |
   |-------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | [/user](../profiling/user-vsperfcmd.md) **:**[`Domain`**\\**]`UserName` |                   Especifica o domínio e o nome de usuário da conta proprietária do processo de trabalho ASP.NET analisado. Esta opção será necessária se o processo estiver sendo executado como um usuário diferente do usuário conectado. O proprietário do processo é listado na coluna Nome de Usuário na guia Processos do Gerenciador de Tarefas do Windows.                   |
   |              [/crosssession](../profiling/crosssession.md)              | Habilita a criação de perfil de processos em outras sessões de logon. Esta opção será necessária se o aplicativo ASP.NET estiver em execução em uma sessão diferente. O identificador da sessão é listado na coluna ID da Sessão na guia Processos do Gerenciador de Tarefas do Windows. **/CS** pode ser especificado como uma abreviação de **/crosssession**. |
   |          [/globaloff](../profiling/globalon-and-globaloff.md)           |                                                                                              Inicia o criador de perfil com a coleta de dados em pausa. Use [/globalon](../profiling/globalon-and-globaloff.md) para retomar a criação de perfil.                                                                                               |
   |           [/counter](../profiling/counter.md) **:** `Config`            |                                                                      Coleta informações do contador de desempenho do processador que é especificado em `Config`. As informações do contador são adicionadas aos dados que são coletados em cada evento de criação de perfil.                                                                      |
   |    [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath`     |                                                                                                                        Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil.                                                                                                                         |
   |         [/automark](../profiling/automark.md) **:** `Interval`          |                                                                                      Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms.                                                                                       |
   |       [/events](../profiling/events-vsperfcmd.md) **:** `Config`        |                                                                                         Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Eventos de ETW são coletados em um arquivo separado (.etl).                                                                                         |


3. Inicie o aplicativo Web [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] normalmente.  

## <a name="controlling-data-collection"></a>Controlando coleção de dados  
 Enquanto o aplicativo de destino estiver em execução, você poderá controlar a coleta de dados iniciando e interrompendo a gravação de dados no arquivo de dados do criador de perfil usando as opções do **VSPerfCmd.exe**. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como a inicialização ou o desligamento do aplicativo.  

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados  

-   Os pares de opções a seguir iniciam e interrompem a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.  

    |Opção|Descrição|  
    |------------|-----------------|  
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|  
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pela ID de processo (`PID`).|  
    |[/threadon](../profiling/threadon-and-threadoff.md) **:** `TID` [/threadoff](../profiling/threadon-and-threadoff.md) **:** `TID`|Inicia (**/threadon**) ou interrompe (**/threadoff**) a coleta de dados para o thread especificado pela ID do thread (`TID`).|  

-   Também é possível usar a opção **VSPerfCmd.exe**[/mark](../profiling/mark.md) para inserir uma marca de criação de perfil no arquivo de dados. O comando **/mark** adiciona um identificador, um carimbo de data/hora e uma cadeia de caracteres de texto opcional definida pelo usuário. As marcas podem ser usadas para filtrar dados em exibições de dados e relatórios do criador de perfil.  

## <a name="ending-the-profiling-session"></a>Encerrando a sessão de criação de perfil  
 Para terminar uma sessão de criação de perfil, feche o aplicativo Web [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] de destino, redefina os IIS para interromper o processo cujo perfil foi criado e, em seguida, desligue o criador de perfil.  

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil  

1.  Feche o aplicativo Web [!INCLUDE[vstecasp](../includes/vstecasp-md.md)].  

2.  Feche o processo de trabalho [!INCLUDE[vstecasp](../includes/vstecasp-md.md)], redefinindo os IIS (Serviços de Informações da Internet). Tipo:  

     **IISReset /stop**  

3.  Desligue o criador de perfil. Tipo:  

     **VSPerfCmd**  [/shutdown](../profiling/shutdown.md)  

4.  Reinicie os IIS. Tipo:  

     **IISReset /start**  

## <a name="restoring-the-application-and-computer-configuration"></a>Restaurando a Configuração do Aplicativo e do Computador  
 Quando você tiver concluído todos os perfis, substitua o arquivo web.config, desmarque as variáveis de ambiente de criação de perfil e reinicie o computador para restaurar o aplicativo e o servidor para os estados em que estavam antes da criação de perfil.  

#### <a name="to-restore-the-application-and-computer-configuration"></a>Para restaurar a configuração do aplicativo e do computador  

1.  Substitua o arquivo web.config por uma cópia do arquivo original.  

2.  Desmarque as variáveis de ambiente de criação de perfil. Tipo:  

     **VSPerfCmd /globaloff**  

3.  Reinicie o computador.  

## <a name="see-also"></a>Consulte também  
 [Criando perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [Exibições de dados do método de instrumentação](../profiling/instrumentation-method-data-views.md)



