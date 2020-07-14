---
title: Anexar o criador de perfil ao aplicativo nativo e coletar dados de simultaneidade
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 12d3e0f3-4b74-4e66-8fbf-8ac99bd4f91c
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- cplusplus
ms.openlocfilehash: dcc125f795a29f53abb07920aa11c9a5e6ee966b
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85329523"
---
# <a name="how-to-attach-the-profiler-to-a-native-stand-alone-application-and-collect-concurrency-data-by-using-the-command-line"></a>Como anexar o criador de perfil a um aplicativo independente nativo e coletar dados de simultaneidade usando a linha de comando
Este artigo descreve como usar as ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para anexar o criador de perfil a um aplicativo independente nativo (C/C++) em execução e coletar dados de contenção do thread.

> [!NOTE]
> Para obter o caminho para as ferramentas de criação de perfil, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md). Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de Prompt de Comando ou adicioná-lo ao próprio comando.

 Enquanto o criador de perfil estiver anexado ao aplicativo, você pode pausar e retomar a coleta de dados. Para concluir uma sessão de criação de perfil, o Criador de perfil não pode mais estar anexado ao aplicativo e o Criador de perfil deve ser desligado explicitamente.

## <a name="attach-the-profiler-to-a-running-native-application"></a>Anexar o criador de perfil a um aplicativo nativo em execução

#### <a name="to-attach-the-profiler-to-a-running-native-application"></a>Para anexar o criador de perfil a um aplicativo nativo em execução

1. Em um prompt de comando, digite o comando a seguir:

     [VSPerfCmd](../profiling/vsperfcmd.md) **/start:concurrency**

     É possível usar qualquer uma das opções na tabela a seguir com a opção **/start:concurrency**.

    |Opção|Descrição|
    |------------|-----------------|
    |[/User](../profiling/user-vsperfcmd.md) **:**[ `Domain\` ]`Username`|Especifica o domínio e o nome de usuário opcional da conta que receberá acesso ao criador de perfil.|
    |[/CrossSession](../profiling/crosssession.md)|Habilita a criação de perfil de processos em outras sessões de logon.|
    |[/WinCounter](../profiling/wincounter.md) **:**`WinCounterPath`|Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil.|
    |[/AutoMark](../profiling/automark.md) **:**`Interval`|Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O valor padrão é 500.|
    |[/Events](../profiling/events-vsperfcmd.md) **:**`Config`|Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Eventos de ETW são coletados em um arquivo separado (.etl).|

2. Anexe o criador de perfil ao aplicativo de destino digitando o seguinte comando:

     **VSPerfCmd**  [/Attach](../profiling/attach.md) **:**{ `PID`&#124;`ProcName` }

     `PID` especifica a ID do processo ou o nome do aplicativo de destino. É possível exibir as IDs de processo de todos os processos em execução no Gerenciador de Tarefas do Windows.

## <a name="control-data-collection"></a>Controlar a coleta de dados
 Enquanto o aplicativo de destino estiver em execução, você pode controlar a coleta de dados iniciando e parando a gravação de dados no arquivo usando as opções de *VSPerfCmd.exe*. Controlando a coleta de dados, é possível coletar dados de uma parte específica da execução do programa, como o início ou o desligamento do aplicativo.

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados

- Os pares de opções na tabela a seguir iniciam e param a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.

    |Opção|Descrição|
    |------------|-----------------|
    |[/GLOBALON/GLOBALOFF](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|
    |[/ProcessOn](../profiling/processon-and-processoff.md) **:** `PID` [/ProcessOff](../profiling/processon-and-processoff.md) **:**`PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo que a ID de processo (`PID`) especificar.|
    |[/Attach](../profiling/attach.md) **:**{ `PID`&#124;`ProcName` } [/Detach](../profiling/detach.md)[**:**{ `PID`&#124;`ProcName` }]|**/attach** começa a coletar dados para o processo que a ID de processo (`PID`) ou o nome de processo (*ProcName*) especificar. **/detach** interrompe a coleta de dados para o processo especificado ou para todos os processos se nenhum processo for especificado.|

## <a name="end-the-profiling-session"></a>Encerrar a sessão de criação de perfil
 Para encerrar uma sessão de criação de perfil, o criador de perfil não pode estar coletando dados. É possível interromper a coleta de dados de um aplicativo cujo perfil foi criado com o método de amostragem, fechando o aplicativo ou invocando a opção **VSPerfCmd/detach**. Depois, invoque a opção **VSPerfCmd /shutdown** para desativar o criador de perfil e fechar o arquivo de dados de criação de perfil.

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil

1. Desanexe o criador de perfil do aplicativo de destino fechando-o ou digitando o seguinte comando:

     **VSPerfCmd /detach**

2. Desligue o criador de perfil digitando o seguinte comando:

     **VSPerfCmd**  [/Shutdown](../profiling/shutdown.md)
