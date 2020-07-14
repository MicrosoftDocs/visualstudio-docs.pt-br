---
title: VSPerfCmd-anexar o criador de perfil ao serviço nativo para obter dados de simultaneidade
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 283a1ee1-b43e-4daf-95ae-1311925a42a8
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- cplusplus
ms.openlocfilehash: 202b7e3f51ff16af15e755ad070813c7c2777744
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85329465"
---
# <a name="how-to-attach-the-profiler-to-a-native-service-to-collect-concurrency-data-by-using-the-command-line"></a>Como anexar o criador de perfil a um serviço nativo para coletar dados de simultaneidade usando a linha de comando
Este artigo descreve como usar as ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para anexar o criador de perfil a um serviço nativo (C/C++) e coletar dados de simultaneidade de thread e do processo usando o método de amostragem.

> [!NOTE]
> Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos UWP também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).

> [!NOTE]
> Para obter o caminho para as ferramentas de criação de perfil, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md). Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de Prompt de Comando ou adicioná-lo ao próprio comando.

 Enquanto o criador de perfil estiver anexado ao serviço, você pode pausar e retomar a coleta de dados. Para encerrar uma sessão de criação de perfil, o criador de perfil não deve mais estar anexado ao serviço e precisa ser desligado explicitamente.

## <a name="attach-the-profiler"></a>Anexar o criador de perfil
 Para anexar o criador de perfil a um serviço nativo, use as opções **VSPerfCmd/start** e **/attach** para inicializar o criador de perfil e anexá-lo ao aplicativo de destino. Você pode especificar **/start** e **/attach** e suas opções respectivas em uma única linha de comando. Você também pode adicionar a opção **/globaloff** para pausar a coleta de dados no início do aplicativo de destino. Depois, você usa **/globalon** para começar a coletar dados.

#### <a name="to-attach-the-profiler-to-a-native-service"></a>Para anexar o criador de perfil a um serviço nativo

1. Se o serviço não estiver em execução, inicie o serviço.

2. Inicie o criador de perfil digitando o seguinte em um prompt de comando:

    [VSPerfCmd](../profiling/vsperfcmd.md) **/Start: Concurrency/output:** `OutputFile` [ `Options` ]

   - A opção [/output](../profiling/output.md)**:** `OutputFile` é necessária com **/Start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).

     É possível usar qualquer opção da tabela a seguir com a opção **/start**.

   > [!NOTE]
   > A maioria dos serviços exigem as opções **/user** e **/crosssession**.

   | Opção | Descrição |
   | - | - |
   | [/User](../profiling/user-vsperfcmd.md) **:**[ `Domain\` ]`UserName` | Especifica o domínio e o nome de usuário opcional da conta que receberá acesso ao criador de perfil. |
   | [/CrossSession](../profiling/crosssession.md) | Habilita a criação de perfil de processos em outras sessões de logon. |
   | [/WinCounter](../profiling/wincounter.md) **:**`WinCounterPath` | Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil. |
   | [/AutoMark](../profiling/automark.md) **:**`Interval` | Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O valor padrão é 500. |
   | [/Events](../profiling/events-vsperfcmd.md) **:**`Config` | Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Eventos de ETW são coletados em um arquivo separado (.etl). |

3. Anexe o criador de perfil ao serviço digitando o seguinte comando em um prompt de comando:

    **VSPerfCmd /attach:** `PID`

    `PID` especifica a ID do processo ou o nome do processo do aplicativo de destino. É possível exibir as IDs de processo de todos os processos em execução no Gerenciador de Tarefas do Windows.

## <a name="control-data-collection"></a>Controlar a coleta de dados
 Enquanto o aplicativo de destino estiver em execução, você poderá controlar a coleta de dados Iniciando e interrompendo a gravação de dados no arquivo com opções de *VSPerfCmd.exe* . Controlando a coleta de dados, é possível coletar dados de uma parte específica da execução do programa, como o início ou o desligamento do aplicativo.

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados

- Os pares de opções na tabela a seguir iniciam e param a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.

    |Opção|Descrição|
    |------------|-----------------|
    |[/GLOBALON/GLOBALOFF](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|
    |[/ProcessOn](../profiling/processon-and-processoff.md) **:** `PID` [/ProcessOff](../profiling/processon-and-processoff.md) **:**`PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo que a ID de processo (`PID`) especificar.|
    |[/Attach](../profiling/attach.md) **:**{ `PID`&#124;`ProcName` } [/Detach](../profiling/detach.md)[**:**{ `PID`&#124;`ProcName` }]|**/attach** começa a coletar dados para o processo que a ID de processo (`PID`) ou o nome de processo (*ProcName*) especificar. **/detach** interrompe a coleta de dados para o processo especificado ou para todos os processos se nenhum processo for especificado.|

## <a name="end-the-profiling-session"></a>Encerrar a sessão de criação de perfil
 Para encerrar uma sessão de criação de perfil, o criador de perfil não pode estar coletando dados. É possível interromper a coleta de dados de um serviço nativo cujo perfil está sendo criado com o método de simultaneidade interrompendo o serviço ou invocando a opção **VSPerfCmd/detach**. Depois, você invoca a opção **VSPerfCmd /shutdown** para desligar o criador de perfil e fechar o arquivo de dados de criação de perfil.

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil

1. Desanexe o criador de perfil do aplicativo de destino parando o serviço ou digitando o seguinte comando no prompt de comando:

     Digite **VSPerfCmd/Detach**

2. Desligue o criador de perfil digitando o seguinte comando em um prompt de comando:

     **VSPerfCmd**  [/Shutdown](../profiling/shutdown.md)
