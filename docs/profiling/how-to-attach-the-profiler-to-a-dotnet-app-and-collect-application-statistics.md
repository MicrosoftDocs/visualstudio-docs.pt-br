---
title: Anexar o criador de perfil para o aplicativo autônomo do .NET Framework; obter estatísticas de aplicativo
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: b62fcbc1-791f-474e-890a-a6c332e0c9ea
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: 68450129d9bb3e9e67793c0a4155e953abbccc3d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85531801"
---
# <a name="how-to-attach-the-profiler-to-a-net-framework-stand-alone-application-and-collect-application-statistics-by-using-the-command-line"></a>Como anexar o criador de perfil a um aplicativo autônomo do .NET Framework e coletar estatísticas de aplicativo usando a linha de comando
Este artigo descreve como usar as ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para anexar o criador de perfil a um aplicativo (cliente) .NET Framework independente em execução e coletar estatísticas de desempenho usando o método de amostragem.

> [!NOTE]
> Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos UWP também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).
>
> Para obter o caminho para as ferramentas de criação de perfil, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md). Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de Prompt de Comando ou adicioná-lo ao próprio comando.
>
> Adicionar dados de interação de camada a uma execução de criação de perfil requer procedimentos específicos com ferramentas de criação de perfil de linha de comando. Confira [Coletar dados de interação de camada](../profiling/adding-tier-interaction-data-from-the-command-line.md).

 Para coletar dados de desempenho de um aplicativo do .NET Framework, as variáveis de ambiente apropriadas devem ser inicializadas antes de iniciar o aplicativo de destino. Quando criador de perfil estiver anexado ao aplicativo, você poderá pausar e retomar a coleta de dados.

 Para concluir uma sessão de criação de perfil, o Criador de perfil não pode mais estar anexado ao aplicativo e o Criador de perfil deve ser desligado explicitamente. Na maioria dos casos, recomendamos desmarcar as variáveis de ambiente de criação de perfil no final de uma sessão de criação de perfil.

## <a name="attach-the-profiler"></a>Anexar o criador de perfil

#### <a name="to-attach-the-profiler-to-a-running-net-framework-application"></a>Para anexar o Criador de Perfil a um aplicativo do .NET Framework em execução

1. Abra uma janela de Prompt de Comando.

2. Inicialize as variáveis de ambiente de criação de perfil. Tipo:

    **VSPerfClrEnv /sampleon** [**/samplelineoff**]

   - A opção **/samplelineoff** desabilita a coleta de dados do número de linha do código-fonte.

3. Inicie o criador de perfil. Tipo:

    **VSPerfCmd/start: exemplo/output:** `OutputFile` [`Options`]

   - A opção [/start](../profiling/start.md)**:sample** inicializa o criador de perfil.

   - A opção [/output](../profiling/output.md)**:** `OutputFile` é necessária com **/Start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).

     É possível usar qualquer uma das opções a seguir com a opção **/start:sample**.

   | Opção | Descrição |
   | - | - |
   | [/User](../profiling/user-vsperfcmd.md) **:**[ `Domain` **\\** ]`UserName` | Especifica o domínio e o nome de usuário da conta opcionais que possui o processo analisado. Esta opção será necessária apenas se o aplicativo analisado estiver sendo executado como um usuário diferente do usuário conectado. |
   | [/CrossSession](../profiling/crosssession.md) | Habilita a criação de perfil de processos em outras sessões de logon. **/CS** pode ser especificado como uma abreviação de **/crosssession**. Esta opção será necessária se o aplicativo estiver em execução em uma sessão diferente. |
   | [/WinCounter](../profiling/wincounter.md) **:**`WinCounterPath` | Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil. |
   | [/AutoMark](../profiling/automark.md) **:**`Interval` | Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms. |
   | [/Events](../profiling/events-vsperfcmd.md) **:**`Config` | Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Os eventos ETW são coletados em um separado (.* ETL*). |

4. Se necessário, inicie o aplicativo de destino normalmente.

5. Anexe o criador de perfil ao aplicativo de destino. Tipo:

    **VSPerfCmd/Attach:**{ `PID`&#124;`ProcessName` } [ `Sample Event` ] [**/TargetCLR:** `Version` ]

   - `PID` especifica a ID do processo ou o nome do aplicativo de destino. `ProcessName` especifica o nome do processo. Observe que, se você especificar `ProcessName` e vários processos que têm o mesmo nome estiverem em execução, os resultados serão imprevisíveis. É possível exibir as IDs de processo de todos os processos em execução no Gerenciador de Tarefas do Windows.

   - [/TargetCLR](../profiling/targetclr.md) **:** `Version` especifica a versão do Common Language Runtime (CLR) para o perfil quando mais de uma versão do tempo de execução é carregada em um aplicativo. Opcional.

   - Por padrão, os dados de desempenho têm amostra obtida a cada 10.000.000 ciclos de relógio de processador não interrompidos. Significa aproximadamente uma vez a cada 10 segundos em um processador de 1GH. Você pode especificar uma das opções a seguir para alterar o intervalo do ciclo do relógio ou para especificar um evento de amostragem diferente. [/TargetCLR](../profiling/targetclr.md)**:** `Version` especifica a versão do CLR para o perfil quando mais de uma versão do tempo de execução é carregada em um aplicativo. Opcional.

   |Evento de exemplo|Descrição|
   |-|-|
   |[/timer](../profiling/timer.md) **:**`Interval`|Altera o intervalo de amostragem para o número de ciclos de relógio não interrompidos especificados pelo `Interval`.|
   |[/PF](../profiling/pf.md) [**:** `Interval` ]|Altera o evento de amostragem para falhas de página. Se `Interval` for especificado, define o número de falhas de página entre as amostras. O padrão é 10.|
   |[/Sys](../profiling/sys-vsperfcmd.md) [**:** `Interval` ]|Altera o evento de amostragem para chamadas do sistema do processo para o kernel do sistema operacional (syscalls). Se `Interval` for especificado, define o número de chamadas entre as amostras. O padrão é 10.|
   |[/Counter](../profiling/counter.md) **:**`Config`|Altera o evento de amostragem e o intervalo para o contador de desempenho do processador e o intervalo especificado em `Config`.|

## <a name="control-data-collection"></a>Controlar a coleta de dados
 Quando o aplicativo de destino estiver em execução, você pode controlar a coleta de dados iniciando e interrompendo a gravação de dados no arquivo de dados do criador de perfil usando as opções do *VSPerfCmd.exe*. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como a inicialização ou o desligamento do aplicativo.

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados

- Os pares de opções a seguir iniciam e interrompem a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.

    |Opção|Descrição|
    |------------|-----------------|
    |[/GLOBALON/GLOBALOFF](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|
    |[/ProcessOn](../profiling/processon-and-processoff.md) **:** `PID` [/ProcessOff](../profiling/processon-and-processoff.md) **:**`PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pelo `PID`.|
    |[/Attach](../profiling/attach.md) **:**{ `PID`&#124;`ProcName` } [/Detach](../profiling/detach.md)[**:**{ `PID`&#124;`ProcName` }]|**/attach** começa a coletar dados para o processo especificado pelo `PID` ou pelo nome de processo (ProcName). **/detach** interrompe a coleta de dados para o processo especificado ou para todos os processos se nenhum processo específico for especificado.|

## <a name="end-the-profiling-session"></a>Encerrar a sessão de criação de perfil
 Para concluir uma sessão de criação de perfil, o criador de perfil deve ser desanexado de todos os processos analisados e o criador de perfil deve ser desligado explicitamente. É possível desanexar o criador de perfil de um aplicativo que foi analisado usando o método de amostragem ao fechar o aplicativo ou chamar a opção **VSPerfCmd /detach**. Depois, chame a opção **VSPerfCmd /shutdown** para desativar o criador de perfil e fechar o arquivo de dados de criação de perfil. O comando **VSPerfClrEnv /off** limpa as variáveis de ambiente da criação de perfil.

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil

1. Realize uma das etapas a seguir para desanexar o criador de perfil do aplicativo de destino:

    - Digite **VSPerfCmd/Detach**

         -ou-

    - Feche o aplicativo de destino.

2. Desligue o criador de perfil. Tipo:

     **VSPerfCmd**  [/Shutdown](../profiling/shutdown.md)

3. (Opcional) desmarcar as variáveis de ambiente de criação de perfil. Tipo:

     **VSPerfClrEnv /off**

## <a name="see-also"></a>Confira também
- [Aplicativos Autônomos de Perfil](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [Exibições de dados do método de amostragem](../profiling/profiler-sampling-method-data-views.md)
