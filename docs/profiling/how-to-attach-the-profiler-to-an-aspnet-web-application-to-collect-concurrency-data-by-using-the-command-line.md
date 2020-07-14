---
title: Anexar o criador de perfil ao aplicativo ASP.NET para coletar dados de simultaneidade
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 0e215fdd-55f8-43ef-9534-06542eefe223
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- aspnet
ms.openlocfilehash: d7e9f2e7fe68dc7bc9d7ceec9e677ab98d4ee1d2
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85329359"
---
# <a name="how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-concurrency-data-by-using-the-command-line"></a>Como anexar o criador de perfil a um aplicativo Web ASP.NET para coletar dados de simultaneidade usando a linha de comando
Este artigo descreve como usar as ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para anexar o criador de perfil a um aplicativo ASP.NET e coletar dados de simultaneidade de thread e do processo.

Para obter o caminho para as ferramentas de criação de perfil, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md). Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de Prompt de Comando ou adicioná-lo ao próprio comando.

 Para coletar dados de simultaneidade, anexe o criador de perfil ao processo de trabalho do ASP.NET que hospeda o site. Enquanto o criador de perfil estiver anexado ao aplicativo, você pode pausar e retomar a coleta de dados. Para encerrar uma sessão de criação de perfil, o criador de perfil não deve mais estar anexado ao aplicativo e precisa ser desligado explicitamente. Na maioria dos casos, você precisa desmarcar as variáveis de ambiente de criação de perfil no final de uma sessão.

## <a name="attach-the-profiler"></a>Anexar o criador de perfil

#### <a name="to-attach-the-profiler-to-a-aspnet-application"></a>Para anexar o criador de perfil a um aplicativo ASP.NET

1. Inicie o criador de perfil digitando o seguinte comando:

    [VSPerfCmd](../profiling/vsperfcmd.md) **/Start: Concurrency/output:** `OutputFile` [ `Options` ]

   - A opção [/start](../profiling/start.md) inicializa o criador de perfil para coletar dados de contenção de recursos.

   - A opção [/output](../profiling/output.md)**:** `OutputFile` é necessária com **/Start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).

     É possível usar qualquer opção da tabela a seguir com a opção **/start**.

   | Opção | Descrição |
   | - | - |
   | [/User](../profiling/user-vsperfcmd.md) **:**[ `Domain\` ]`UserName` | Especifica o domínio e o nome de usuário opcional da conta que receberá acesso ao criador de perfil. |
   | [/CrossSession](../profiling/crosssession.md) | Habilita a criação de perfil de processos em outras sessões de logon. |
   | [/WinCounter](../profiling/wincounter.md) **:**`WinCounterPath` | Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil. |
   | [/AutoMark](../profiling/automark.md) **:**`Interval` | Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O valor padrão é 500. |
   | [/Events](../profiling/events-vsperfcmd.md) **:**`Config` | Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Os eventos ETW são coletados em um separado (.* ETL*). |

2. Inicie o aplicativo ASP.NET de maneira normal.

3. Anexe o criador de perfil ao processo de trabalho do ASP.net digitando o seguinte comando:**VSPerfCmd/Attach:** `PID` [**/TargetCLR:** `Version` ]

   - `PID` especifica a ID ou o nome do processo de trabalho do ASP.NET. É possível exibir as IDs de processo de todos os processos em execução no Gerenciador de Tarefas do Windows.

   - [/TargetCLR](../profiling/targetclr.md) **:** `Version` especifica a versão do Common Language Runtime (CLR) para o perfil quando mais de uma versão do tempo de execução é carregada em um aplicativo. Esse parâmetro é opcional.

## <a name="control-data-collection"></a>Controlar a coleta de dados
 Enquanto o aplicativo está em execução, você pode controlar a coleta de dados Iniciando e interrompendo a gravação de dados no arquivo usando opções de *VSPerfCmd.exe* . Controlando a coleta de dados, é possível coletar dados de uma parte específica da execução do programa, como o início ou o desligamento do aplicativo.

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados

- Os pares de opções VSPerfCmd na tabela a seguir iniciam e interrompem a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.

    |Opção|Descrição|
    |------------|-----------------|
    |[/GLOBALON/GLOBALOFF](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|
    |[/ProcessOn](../profiling/processon-and-processoff.md) **:** `PID` [ProcessOff](../profiling/processon-and-processoff.md) **:**  `PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo que a ID de processo (`PID`) especificar.|
    |[/Attach](../profiling/attach.md) **:**{ `PID`&#124;`ProcName` } [/Detach](../profiling/detach.md)[**:**{ `PID`&#124;`ProcName` }]|**/attach** começa a coletar dados para o processo que a ID de processo (`PID`) ou o nome de processo (*ProcName*) especificar. **/detach** interrompe a coleta de dados para o processo especificado ou para todos os processos se nenhum processo for especificado.|

## <a name="end-the-profiling-session"></a>Encerrar a sessão de criação de perfil
 Para encerrar uma sessão de criação de perfil, o criador de perfil não pode estar coletando dados. É possível interromper a coleta de dados de um aplicativo cujo perfil foi criado com o método de simultaneidade reiniciando o processo de trabalho do ASP.NET ou invocando a opção **VSPerfCmd/detach**. Depois, você invoca a opção **VSPerfCmd /shutdown** para desligar o criador de perfil e fechar o arquivo de dados de criação de perfil. O comando **VSPerfClrEnv /globaloff** limpa as variáveis de ambiente de criação de perfil, mas a configuração do sistema não é redefinida até que o computador seja reiniciado.

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil

1. Desanexe o criador de perfil do aplicativo de destino fechando-o ou digitando o seguinte no prompt de comando:

     **VSPerfCmd /detach**

2. Desligue o criador de perfil digitando o seguinte comando em um prompt de comando:

     **VSPerfCmd**  [/Shutdown](../profiling/shutdown.md)

## <a name="see-also"></a>Veja também
- [Criar o perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [Criação rápida de perfil de site com VSPerfASPNETCmd](../profiling/rapid-web-site-profiling-with-vsperfaspnetcmd.md)
