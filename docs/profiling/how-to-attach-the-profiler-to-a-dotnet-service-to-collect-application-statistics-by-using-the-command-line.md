---
title: Anexar criador de perfil ao serviço do .NET para coletar estatísticas do aplicativo
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: a0046c47-26c8-4bec-96a0-81da05e5104a
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: ac59e0e08894ca143df6a68c49e5f5f8b24ebc50
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85328707"
---
# <a name="how-to-attach-the-profiler-to-a-net-service-to-collect-application-statistics-by-using-the-command-line"></a>Como anexar o criador de perfil a um serviço do .NET para coletar estatísticas do aplicativo usando a linha de comando
Este artigo descreve como usar as ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para anexar o criador de perfil a um serviço do .NET Framework e coletar estatísticas de desempenho usando o método de amostragem.

> [!NOTE]
> Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos UWP também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).
>
> Para obter o caminho para as ferramentas de criação de perfil, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md). Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de Prompt de Comando ou adicioná-lo ao próprio comando.
>
> Adicionar dados de interação de camada a uma execução de criação de perfil requer procedimentos específicos com ferramentas de criação de perfil de linha de comando. Confira [Coletar dados de interação de camada](../profiling/adding-tier-interaction-data-from-the-command-line.md).

 Para coletar dados de desempenho de um serviço .NET Framework, você deve usar a ferramenta [VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) para inicializar as variáveis de ambiente apropriadas. Em seguida, reinicie o computador que hospeda o serviço e configure-o para a criação de perfil. Em seguida, anexe o criador de perfil ao processo do serviço. Enquanto o criador de perfil estiver anexado ao serviço, você pode pausar e retomar a coleta de dados.

 Para concluir uma sessão de criador de perfil, o criador de perfil deve ser desanexado do serviço e desligado explicitamente. Na maioria dos casos, recomendamos desmarcar as variáveis de ambiente de criação de perfil no final de uma sessão.

## <a name="attach-the-profiler"></a>Anexar o criador de perfil

#### <a name="to-attach-the-profiler-to-a-net-framework-service"></a>Para anexar o criador de perfil a um serviço do .NET Framework

1. Instale o serviço.

2. Abra una janela de prompt de comando.

3. Inicialize as variáveis de ambiente de criação de perfil. Tipo:

    **VSPerfClrEnv /globalsampleon** [**/samplelineoff**]

   - **/globalsampleon** habilita a amostragem.

   - **/samplelineoff** desabilita a atribuição de dados coletados a linhas específicas do código-fonte. Quando essa opção for especificada, os dados serão atribuídos somente a funções.

4. Reinicie o computador.

5. Abra una janela de prompt de comando.

6. Inicie o criador de perfil. Tipo:

    **VSPerfCmd**  [/Start](../profiling/start.md) **: exemplo**  [/output](../profiling/output.md) **:** `OutputFile` [ `Options` ]

   - A opção **/Start: sample** Inicializa o criador de perfil.

   - A opção **/output:** `OutputFile` é necessária com **/Start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).

     É possível usar qualquer uma das opções a seguir com a opção **/start:sample**.

   > [!NOTE]
   > Normalmente, as opções **/user** e **/crosssession** são necessárias para serviços.

   | Opção | Descrição |
   | - | - |
   | [/User](../profiling/user-vsperfcmd.md) **:**[ `Domain` **\\** ]`UserName` | Especifica o domínio e o nome de usuário da conta que possui o processo analisado. Esta opção é necessária apenas se o processo estiver sendo executado como um usuário diferente do usuário conectado. O proprietário do processo é listado na coluna Nome de Usuário na guia Processos do Gerenciador de Tarefas do Windows. |
   | [/CrossSession](../profiling/crosssession.md) | Habilita a criação de perfil de processos em outras sessões. Esta opção é necessária se o serviço estiver em execução em uma sessão diferente. A ID da sessão é listada na coluna ID da Sessão na guia Processos do Gerenciador de Tarefas do Windows. **/CS** pode ser especificado como uma abreviação de **/crosssession**. |
   | [/WinCounter](../profiling/wincounter.md) **:**`WinCounterPath` | Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil. |
   | [/AutoMark](../profiling/automark.md) **:**`Interval` | Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms. |
   | [/Events](../profiling/events-vsperfcmd.md) **:**`Config` | Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Eventos de ETW são coletados em um arquivo separado (.etl). |

7. Se necessário, inicie o serviço.

8. Anexe o criador de perfil ao serviço. Tipo:

    **VSPerfCmd**[/Attach](../profiling/attach.md) **:** { `PID`&#124;`ProcName` } [ `Sample Event` ] [[/TargetCLR](../profiling/targetclr.md)**:** `Version` ]  

   - Especifica a ID do processo (`PID`) ou o nome do processo (ProcName) do serviço. É possível exibir as IDs de processo e nomes de todos os processos em execução no Gerenciador de Tarefas do Windows.

     Por padrão, os dados de desempenho têm amostra obtida a cada 10.000.000 ciclos de relógio de processador não interrompidos. Significa aproximadamente 100 amostras por segundo em um processador 1GH. Você pode especificar uma das opções a seguir para alterar o intervalo de ciclo de relógio ou especificar um evento de amostragem diferente.

   |Evento de Amostra|Descrição|
   |------------------|-----------------|
   |[/timer](../profiling/timer.md) **:**`Interval`|Altera o intervalo de amostragem para o número de ciclos de relógio não interrompidos especificados por `Interval`.|
   |[/PF](../profiling/pf.md)[**:** `Interval` ]|Altera o evento de amostragem para falhas de página. Se `Interval` for especificado, define o número de falhas de página entre as amostras. O padrão é 10.|
   |[/Sys](../profiling/sys-vsperfcmd.md)[ `:``Interval` ]|Altera o evento de amostragem para chamadas do sistema do processo para o kernel do sistema operacional (syscalls). Se `Interval` for especificado, define o número de chamadas entre as amostras. O padrão é 10.|
   |[/Counter](../profiling/counter.md) **:**`Config`|Altera o evento de amostragem e o intervalo para o contador de desempenho do processador e o intervalo especificado em `Config`.|

   - **TargetCLR:** `Version` Especifica a versão do Common Language Runtime (CLR) para o perfil quando mais de uma versão do tempo de execução é carregada em um aplicativo. Opcional.

## <a name="control-data-collection"></a>Controlar a coleta de dados
 Quando o serviço estiver em execução, você pode usar as opções *VSPerfCmd.exe* para iniciar e parar a gravação de dados no arquivo de dados do criador de perfil. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como a inicialização ou o desligamento do aplicativo.

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados

- Os pares de opções **VSPerfCmd** a seguir iniciam e param a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.

    |Opção|Descrição|
    |------------|-----------------|
    |[/GLOBALON/GLOBALOFF](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|
    |[/ProcessOn](../profiling/processon-and-processoff.md) **:** `PID` [/ProcessOff](../profiling/processon-and-processoff.md) **:**`PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pela ID de processo (`PID`).|
    |**/Attach:**{ `PID`&#124;`ProcName` } [/Detach](../profiling/detach.md)[: { `PID`&#124;`ProcName` }]|**/attach** começa a coletar dados para o processo especificado pela ID de processo ou pelo nome de processo. **/detach** interrompe a coleta de dados para o processo especificado ou para todos os processos se nenhum processo específico for especificado.|

## <a name="end-the-profiling-session"></a>Encerrar a sessão de criação de perfil
 Para concluir uma sessão de criação de perfil, o criador de perfil deve ser desanexado de todos os processos analisados e o criador de perfil deve ser desligado explicitamente. É possível desanexá-lo de um aplicativo que foi analisado usando o método de amostragem fechando o aplicativo ou chamando a opção **VSPerfCmd /detach**. Depois, chame a opção **VSPerfCmd /shutdown** para desativar o criador de perfil e fechar o arquivo de dados de criação de perfil.

 O comando **VSPerfClrEnv /globaloff** limpa as variáveis de ambiente de criação de perfil, mas a configuração do sistema não é redefinida até que o computador seja reiniciado.

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil

1. Siga um destes procedimentos para desanexar o criador de perfil do aplicativo de destino:

    - Parar o serviço.

         -ou-

    - Digite **VSPerfCmd/Detach**

2. Desligue o criador de perfil. Tipo:

     **VSPerfCmd /shutdown**

3. (Opcional) desmarcar as variáveis de ambiente de criação de perfil. Tipo:

     **VSPerfClrEnv /globaloff**

4. Reinicie o computador.

## <a name="see-also"></a>Veja também
- [Profile services (Serviços de perfil)](../profiling/command-line-profiling-of-services.md)
- [Exibições de dados do método de amostragem](../profiling/profiler-sampling-method-data-views.md)
