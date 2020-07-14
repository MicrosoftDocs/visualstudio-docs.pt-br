---
title: Anexar o criador de perfil a um aplicativo do .NET para coletar dados de memória
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: how-to
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: dbe8f0cdb976dfb687071b231b2907b6b7124b3a
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85328738"
---
# <a name="how-to-attach-the-profiler-to-a-net-framework-stand-alone-application-to-collect-memory-data-by-using-the-command-line"></a>Como anexar o criador de perfil a um aplicativo .NET Framework independente para coletar dados da memória usando a linha de comando

Este artigo descreve como usar as ferramentas de linha de comando das Ferramentas de Criação de Perfil do Visual Studio para anexar o criador de perfil a um aplicativo (cliente) .NET Framework independente em execução e coletar dados da memória.

> [!NOTE]
> Para obter o caminho para as ferramentas de criação de perfil, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md). Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de Prompt de Comando ou adicioná-lo ao próprio comando.

Para anexar a um aplicativo do .NET Framework e coletar dados de memória, você deve usar a ferramenta [VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) para inicializar as variáveis de ambiente apropriadas antes de inicia o aplicativo de destino. Quando criador de perfil estiver anexado ao aplicativo, você poderá usar a ferramenta *VSPerfCmd.exe* para pausar e retomar a coleta de dados.

Para concluir uma sessão de criação de perfil, o criador de perfil deve ser desanexado de todos os processos analisados e o criador de perfil deve ser desligado explicitamente. Na maioria dos casos, recomendamos desmarcar as variáveis de ambiente de criação de perfil no final de uma sessão.

## <a name="attach-the-profiler"></a>Anexar o criador de perfil

### <a name="to-attach-the-profiler-to-a-running-net-framework-application"></a>Para anexar o Criador de Perfil a um aplicativo do .NET Framework em execução

1. Abra uma janela de Prompt de Comando.

2. Inicialize as variáveis de ambiente de criação de perfil. Tipo:

     **VSPerfClrEnv** {**/samplegc** &#124; **/samplegclife**} [**/samplelineoff**]

    - As opções **/samplegc** e **/samplegclife** especificam se serão coletados apenas dados de alocação de memória ou dados de alocação de memória e dados de tempo de vida do objeto. Somente uma opção deve ser especificada.

        |Opção|Descrições|
        |------------|------------------|
        |**/samplegc**|Coleta somente dados de alocação de memória.|
        |**/samplegclife**|Coleta de dados de alocação de memória e de tempo de vida do objeto.|

    - A opção **/samplelineoff** desabilita a coleta de dados do número de linha do código-fonte.

3. Inicie o criador de perfil. Tipo:

     **VSPerfCmd/start: exemplo/output:** `OutputFile` [`Options`]

   - A opção [/start](../profiling/start.md)**:sample** inicializa o criador de perfil.

   - A opção [/output](../profiling/output.md)**:** `OutputFile` é necessária com **/Start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).

     É possível usar qualquer uma das opções a seguir com a opção **/start:sample**.

     | Opção | Descrição |
     | - | - |
     | [/User](../profiling/user-vsperfcmd.md) **:**[ `Domain` **\\** ]`UserName` | Especifica o domínio e o nome de usuário da conta que possui o processo analisado. Esta opção será necessária apenas se o processo estiver sendo executado como um usuário diferente do usuário conectado. O proprietário do processo é listado na coluna Nome de Usuário na guia Processos do Gerenciador de Tarefas do Windows. |
     | [/crosssession &#124; /cs](../profiling/crosssession.md) | Habilita a criação de perfil de processos em outras sessões. Esta opção será necessária se o aplicativo estiver em execução em uma sessão diferente. O identificador da sessão é listado na coluna ID da Sessão na guia Processos do Gerenciador de Tarefas do Windows. **/CS** pode ser especificado como uma abreviação de **/crosssession**. |
     | [/WinCounter](../profiling/wincounter.md) **:**`WinCounterPath` | Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil. |
     | [/AutoMark](../profiling/automark.md) **:**`Interval` | Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms. |

4. Se necessário, inicie o aplicativo de destino normalmente.

5. Anexe o criador de perfil ao aplicativo de destino. Tipo:

     **VSPerfCmd**[/Attach](../profiling/attach.md) **:**{ `PID`&#124;`ProcName` } [[/TargetCLR](../profiling/targetclr.md)**:** `Version` ]  

    - `PID` especifica a ID do processo ou o nome do aplicativo de destino. `ProcessName` especifica o nome do processo. Observe que, se você especificar `ProcessName` e vários processos que têm o mesmo nome estiverem em execução, os resultados serão imprevisíveis. É possível exibir as IDs de processo de todos os processos em execução no Gerenciador de Tarefas do Windows.

    - **/TargetCLR:** `Version` Especifica a versão do Common Language Runtime (CLR) para o perfil quando mais de uma versão do tempo de execução é carregada em um aplicativo. Opcional.

## <a name="control-data-collection"></a>Controlar a coleta de dados

Quando o aplicativo de destino estiver em execução, você pode controlar a coleta de dados iniciando e interrompendo a gravação de dados no arquivo usando as opções de *VSPerfCmd.exe*. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como a inicialização ou o desligamento do aplicativo.

### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados

- Os pares de opções a seguir iniciam e interrompem a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.

    |Opção|Descrição|
    |------------|-----------------|
    |[/GLOBALON/GLOBALOFF](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|
    |[/ProcessOn](../profiling/processon-and-processoff.md) **:** `PID` [/ProcessOff](../profiling/processon-and-processoff.md) **:**`PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pelo `PID`.|
    |[/Attach](../profiling/attach.md) **:**{ `PID`&#124;`ProcName` } [/Detach](../profiling/detach.md)[**:**{ `PID`&#124;`ProcName` }]|**/attach** começa a coletar dados para o processo especificado pelo `PID` ou pelo nome de processo (ProcName). **/detach** interrompe a coleta de dados para o processo especificado ou para todos os processos se nenhum processo específico for especificado.|

## <a name="end-the-profiling-session"></a>Encerrar a sessão de criação de perfil

Para concluir uma sessão de criação de perfil, o criador de perfil deve ser desanexado de todos os processos analisados e o criador de perfil deve ser desligado explicitamente. É possível desanexar o criador de perfil de um aplicativo que foi analisado usando o método de amostragem ao fechar o aplicativo ou chamar a opção **VSPerfCmd /detach**. Depois, você chama a opção **VSPerfCmd /shutdown** para desligar o criador de perfil e fechar o arquivo de dados de criação de perfil. O comando **VSPerfClrEnv /off** limpa as variáveis de ambiente da criação de perfil.

### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil

1. Realize uma das etapas a seguir para desanexar o criador de perfil do aplicativo de destino:

    - Digite **VSPerfCmd/Detach**

         -ou-

    - Feche o aplicativo de destino.

2. Desligue o criador de perfil. Tipo:

     **VSPerfCmd**  [/Shutdown](../profiling/shutdown.md)

3. (Opcional) desmarcar as variáveis de ambiente de criação de perfil. Tipo:

     **VSPerfCmd /off**

## <a name="see-also"></a>Veja também

[Perfis de aplicativos](../profiling/command-line-profiling-of-stand-alone-applications.md) 
 autônomos [Exibições de dados de memória do .net](../profiling/dotnet-memory-data-views.md)
