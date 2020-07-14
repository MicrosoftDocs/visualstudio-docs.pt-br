---
title: Anexar criador de perfil ao serviço .NET para coletar dados de simultaneidade
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: ffbdfe37-8325-44be-bd36-2c8aab2dec7b
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: 24c49015915b8a1d214a833c38c5550f51c50c13
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85328695"
---
# <a name="how-to-attach-the-profiler-to-a-net-service-to-collect-concurrency-data-by-using-the-command-line"></a>Como anexar o criador de perfil a um serviço do .NET para coletar dados de simultaneidade usando a linha de comando
Este artigo descreve como usar as ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para anexar o criador de perfil a um serviço .NET Framework e coletar dados de simultaneidade de thread e do processo usando o método de amostragem.

> [!NOTE]
> Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos UWP também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).

> [!NOTE]
> Para obter o caminho para as ferramentas de criação de perfil, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md). Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de Prompt de Comando ou adicioná-lo ao próprio comando.

 Para coletar dados de simultaneidade, anexe o criador de perfil ao processo do serviço. Enquanto o criador de perfil estiver anexado ao serviço, você pode pausar e retomar a coleta de dados. Para encerrar uma sessão de criação de perfil, o criador de perfil não deve mais estar anexado ao serviço e precisa ser desligado explicitamente. Na maioria dos casos, recomendamos desmarcar as variáveis de ambiente de criação de perfil no final de uma sessão.

## <a name="attach-the-profiler"></a>Anexar o criador de perfil

#### <a name="to-attach-the-profiler-to-a-net-framework-service"></a>Para anexar o criador de perfil a um serviço do .NET Framework

1. Instale o serviço.

2. Abra uma janela de comando.

3. Inicialize as variáveis de ambiente de criação de perfil. Tipo:

     [VSPerfClrEnv](../profiling/vsperfclrenv.md) **/globalsampleon** [**/samplelineoff**]

    - **/globalsampleon** habilita a amostragem.

    - **/samplelineoff** desabilita a atribuição de dados coletados a linhas específicas do código-fonte. Quando essa opção for especificada, os dados serão atribuídos somente a funções.

4. Reinicie o computador.

5. Inicie o criador de perfil. Tipo:

     [VSPerfCmd](../profiling/vsperfcmd.md) **/Start: Concurrency/output:** `OutputFile` [ `Options` ]

     A opção [/output](../profiling/output.md)**:** `OutputFile` é necessária com **/Start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).

     É possível usar qualquer uma das opções a seguir com a opção **/start**.

    > [!NOTE]
    > Normalmente, as opções **/user** e **/crosssession** são necessárias para serviços.

    |Opção|Descrição|
    |------------|-----------------|
    |[/User](../profiling/user-vsperfcmd.md) **:**[ `Domain` **\\** ]`UserName`|Especifica o domínio e o nome de usuário da conta que possui o processo analisado. Esta opção é necessária apenas se o processo estiver sendo executado como um usuário diferente do usuário conectado. O proprietário do processo é listado na coluna **Nome de Usuário** na guia **Processos** do Gerenciador de Tarefas do Windows.|
    |[/CrossSession](../profiling/crosssession.md)|Habilita a criação de perfil de processos em outras sessões. Esta opção é necessária se o serviço estiver em execução em uma sessão diferente. A ID da sessão é listada na coluna **ID da Sessão** na guia **Processos** do Gerenciador de Tarefas do Windows. **/CS** pode ser especificado como uma abreviação de **/crosssession**.|
    |[/WinCounter](../profiling/wincounter.md) **:**`WinCounterPath`|Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil.|
    |[/AutoMark](../profiling/automark.md) **:**`Interval`|Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms.|
    |[/Events](../profiling/events-vsperfcmd.md) **:**`Config`|Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Os eventos ETW são coletados em um separado (.* ETL*).|

6. Se necessário, inicie o serviço.

7. Anexe o criador de perfil ao serviço. Tipo:

     **/Attach VSPerfCmd:** `PID` [[/TargetCLR](../profiling/targetclr.md)**:** `Version` ]

    - `PID` especifica a ID do processo ou o nome do processo do serviço. É possível exibir as IDs de processo de todos os processos em execução no Gerenciador de Tarefas do Windows.

    - **TargetCLR:** `Version` Especifica a versão do Common Language Runtime (CLR) para o perfil quando mais de uma versão do tempo de execução é carregada em um aplicativo. Opcional.

## <a name="control-data-collection"></a>Controlar a coleta de dados
 Enquanto o serviço está em execução, você pode controlar a coleta de dados Iniciando e interrompendo a gravação de dados no arquivo usando opções de *VSPerfCmd.exe* . Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como o início ou o desligamento do aplicativo.

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados

- Os pares de opções **VSPerfCmd** a seguir iniciam e param a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.

    |Opção|Descrição|
    |------------|-----------------|
    |[/GLOBALON/GLOBALOFF](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|
    |[/ProcessOn](../profiling/processon-and-processoff.md) **:** `PID` [/ProcessOff](../profiling/processon-and-processoff.md) **:**`PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pela ID de processo (`PID`).|
    |**/Attach:**{ `PID`&#124;`ProcName` } [/Detach](../profiling/detach.md)[: { `PID`&#124;`ProcName` }]|**/attach** começa a coletar dados para o processo especificado pela ID de processo ou pelo nome de processo. **/detach** interrompe a coleta de dados para o processo especificado ou para todos os processos se nenhum processo específico for especificado.|

- Também é possível usar a opção **VSPerfCmd.exe**[/mark](../profiling/mark.md) para inserir uma marca de criação de perfil no arquivo de dados. O comando **/mark** adiciona um identificador, um carimbo de data/hora e uma cadeia de caracteres de texto opcional definida pelo usuário. As marcas podem ser usadas para filtrar dados em exibições de dados e relatórios do criador de perfil. Os pares de opções VSPerfCmd a seguir iniciam e interrompem a coleta de dados. Especifica cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.

## <a name="end-the-profiling-session"></a>Encerrar a sessão de criação de perfil
 Para encerrar uma sessão de criação de perfil, o criador de perfil não pode estar coletando dados. É possível interromper a coleta de dados de um aplicativo cujo perfil foi criado com o método de simultaneidade interrompendo o serviço ou invocando a opção **VSPerfCmd /detach**. Depois, invoque a opção **VSPerfCmd /shutdown** para desativar o criador de perfil e fechar o arquivo de dados de criação de perfil. O comando **VSPerfClrEnv /globaloff** limpa as variáveis de ambiente de criação de perfil, mas a configuração do sistema não é redefinida até que o computador seja reiniciado.

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil

1. Siga um destes procedimentos para desanexar o criador de perfil do aplicativo de destino.

    - Parar o serviço.

         -ou-

    - Digite **VSPerfCmd /detach.**

2. Desligue o criador de perfil. Tipo:

     **VSPerfCmd**  [Shutdown](../profiling/shutdown.md)
