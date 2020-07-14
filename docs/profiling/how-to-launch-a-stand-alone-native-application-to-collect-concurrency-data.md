---
title: Linha de comando do profiler-abrir aplicativo cliente nativo, obter dados de simultaneidade
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: e5aed651-afed-4b70-9a7e-1a6032cc614f
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- cplusplus
ms.openlocfilehash: 0aeebe82e3c7b574b65ab463a7bfd986d43d46ef
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85327658"
---
# <a name="how-to-launch-a-stand-alone-native-application-with-the-profiler-to-collect-concurrency-data-by-using-the-command-line"></a>Como iniciar um aplicativo nativo autônomo com o criador de perfil para coletar dados de simultaneidade usando a linha de comando
Este tópico descreve como usar ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para iniciar um aplicativo nativo autônomo (cliente) e coletar dados de simultaneidade de thread e processo.

 Uma sessão de criação de perfil tem as seguintes partes:

- Iniciar o aplicativo com o criador de perfil

- Controlando a coleta de dados

- Encerrando a sessão de criação de perfil

> [!NOTE]
> Para obter o caminho para as ferramentas de criação de perfil, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md). Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de Prompt de Comando ou adicioná-lo ao próprio comando.

## <a name="start-the-application-with-the-profiler"></a>Iniciar o aplicativo com o criador de perfil
 Para iniciar um aplicativo de destino com o criador de perfil, use as opções [/start](../profiling/vsperfcmd.md) e **/launch** do **VSPerfCmd.exe** para inicializar o Criador de Perfil e iniciar o aplicativo. Você pode especificar **/start** e **/launch** e suas respectivas opções. Você também pode adicionar a opção **/globaloff** para pausar a coleta de dados no início do aplicativo de destino. Depois, você usa **/globalon** para começar a coletar dados.

#### <a name="to-start-an-application-with-the-profiler"></a>Para iniciar um aplicativo com o criador de perfil

1. Em um prompt de comando, digite o comando a seguir:

     [VSPerfCmd](../profiling/vsperfcmd.md) **/Start: Concurrency/output:** `OutputFile` [ `Options` ]

     A opção [/output](../profiling/output.md)**:** `OutputFile` é necessária com **/Start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).

     É possível usar qualquer uma das opções na tabela a seguir com a opção **/start:concurrency**.

    |Opção|Descrição|
    |------------|-----------------|
    |[/WinCounter](../profiling/wincounter.md) **:**`WinCounterPath`|Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil.|
    |[/AutoMark](../profiling/automark.md) **:**`Interval`|Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O valor padrão é 500.|
    |[/Events](../profiling/events-vsperfcmd.md) **:**`Config`|Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Eventos de ETW são coletados em um arquivo separado (.etl).|

2. Inicie o aplicativo de destino digitando:

     **VSPerfCmd**  [/Launch](../profiling/launch.md) **:** `AppName` [ `Options` ]

     É possível usar qualquer uma das opções na tabela a seguir com a opção **/launch**.

    |Opção|Descrição|
    |------------|-----------------|
    |[/args](../profiling/args.md) **:**`Arguments`|Especifica uma cadeia de caracteres que contém os argumentos de linha de comando a serem passados para o aplicativo de destino.|
    |[/console](../profiling/console.md)|Inicia o aplicativo de destino de linha de comando em uma janela separada.|
    |[/TargetCLR](../profiling/targetclr.md) **:**`CLRVersion`|Especifica a versão do CLR (Common Language Runtime) a ser analisada se o aplicativo carregar mais de uma versão do CLR.|

## <a name="control-data-collection"></a>Controlar a coleta de dados
 Enquanto o aplicativo de destino estiver em execução, você poderá controlar a coleta de dados Iniciando e interrompendo a gravação de dados no arquivo com opções de *VSPerfCmd.exe* . Controlando a coleta de dados, é possível coletar dados de uma parte específica da execução do programa, como o início ou o desligamento do aplicativo.

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados

- Os pares de opções na tabela a seguir iniciam e param a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.

    |Opção|Descrição|
    |------------|-----------------|
    |[/GLOBALON/GLOBALOFF](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|
    |[/ProcessOn](../profiling/processon-and-processoff.md) **:** `PID` [/ProcessOff](../profiling/processon-and-processoff.md) **:**`PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo que a ID de processo (`PID`) especificar.|
    |[/Attach](../profiling/attach.md) **:**{ `PID`&#124;`ProcName` } [/Detach](../profiling/detach.md)[**:**{ `PID`&#124;`ProcName` }]|**/attach** começa a coletar dados para o processo que a ID de processo (`PID`) ou o nome de processo (*ProcName*) especificar. **/detach** interrompe a coleta de dados para o processo especificado ou para todos os processos se nenhum processo for especificado.|

- Também é possível usar a opção **VSPerfCmd.exe**[/mark](../profiling/mark.md) para inserir uma marca de criação de perfil no arquivo de dados. O comando **/mark** adiciona um identificador, um carimbo de data/hora e uma cadeia de caracteres de texto opcional definida pelo usuário. As marcas podem ser usadas para filtrar dados em exibições de dados e relatórios do criador de perfil.

## <a name="end-the-profiling-session"></a>Encerrar a sessão de criação de perfil
 Para encerrar uma sessão de criação de perfil, o criador de perfil não pode estar coletando dados. Você pode parar a coleta de dados de simultaneidade ao fechar o aplicativo analisado ou ao invocar a opção **VSPerfCmd /detach**. Depois, você invoca a opção **VSPerfCmd /shutdown** para desligar o criador de perfil e fechar o arquivo de dados de criação de perfil.

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil

1. Desanexe o criador de perfil do aplicativo de destino fechando-o ou digitando o seguinte comando no prompt de comando:

     **VSPerfCmd /detach**

2. Desligue o criador de perfil digitando o seguinte comando em um prompt de comando:

     **VSPerfCmd**  [/Shutdown](../profiling/shutdown.md)