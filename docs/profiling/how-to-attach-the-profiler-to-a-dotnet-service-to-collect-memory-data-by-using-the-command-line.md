---
title: Anexar o criador de perfil a um serviço do .NET para coletar dados de memória
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: aeac39af-ad99-479f-aa36-4104356ca512
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: 6552ca62be6de2e99b4e650daaa117e4025746cf
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85328681"
---
# <a name="how-to-attach-the-profiler-to-a-net-service-to-collect-memory-data-by-using-the-command-line"></a>Como anexar o criador de perfil a um serviço do .NET para coletar dados da memória usando a linha de comando
Este artigo descreve como usar as ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para anexar o criador de perfil a um serviço .NET Framework e coletar dados de memória. É possível coletar dados sobre o número e tamanho das alocações de memória, bem como sobre o tempo de vida de objetos de memória.

> [!NOTE]
> Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos UWP também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).
>
> [!NOTE]
> Para obter o caminho para as ferramentas de criação de perfil, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md). Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de Prompt de Comando ou adicioná-lo ao próprio comando.

 Para coletar dados de memória de um serviço .NET Framework, use a ferramenta [VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) para inicializar as variáveis de ambiente apropriadas no computador que hospeda o serviço. O computador deve ser reiniciado para configurá-lo para a criação de perfil.

 Você usar a ferramenta [VSPerfCmd](../profiling/vsperfcmd.md) para anexar o criador de perfil ao processo do serviço. Enquanto o criador de perfil estiver anexado ao serviço, você pode pausar e retomar a coleta de dados.

 Para concluir uma sessão de criador de perfil, o criador de perfil deve ser desanexado do serviço e desligado explicitamente. Na maioria dos casos, recomendamos desmarcar as variáveis de ambiente de criação de perfil no final de uma sessão.

## <a name="attach-the-profiler"></a>Anexar o criador de perfil

#### <a name="to-attach-the-profiler-to-a-net-framework-service"></a>Para anexar o criador de perfil a um serviço do .NET Framework

1. Se necessário, instale o serviço.

2. Abra una janela de prompt de comando.

3. Inicialize as variáveis de ambiente de criação de perfil. Tipo:

    **VSPerfClrEnv** {**/globalsamplegc /globalsamplegclife**}[**/samplelineoff**]

   - As opções **/globalsamplegclife** e **/globalsamplegclife** especificam o tipo de dados de memória a serem coletados. Especifique uma e apenas uma das seguintes opções.

     **/globalsamplegc** Habilita a coleta de dados de alocação de memória.

     **/globalsamplegclife** Habilita a coleta de dados de alocação de memória e de dados de tempo de vida do objeto.

   - A opção **/samplelineoff** desabilita a coleta de dados do número de linha do código-fonte.

4. Reinicie o computador para definir a nova configuração do ambiente.

5. Se necessário, inicie o serviço.

6. Abra una janela de prompt de comando. Se necessário, adicione o caminho do criador de perfil à variável de ambiente PATH.

7. Inicie o criador de perfil. Tipo:

    **VSPerfCmd**  [/Start](../profiling/start.md) **: exemplo**  [/output](../profiling/output.md) **:** `OutputFile` [ `Options` ]

   - A opção **/Start: sample** Inicializa o criador de perfil.

   - A opção **/output:** `OutputFile` é necessária com **/Start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).

     É possível usar uma ou várias opções a seguir com a opção **/start:sample**.

   > [!NOTE]
   > Normalmente, as opções **/user** e **/crosssession** são necessárias para serviços.

   | Opção | Descrição |
   | - | - |
   | [/User](../profiling/user-vsperfcmd.md) **:**[ `Domain` **\\** ]`UserName` | Especifica o domínio e o nome de usuário da conta que possui o processo. Esta opção será necessária se o processo estiver sendo executado como um usuário diferente do usuário conectado. O proprietário do processo é listado na coluna Nome de Usuário na guia Processos do Gerenciador de Tarefas do Windows. |
   | [/CrossSession](../profiling/crosssession.md) | Habilita a criação de perfil de processos em outras sessões de logon. Esta opção será necessária se o aplicativo ASP.NET estiver em execução em uma sessão diferente. A ID da sessão é listada na coluna ID da Sessão na guia Processos do Gerenciador de Tarefas do Windows. **/CS** pode ser especificado como uma abreviação de **/crosssession**. |
   | [/User](../profiling/user-vsperfcmd.md) **:**[ `Domain` **\\** ]`UserName` | Especifica o domínio e o nome de usuário opcionais da conta de logon na qual o serviço é executado. A conta de logon é listada na coluna Fazer logon como do serviço no Gerenciador de Controle de Serviço Windows. |
   | [/CrossSession&#124;cs](../profiling/crosssession.md) | Habilita a criação de perfil de processos em outras sessões de logon. |
   | [/WinCounter](../profiling/wincounter.md) **:**`WinCounterPath` | Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil. |
   | [/AutoMark](../profiling/automark.md) **:**`Interval` | Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms. |
   | [/Events](../profiling/events-vsperfcmd.md) **:**`Config` | Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Eventos de ETW são coletados em um arquivo separado (.etl). |

8. Anexe o criador de perfil ao serviço. Tipo:

    **VSPerfCmd**[/Attach](../profiling/attach.md) **:**{ `PID`&#124;`ProcName` } [[/TargetCLR](../profiling/targetclr.md)**:** `Version` ]  

   - Especifica a ID ou o nome do processo do serviço. É possível exibir as IDs de processo e nomes de todos os processos em execução no Gerenciador de Tarefas do Windows.

   - **TargetCLR:** `Version` Especifica a versão do Common Language Runtime (CLR) para o perfil quando mais de uma versão do tempo de execução é carregada em um aplicativo. Opcional.

## <a name="control-data-collection"></a>Controlar a coleta de dados
 Enquanto o serviço estiver em execução, você pode usar as opções *VSPerfCmd.exe* para interromper e iniciar a gravação de dados no arquivo de dados do criador de perfil. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como a inicialização ou o desligamento do aplicativo.

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados

- Os pares de opções **VSPerfCmd** a seguir iniciam e param a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.

    |Opção|Descrição|
    |------------|-----------------|
    |[/GLOBALON/GLOBALOFF](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|
    |[/ProcessOn](../profiling/processon-and-processoff.md) **:** `PID` [/ProcessOff](../profiling/processon-and-processoff.md) **:**`PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pela ID de processo (`PID`).|
    |**/Attach:**{ `PID`&#124;`ProcName` } [/Detach](../profiling/detach.md)[: { `PID`&#124;`ProcName` }]|**/attach** começa a coletar dados para o processo especificado pela ID de processo ou pelo nome de processo. **/Detach** interrompe a coleta de dados para o processo especificado ou para todos os processos se um processo específico não for especificado.|

## <a name="end-the-profiling-session"></a>Encerrar a sessão de criação de perfil
 Para encerrar uma sessão de criação de perfil, o criador de perfil não pode estar coletando dados. É possível interromper a coleta de dados de um aplicativo analisado com o método de amostragem interrompendo o serviço ou chamando a opção **VSPerfCmd /detach**. Em seguida, chame a opção **VSPerfCmd** [/shutdown](../profiling/shutdown.md) para desativar o criador de perfil e fechar o arquivo de dados de criação de perfil. O comando **VSPerfClrEnv /globaloff** limpa as variáveis de ambiente de criação de perfil, mas a configuração do sistema não é redefinida até que o computador seja reiniciado.

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
- [Exibições de dados de memória do .NET](../profiling/dotnet-memory-data-views.md)
