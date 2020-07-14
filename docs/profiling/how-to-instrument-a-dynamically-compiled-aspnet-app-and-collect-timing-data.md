---
title: Linha de comando do profiler-Instrument Dynamic ASP.NET app, obter dados de tempo
ms.date: 11/04/2016
ms.topic: how-to
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- aspnet
ms.openlocfilehash: f510878c3952cb98bcbee3bfecedf05b87b2658f
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85327964"
---
# <a name="how-to-instrument-a-dynamically-compiled-aspnet-web-application-and-collect-detailed-timing-data-with-the-profiler-by-using-the-command-line"></a>Como instrumentar um aplicativo Web ASP.NET compilado dinamicamente e coletar dados de tempo detalhados com o criador de perfil usando a linha de comando

Este tópico descreve como usar as ferramentas de linha de comando das Ferramentas de Criação de Perfil do Visual Studio para coletar dados de tempo detalhados para um aplicativo [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] compilado dinamicamente usando o método de criação de perfil por instrumentação.

> [!NOTE]
> Para obter o caminho para as ferramentas de criação de perfil, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md). Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de Prompt de Comando ou adicioná-lo ao próprio comando.

Para coletar dados de desempenho de um [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] aplicativo Web, você modifica o arquivo de *web.config* do aplicativo de destino para habilitar a ferramenta de [VSInstr.exe](../profiling/vsinstr.md) para instrumentar os arquivos de aplicativo compilados dinamicamente. Em seguida, use a ferramenta [VSPerfCLREnv. cmd](../profiling/vsperfclrenv.md) para definir as variáveis de ambiente apropriadas no servidor Web para habilitar a criação de perfil e reinicie o computador.

Inicie o criador de perfil e, em seguida, execute o aplicativo de destino. Enquanto o criador de perfil estiver anexado ao aplicativo, você pode pausar e retomar a coleta de dados. Quando você terminar a criação de perfil, feche o aplicativo, feche o processo de trabalho dos IIS (Serviços de Informações da Internet) e, em seguida, desligue o criador de perfil. Quando você concluir o trabalho de criação de perfil, restaure o arquivo de *web.config* e o servidor Web para seus Estados originais.

## <a name="configure-the-aspnet-web-application-and-the-web-server"></a>Configurar o aplicativo Web ASP.NET e o servidor Web

1. Modifique o arquivo de *web.config* do aplicativo de destino. Consulte [como: modificar arquivos de web.config para instrumentar e criar perfil de aplicativos web ASP.NET dinamicamente compilados](../profiling/how-to-modify-web-config-files-to-instrument-dynamically-compiled-aspnet-apps.md).

2. Abra uma janela de Prompt de Comando.

3. Inicialize as variáveis de ambiente de criação de perfil. Tipo:

     **VSPerfClrEnv /globaltraceon**

    - **/globaltraceon** habilita a criação de perfil usando o método de instrumentação.

4. Reinicie o computador.

## <a name="run-the-profiling-session"></a>Executar a sessão de criação de perfil

1. Abra uma janela de Prompt de Comando.

2. Inicie o criador de perfil. Tipo:

     **VSPerfCmd**  [/Start](../profiling/start.md) **: Trace**  [/output](../profiling/output.md) **:** `OutputFile` [ `Options` ]

   - A opção **/Start: Trace** Inicializa o criador de perfil.

   - A opção **/output:** `OutputFile` é necessária com **/Start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.*vsp*).

     É possível usar qualquer uma das opções a seguir com a opção **/start:trace**.

     > [!NOTE]
     > Normalmente, as opções **/user** e **/crosssession** são necessárias para aplicativos ASP.NET.

     | Opção | Descrição |
     | - | - |
     | [/User](../profiling/user-vsperfcmd.md) **:**[ `Domain` **\\** ]`UserName` | Especifica o domínio e o nome de usuário da conta proprietária do processo de trabalho ASP.NET analisado. Esta opção será necessária se o processo estiver sendo executado como um usuário diferente do usuário conectado. O proprietário do processo é listado na coluna **Nome de Usuário** na guia **Processos** do Gerenciador de Tarefas do Windows. |
     | [/CrossSession](../profiling/crosssession.md) | Habilita a criação de perfil de processos em outras sessões de logon. Esta opção será necessária se o aplicativo ASP.NET estiver em execução em uma sessão diferente. O identificador de sessão é listado na coluna **ID da sessão** na guia **processos** do Gerenciador de tarefas do Windows. **/CS** pode ser especificado como uma abreviação de **/crosssession**. |
     | [/globaloff](../profiling/globalon-and-globaloff.md) | Inicia o criador de perfil com a coleta de dados em pausa. Use [/globalon](../profiling/globalon-and-globaloff.md) para retomar a criação de perfil. |
     | [/Counter](../profiling/counter.md) **:**`Config` | Coleta informações do contador de desempenho do processador que é especificado em `Config`. As informações do contador são adicionadas aos dados que são coletados em cada evento de criação de perfil. |
     | [/WinCounter](../profiling/wincounter.md) **:**`WinCounterPath` | Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil. |
     | [/AutoMark](../profiling/automark.md) **:**`Interval` | Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms. |
     | [/Events](../profiling/events-vsperfcmd.md) **:**`Config` | Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Os eventos ETW são coletados em um separado (.* ETL*). |

3. Inicie o aplicativo Web [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] normalmente.

## <a name="control-data-collection"></a>Controlar a coleta de dados

Enquanto o aplicativo de destino estiver em execução, você poderá controlar a coleta de dados iniciando e interrompendo a gravação de dados no arquivo de dados do criador de perfil usando as opções do *VSPerfCmd.exe*. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como a inicialização ou o desligamento do aplicativo.

- Os pares de opções a seguir iniciam e interrompem a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.

    |Opção|Descrição|
    |------------|-----------------|
    |[/GLOBALON/GLOBALOFF](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|
    |[/ProcessOn](../profiling/processon-and-processoff.md) **:** `PID` [/ProcessOff](../profiling/processon-and-processoff.md) **:**`PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pela ID de processo (`PID`).|
    |[/ThreadOn](../profiling/threadon-and-threadoff.md) **:** `TID` [/ThreadOff](../profiling/threadon-and-threadoff.md) **:**`TID`|Inicia (**/threadon**) ou interrompe (**/threadoff**) a coleta de dados para o thread especificado pela ID do thread (`TID`).|

- Também é possível usar a opção **VSPerfCmd.exe**[/mark](../profiling/mark.md) para inserir uma marca de criação de perfil no arquivo de dados. O comando **/mark** adiciona um identificador, um carimbo de data/hora e uma cadeia de caracteres de texto opcional definida pelo usuário. As marcas podem ser usadas para filtrar dados em exibições de dados e relatórios do criador de perfil.

## <a name="end-the-profiling-session"></a>Encerrar a sessão de criação de perfil

Para terminar uma sessão de criação de perfil, feche o aplicativo Web [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] de destino, redefina o IIS para interromper o processo cujo perfil foi criado e, em seguida, desligue o criador de perfil.

1. Feche o aplicativo Web [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)].

2. Feche o processo de trabalho [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)], redefinindo os IIS (Serviços de Informações da Internet). Tipo:

     **IISReset /stop**

3. Desligue o criador de perfil. Tipo:

     **VSPerfCmd**  [/Shutdown](../profiling/shutdown.md)

4. Reinicie o IIS. Tipo:

     **IISReset /start**

## <a name="restore-the-application-and-computer-configuration"></a>Restaurar a configuração do aplicativo e do computador

Quando você tiver concluído toda a criação de perfil, substitua o arquivo *web.config* , desmarque as variáveis de ambiente de criação de perfil e reinicie o computador para restaurar o aplicativo e o servidor para os Estados em que estavam antes da criação de perfil.

1. Substitua o arquivo *web.config* por uma cópia do arquivo original.

2. Desmarque as variáveis de ambiente de criação de perfil. Tipo:

     **VSPerfCmd /globaloff**

3. Reinicie o computador.

## <a name="see-also"></a>Veja também

[Perfis de aplicativos](../profiling/command-line-profiling-of-aspnet-web-applications.md) 
 Web ASP.net [Exibições de dados do método de instrumentação](../profiling/instrumentation-method-data-views.md)
