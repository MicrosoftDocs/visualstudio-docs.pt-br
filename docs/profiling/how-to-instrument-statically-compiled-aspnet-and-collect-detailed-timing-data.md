---
title: Como instrumentar um aplicativo Web ASP .NET compilado estaticamente e coletar dados de tempo detalhados com o criador de perfil usando a linha de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: b260ce68-76e6-4c3b-8062-3c00bd5cf7b8
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- aspnet
ms.openlocfilehash: efb4e449114a0920c5fd73feba10b1e0d9e0be3a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49865396"
---
# <a name="how-to-instrument-a-statically-compiled-aspnet-web-application-and-collect-detailed-timing-data-with-the-profiler-by-using-the-command-line"></a>Como instrumentar um aplicativo Web ASP.NET compilado estaticamente e coletar dados de tempo detalhados com o criador de perfil usando a linha de comando
Este tópico descreve como usar as ferramentas da linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para instrumentar um componente Web ou site do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] pré-compilado e coletar dados de tempo detalhados.  

> [!NOTE]
>  As ferramentas de linha de comando das Ferramentas de Criação de Perfil estão localizadas no subdiretório *\Team Tools\Performance Tools* do diretório de instalação do [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)]. Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de Prompt de Comando ou adicioná-lo ao próprio comando. Para saber mais, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).  
> 
>  Adicionar dados de interação de camada a uma execução de criação de perfil requer procedimentos específicos com ferramentas de criação de perfil de linha de comando. Consulte [Coletando dados de interação entre camadas](../profiling/adding-tier-interaction-data-from-the-command-line.md).  

 Para coletar dados de tempo detalhados de um componente Web de [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] usando o método de instrumentação, use a ferramenta [VSInstr.exe](../profiling/vsinstr.md) para gerar uma versão instrumentada do componente. No computador que hospeda o componente, substitua a versão não instrumentada do componente pela versão instrumentada. Depois, use a ferramenta [VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) para inicializar as variáveis de ambiente de criação de perfil global e reinicie o computador host. Em seguida, inicie o criador de perfil.  

 Quando o componente instrumentado é executado, os dados de tempo são automaticamente coletados para um arquivo de dados. Você pode pausar e retomar a coleta de dados durante a sessão de criação de perfil.  

 Para encerrar uma sessão de criação de perfil, feche o processo de trabalho [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] que hospeda o componente e desligue explicitamente o criador de perfil. Na maioria dos casos, recomendamos desmarcar as variáveis de ambiente de criação de perfil no final de uma sessão.  

## <a name="start-to-profile"></a>Iniciar a criação de perfil  

#### <a name="to-instrument-an-aspnet-web-component-and-start-profiling"></a>Para instrumentar um componente Web ASP.NET e iniciar a criação de perfil  

1. Abra uma janela do Prompt de Comando.  

2. Use a ferramenta **VSInstr** para gerar uma versão instrumentada do aplicativo de destino. Se necessário, substitua os binários do aplicativo no computador host do ASP.NET com os binários instrumentados.  

3. Inicialize as variáveis de ambiente de criação de perfil do .NET. Na janela de Prompt de Comando, digite:  

    **VSPerfClrEnv /globaltraceon**  

4. Reinicie o computador.  

5. Abra uma janela do Prompt de Comando. Se necessário, defina o caminho das ferramentas do criador de perfil.  

6. Inicie o criador de perfil. Tipo:  

    **VSPerfCmd /start:trace /output:** `OutputFile` [`Options`]  

   - A opção [/start](../profiling/start.md)**:trace** inicializa o criador de perfil.  

   - A opção [/output](../profiling/output.md)**:**`OutputFile` é necessária com **/start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).  

     É possível usar qualquer uma das opções a seguir com a opção **/start:trace**.  

   > [!NOTE]
   >  Normalmente, as opções **/user** e **/crosssession** são necessárias para aplicativos ASP.NET.  

   | Opção | Descrição |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:**[`Domain`**\\**]`UserName` | Especifica o domínio e o nome de usuário da conta proprietária do processo de trabalho ASP.NET analisado. Esta opção será necessária se o processo estiver sendo executado como um usuário diferente do usuário conectado. O proprietário do processo é listado na coluna **Nome de Usuário** na guia **Processos** do Gerenciador de Tarefas do Windows. |
   | [/crosssession](../profiling/crosssession.md) | Habilita a criação de perfil de processos em outras sessões de logon. Esta opção será necessária se o aplicativo ASP.NET estiver em execução em uma sessão diferente. O identificador da sessão é listado na coluna ID da Sessão na guia **Processos** do Gerenciador de Tarefas do Windows. **/CS** pode ser especificado como uma abreviação de **/crosssession**. |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil. |
   | [/automark](../profiling/automark.md) **:** `Interval` | Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms. |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Os eventos do ETW são coletados em um arquivo separado (.*etl*). |
   | [/globaloff](../profiling/globalon-and-globaloff.md) | Para iniciar o criador de perfil com a coleta de dados em pausa, adicione a opção **/globaloff** na linha de comando **/start**. Use **/globalon** para retomar a criação de perfil. |


7. Abra o site da Web que contém o componente instrumentado.  

## <a name="control-data-collection"></a>Controlar a coleta de dados  
 Quando o aplicativo de destino estiver em execução, você pode controlar a coleta de dados iniciando e interrompendo a gravação de dados no arquivo usando as opções de *VSPerfCmd.exe*. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como a inicialização ou o desligamento do aplicativo.  

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados  

-   Os pares de opções a seguir iniciam e interrompem a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.  

    |Opção|Descrição|  
    |------------|-----------------|  
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|  
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pela ID de processo (`PID`).|  
    |[/threadon](../profiling/threadon-and-threadoff.md) **:** `TID` [/threadoff](../profiling/threadon-and-threadoff.md) **:** `TID`|Inicia (**/threadon**) ou interrompe (**/threadoff**) a coleta de dados para o thread especificado pela ID do thread (`TID`).|  

## <a name="end-the-profiling-session"></a>Encerrar a sessão de criação de perfil  
 Para terminar uma sessão de criação de perfil, feche o aplicativo Web [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] e use os o comando **IISReset** do IIS (Serviços de Informações da Internet) para fechar o processo de trabalho do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)]. Chame a opção **VSPerfCmd** [/shutdown](../profiling/shutdown.md) para desligar o criador de perfil e fechar o arquivo de dados de criação de perfil.  

 O comando **VSPerfClrEnv /globaloff** limpa as variáveis de ambiente da criação de perfil. Você deve reiniciar o computador para que as novas configurações de ambiente sejam aplicadas.  

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil  

1. Feche o aplicativo Web [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)].  

2. Feche o processo de trabalho [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)]. Tipo:  

    **IISReset /stop**  

3. Desligue o criador de perfil. Tipo:  

    **VSPerfCmd /shutdown**  

4. (Opcional). Desmarque as variáveis de ambiente de criação de perfil. Tipo:  

    **VSPerfCmd /globaloff**  

5. Reinicie o computador.  

## <a name="see-also"></a>Consulte também  
 [Criar o perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [Exibições de dados do método de instrumentação](../profiling/instrumentation-method-data-views.md)