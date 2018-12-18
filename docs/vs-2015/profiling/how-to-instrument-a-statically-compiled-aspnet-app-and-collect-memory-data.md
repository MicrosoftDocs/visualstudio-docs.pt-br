---
title: Como instrumentar um aplicativo Web ASP .NET compilado estaticamente e coletar dados de memória usando a linha de comando do criador de perfil | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ea1dcb7c-1dc3-49ff-9418-8795b5b3d3bc
caps.latest.revision: 21
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1f1ffce16632d0daceaf5e917dbbe62dadd29cc2
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51750167"
---
# <a name="how-to-instrument-a-statically-compiled-aspnet-web-application-and-collect-memory-data-by-using-the-profiler-command-line"></a>Como instrumentar um aplicativo Web do ASP.NET compilado estaticamente e coletar dados de memória usando a linha de comando do criador de perfil
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico descreve como usar as ferramentas da linha de comando das Ferramentas de criação de perfil do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para instrumentar um componente Web do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] pré-compilado ou site da Web e coletar dados detalhados de alocação de memória .NET, tempo de vida do objeto e de tempo.  

> [!NOTE]
>  As ferramentas de linha de comando das Ferramentas de Criação de Perfil ficam localizadas no subdiretório \Team Tools\Performance Tools do diretório de instalação do [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]. Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de prompt de comando ou adicioná-lo ao próprio comando. Para obter mais informações, consulte [Especificando o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).  

 Para coletar dados de um componente Web de [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] usando o método de instrumentação, use a ferramenta [VSInstr.exe](../profiling/vsinstr.md) para gerar uma versão instrumentada do componente. No computador que hospeda o componente, substitua a versão não instrumentada do componente pela versão instrumentada. Depois, use a ferramenta [VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) para inicializar as variáveis de ambiente de criação de perfil global e reinicie o computador host. Em seguida, inicie o criador de perfil.  

 Quando o componente instrumentado é executado, os dados de tempo são automaticamente coletados para um arquivo de dados. Você pode pausar e retomar a coleta de dados durante a sessão de criação de perfil.  

 Para encerrar uma sessão de criação de perfil, feche o processo de trabalho [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] que hospeda o componente e desligue explicitamente o criador de perfil. Na maioria dos casos, recomendamos desmarcar as variáveis de ambiente de criação de perfil no final de uma sessão.  

## <a name="starting-to-profile"></a>Iniciando o perfil  

#### <a name="to-instrument-an-aspnet-web-component-and-start-profiling"></a>Para instrumentar um componente Web do ASP.NET e iniciar a criação de perfil  

1. Use a ferramenta **VSInstr** para gerar uma versão instrumentada do aplicativo de destino. Se necessário, substitua os binários do aplicativo no computador host do ASP.NET com os binários instrumentados.  

2. Abrir uma janela do Prompt de comando  

3. Inicialize as variáveis de ambiente de criação de perfil do .NET. Em uma janela de prompt de comando, digite:  

    **VSPerfClrEnv /globaltracegc**  

    -ou-  

    **VSPerfClrEnv /globaltracegclife**  

   -   **/globaltracegc** coleta dados de tempo e de alocação de memória do .NET.  

   -   **/globaltracegclife** coleta dados detalhados de alocação de memória do .NET, tempo de vida do objeto e dados tempo.  

4. Reinicie o computador.  

5. Abra uma janela do prompt de comando.  

6. Inicie o criador de perfil. Em uma janela de prompt de comando, digite:  

    **VSPerfCmd /start:trace /output:** `OutputFile` [`Options`]  

   - A opção [/start](../profiling/start.md)**:trace** inicializa o criador de perfil.  

   - A opção [/output](../profiling/output.md)**:**`OutputFile` é necessária com **/start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).  

     É possível usar qualquer uma das opções a seguir com a opção **/start:trace**.  

   > [!NOTE]
   >  Normalmente, as opções **/user** e **/crosssession** são necessárias para aplicativos ASP.NET.  

   |                                 Opção                                  |                                                                                                                                            Descrição                                                                                                                                             |
   |-------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | [/user](../profiling/user-vsperfcmd.md) **:**[`Domain`**\\**]`UserName` |  Especifica o domínio e o nome de usuário opcional da conta que possui o processo de trabalho do ASP.NET. Esta opção será necessária se o processo for executado como um usuário diferente do usuário conectado. O nome é listado na coluna Nome de Usuário na guia Processos do Gerenciador de tarefas do Windows.   |
   |              [/crosssession](../profiling/crosssession.md)              | Habilita a criação de perfil de processos em outras sessões. Esta opção será necessária se o aplicativo estiver em execução em uma sessão diferente. A ID da sessão é listada na coluna ID da Sessão na guia Processos do Gerenciador de Tarefas do Windows. **/CS** pode ser especificado como uma abreviação de **/crosssession**. |
   |    [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath`     |                                                                                                             Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil.                                                                                                              |
   |         [/automark](../profiling/automark.md) **:** `Interval`          |                                                                           Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms.                                                                            |
   |       [/events](../profiling/events-vsperfcmd.md) **:** `Config`        |                                                                              Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Eventos de ETW são coletados em um arquivo separado (.etl).                                                                              |
   |          [/globaloff](../profiling/globalon-and-globaloff.md)           |                                                                      Para iniciar o criador de perfil com a coleta de dados em pausa, adicione a opção **/globaloff** na linha de comando **/start**. Use **/globalon** para retomar a criação de perfil.                                                                       |


7. Abra o site da Web que contém o componente instrumentado.  

## <a name="controlling-data-collection"></a>Controlando coleção de dados  
 Enquanto o aplicativo de destino estiver em execução, você pode controlar a coleta de dados iniciando e parando a gravação de dados no arquivo usando as opções de **VSPerfCmd.exe**. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como a inicialização ou o desligamento do aplicativo.  

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados  

-   Os pares de opções a seguir iniciam e interrompem a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.  

    |Opção|Descrição|  
    |------------|-----------------|  
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|  
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pela ID de processo (`PID`).|  
    |[/threadon](../profiling/threadon-and-threadoff.md) **:** `TID` [/threadoff](../profiling/threadon-and-threadoff.md) **:** `TID`|Inicia (**/threadon**) ou interrompe (**/threadoff**) a coleta de dados para o thread especificado pela ID do thread (`TID`).|  

## <a name="ending-the-profiling-session"></a>Encerrando a sessão de criação de perfil  
 Para terminar uma sessão de criação de perfil, feche o aplicativo Web [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] e use os o comando **IISReset** do IIS (Serviços de Informações da Internet) para fechar o processo de trabalho do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)]. Chame a opção **VSPerfCmd** [/shutdown](../profiling/shutdown.md) para desativar o criador de perfil e fechar o arquivo de dados de criação de perfil. O comando **VSPerfClrEnv /globaloff** limpa as variáveis de ambiente da criação de perfil. Você deve reiniciar o computador para que as novas configurações de ambiente sejam aplicadas.  

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil  

1.  Feche o aplicativo Web [!INCLUDE[vstecasp](../includes/vstecasp-md.md)].  

2.  Feche o processo de trabalho [!INCLUDE[vstecasp](../includes/vstecasp-md.md)]. Tipo:  

     **IISReset /stop**  

3.  Desligue o criador de perfil. Tipo:  

     **VSPerfCmd /shutdown**  

4.  (Opcional). Desmarque as variáveis de ambiente de criação de perfil. Tipo:  

     **VSPerfCmd /globaloff**  

5.  Reinicie o computador. Se necessário, reinicie o IIS. Tipo:  

     **IISReset /start**  

## <a name="see-also"></a>Consulte também  
 [Criando perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [Exibições de dados da memória do .NET](../profiling/dotnet-memory-data-views.md)



