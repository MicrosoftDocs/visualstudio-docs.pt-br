---
title: Como instrumentar um aplicativo Web ASP .NET compilado dinamicamente e coletar dados de memória usando a linha de comando do criador de perfil | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 2cdd9903-39db-47e8-93dd-5e6a21bc3435
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- aspnet
ms.openlocfilehash: 9c1d908a29d4255401aaad4567b56be16ce467cb
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49862665"
---
# <a name="how-to-instrument-a-dynamically-compiled-aspnet-web-application-and-collect-memory-data-by-using-the-profiler-command-line"></a>Como instrumentar um aplicativo Web ASP.NET compilado dinamicamente e coletar dados de memória usando a linha de comando do criador de perfil
Este tópico descreve como usar as ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para coletar dados detalhados de alocação de memória do .NET e dados de tempo de vida do objeto de um aplicativo Web [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] compilado dinamicamente usando o método de criação de perfil por instrumentação.  

> [!NOTE]
>  As ferramentas de linha de comando das Ferramentas de Criação de Perfil estão localizadas no subdiretório *\Team Tools\Performance Tools* do diretório de instalação do [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)]. Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de prompt de comando ou adicioná-lo ao próprio comando. Para saber mais, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).  

 Para coletar dados de desempenho de um aplicativo Web [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)], modifique o arquivo *web.config* do aplicativo de destino para permitir que a ferramenta [VSInstr.exe](../profiling/vsinstr.md) instrumente os arquivos do aplicativo compilado dinamicamente. Use a ferramenta [VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) para configurar o servidor que hospeda o aplicativo Web [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] e habilite a criação de perfil de memória do .NET, definindo as variáveis de ambiente adequadas e, em seguida, reinicie o computador.  

 Para coletar dados, inicie o criador de perfil e, em seguida, execute o aplicativo de destino. Enquanto o criador de perfil é anexado ao aplicativo, você pode pausar e retomar a coleta de dados. Ao terminar de coletar os dados apropriados, feche o aplicativo, feche o processo de trabalho de Serviços de Informações da Internet (IIS) e, em seguida, desligue o criador de perfil.  

 Quando você tiver concluído o trabalho de criação de perfil, restaure o arquivo *web.config* e o servidor Web para seus estados originais.  

## <a name="configure-the-aspnet-web-application-and-the-web-server"></a>Configurar o aplicativo Web ASP.NET e o servidor Web  

#### <a name="to-configure-the-aspnet-web-application-and-the-web-server"></a>Para configurar o aplicativo Web ASP.NET e o servidor Web  

1.  Modifique o arquivo *web.config* do aplicativo de destino. Confira [Como modificar arquivos web.config para instrumentar e criar perfil de aplicativos Web ASP.NET compilados dinamicamente](../profiling/how-to-modify-web-config-files-to-instrument-dynamically-compiled-aspnet-apps.md).  

2.  Abra uma janela de prompt de comando no computador que hospeda o aplicativo Web.  

3.  Inicialize as variáveis de ambiente de criação de perfil. Tipo:  

     **VSPerfClrEnv /globaltracegc**  

     -ou-  

     **VSPerfClrEnv /globaltracegclife**  

    -   **/globaltracegc** habilita a coleta de dados de alocação de memória.  

    -   **/globaltracegclife** habilita a coleta de dados de alocação de memória e dados de tempo de vida do objeto.  

4.  Reinicie o computador.  

## <a name="run-the-profiling-session"></a>Executar a sessão de criação de perfil  

#### <a name="to-profile-the-aspnet-web-application"></a>Para criar o perfil do aplicativo Web ASP.NET  

1. Inicie o criador de perfil. Tipo:  

    **VSPerfCmd** [/start](../profiling/start.md) **:trace** [/output](../profiling/output.md) **:** `OutputFile` [`Options`]  

   - A opção **/start:trace** inicializa o criador de perfil.  

   - A opção **/output:**`OutputFile` é necessária com **/start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.*vsp*).  

     É possível usar qualquer uma das opções a seguir com a opção **/start:trace**.  

   > [!NOTE]
   >  Normalmente, as opções **/user** e **/crosssession** são necessárias para aplicativos ASP.NET.  

   | Opção | Descrição |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:**[`Domain`**\\**]`UserName` | Especifica o domínio e o nome de usuário opcional da conta que possui o processo de trabalho [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)]. Esta opção será necessária se o processo estiver sendo executado como um usuário diferente do usuário conectado. O nome é listado na coluna **Nome de Usuário** na guia **Processos** do Gerenciador de Tarefas do Windows. |
   | [/crosssession](../profiling/crosssession.md) | Habilita a criação de perfil de processos em outras sessões. Esta opção será necessária se o aplicativo estiver em execução em uma sessão diferente. A ID da sessão é listada na coluna **ID da Sessão** na guia **Processos** do Gerenciador de Tarefas do Windows. **/CS** pode ser especificado como uma abreviação de **/crosssession**. |
   | [/globaloff](../profiling/globalon-and-globaloff.md) | Inicia o criador de perfil com a coleta de dados em pausa. Use [/globalon](../profiling/globalon-and-globaloff.md) para retomar a criação de perfil. |
   | [/counter](../profiling/counter.md) **:** `Config` | Coleta informações do contador de desempenho do processador especificado em `Config`. As informações do contador são adicionadas aos dados coletados em cada evento de criação de perfil. |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil. |
   | [/automark](../profiling/automark.md) **:** `Interval` | Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms. |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Os eventos do ETW são coletados em um arquivo separado (.*etl*). |


2. Inicie o aplicativo Web [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] normalmente.  

## <a name="control-data-collection"></a>Controlar a coleta de dados  
 Enquanto o aplicativo de destino estiver em execução, você poderá controlar a coleta de dados iniciando e interrompendo a gravação de dados no arquivo de dados do criador de perfil usando as opções do *VSPerfCmd.exe*. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como a inicialização ou o desligamento do aplicativo.  

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados  

-   Os pares de opções a seguir iniciam e interrompem a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.  

    |Opção|Descrição|  
    |------------|-----------------|  
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|  
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pela ID de processo (`PID`).|  
    |[/threadon](../profiling/threadon-and-threadoff.md) **:** `TID` [/threadoff](../profiling/threadon-and-threadoff.md) **:** `TID`|Inicia (**/threadon**) ou interrompe (**/threadoff**) a coleta de dados para o thread especificado pela ID do thread (`TID`).|  

-   Também é possível usar a opção **VSPerfCmd.exe**[/mark](../profiling/mark.md) para inserir uma marca de criação de perfil no arquivo de dados. O comando **/mark** adiciona um identificador, um carimbo de data/hora e uma cadeia de caracteres de texto opcional definida pelo usuário. As marcas podem ser usadas para filtrar dados em exibições de dados e relatórios do criador de perfil.  

## <a name="end-the-profiling-session"></a>Encerrar a sessão de criação de perfil  
 Para terminar uma sessão de criação de perfil, feche o aplicativo Web [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] de destino, interrompa o IIS (Serviços de Informações da Internet) para interromper o processo cujo perfil foi criado e, em seguida, desligue o criador de perfil. depois, reinicie os IIS.  

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil  

1. Feche o aplicativo Web [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)].  

2. Feche o processo de trabalho [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)], redefinindo os IIS (Serviços de Informações da Internet). Tipo:  

    **IISReset /stop**  

3. Desligue o criador de perfil. Tipo:  

    **VSPerfCmd** [/shutdown](../profiling/shutdown.md)  

4. Reinicie os IIS. Tipo:  

    **IISReset /start**  

## <a name="restore-the-application-and-computer-configuration"></a>Restaurar a configuração do aplicativo e do computador  
 Quando você tiver concluído todas as criações de perfis, substitua o arquivo *web.config*, limpe as variáveis de ambiente de criação de perfil e reinicie o computador para restaurar o servidor e o aplicativo [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] para seus estados originais.  

#### <a name="to-restore-the-application-and-computer-configuration"></a>Para restaurar a configuração do aplicativo e do computador  

1.  Substitua o arquivo *web.config* por uma cópia do arquivo original.  

2.  (Opcional). Desmarque as variáveis de ambiente de criação de perfil. Tipo:  

     **VSPerfCmd /globaloff**  

3.  Reinicie o computador.  

## <a name="see-also"></a>Consulte também  
 [Criar o perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [Exibições de dados da memória do .NET](../profiling/dotnet-memory-data-views.md)
