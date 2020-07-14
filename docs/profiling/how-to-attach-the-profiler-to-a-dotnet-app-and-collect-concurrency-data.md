---
title: Anexar o criador de perfil a um aplicativo .NET para coletar dados de simultaneidade | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: fdd41576-797e-4312-8520-fee7bb767e4a
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: ab5ae5059b5315d37f6b471c31026e6fe6609e8b
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85330157"
---
# <a name="how-to-attach-the-profiler-to-a-net-framework-stand-alone-application-to-collect-concurrency-data-by-using-the-command-line"></a>Como anexar o criador de perfil a um aplicativo .NET Framework independente para coletar dados de simultaneidade usando a linha de comando
Este artigo descreve como usar as ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para anexar o criador de perfil a um aplicativo (cliente) .NET Framework independente em execução e coletar dados de simultaneidade de thread e do processo.

> [!NOTE]
> Para obter o caminho para as ferramentas de criação de perfil, consulte [Walkthrough: usando APIs do profiler](../profiling/walkthrough-using-profiler-apis.md). Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar as ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de prompt de comando ou adicioná-lo ao próprio comando. Para saber mais, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).

 Enquanto o criador de perfil estiver anexado ao aplicativo, você pode pausar e retomar a coleta de dados. Para encerrar uma sessão de criação de perfil, o criador de perfil não deve mais estar anexado ao aplicativo e precisa ser desligado explicitamente.

## <a name="attach-the-profiler"></a>Anexar o criador de perfil

#### <a name="to-attach-the-profiler-to-a-running-net-framework-application"></a>Para anexar o Criador de Perfil a um aplicativo do .NET Framework em execução

1. Abra una janela de prompt de comando.

2. Inicie o criador de perfil. Tipo:

     [VSPerfCmd](../profiling/vsperfcmd.md) **/Start: Concurrency/output:** `OutputFile` [ `Options` ]

     A opção [/output](../profiling/output.md)**:** `OutputFile` é necessária com **/Start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).

     É possível usar qualquer uma das opções a seguir com a opção **/start:concurrency**.

    |Opção|Descrição|
    |------------|-----------------|
    |[/WinCounter](../profiling/wincounter.md) **:**`WinCounterPath`|Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil.|
    |[/AutoMark](../profiling/automark.md) **:**`Interval`|Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms.|
    |[/Events](../profiling/events-vsperfcmd.md) **:**`Config`|Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Eventos de ETW são coletados em um arquivo separado (.etl).|

3. Inicie o aplicativo de destino normalmente.

4. Anexe o criador de perfil ao aplicativo de destino. Tipo:

     **VSPerfCmd /attach:** `PID` [**/lineoff**] [**/targetclr:**`Version`]

    - `PID` especifica a ID do processo ou o nome do aplicativo de destino. É possível exibir as IDs de processo de todos os processos em execução no Gerenciador de Tarefas do Windows.

    - [/lineoff](../profiling/lineoff.md) desabilita a coleta de dados de número de linha.

    - [/TargetCLR](../profiling/targetclr.md) **:** `Version` especifica a versão do Common Language Runtime (CLR) para o perfil quando mais de uma versão do tempo de execução é carregada em um aplicativo. Opcional.

## <a name="control-data-collection"></a>Controlar a coleta de dados
 Enquanto o aplicativo de destino estiver em execução, você pode controlar a coleta de dados iniciando e parando a gravação de dados no arquivo usando as opções de *VSPerfCmd.exe*. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como o início ou o desligamento do aplicativo.

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados

- Os seguintes pares de *VSPerfCmd.exe* opções iniciam e param a coleta de dados. Especifica cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.

    |Opção|Descrição|
    |------------|-----------------|
    |[/GLOBALON/GLOBALOFF](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|
    |[/ProcessOn](../profiling/processon-and-processoff.md) **:** `PID` [/ProcessOff](../profiling/processon-and-processoff.md) **:**`PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pela ID de processo (`PID`).|
    |[/Attach](../profiling/attach.md) **:**{ `PID`&#124;`ProcName` } [/Detach](../profiling/detach.md)[**:**{ `PID`&#124;`ProcName` }]|**/attach** começa a coletar dados para o processo especificado pela ID de processo (`PID`) ou pelo nome de processo (ProcName). **/detach** interrompe a coleta de dados para o processo especificado ou para todos os processos se nenhum processo específico for especificado.|

## <a name="end-the-profiling-session"></a>Encerrar a sessão de criação de perfil
 Para encerrar uma sessão de criação de perfil, o criador de perfil não pode estar coletando dados. É possível interromper a coleta de dados de um aplicativo analisado com o método de simultaneidade fechando o aplicativo ou invocando a opção **VSPerfCmd /detach**. Depois, invoque a opção **VSPerfCmd /shutdown** para desativar o criador de perfil e fechar o arquivo de dados de criação de perfil. O comando **VSPerfClrEnv /off** limpa as variáveis de ambiente da criação de perfil.

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil

1. Siga um destes procedimentos para desanexar o criador de perfil do aplicativo de destino.

    - Digite **VSPerfCmd/Detach**

         -ou-

    - Feche o aplicativo de destino.

2. Desligue o criador de perfil. Tipo:

     VSPerfCmd[/Shutdown](../profiling/shutdown.md)
