---
title: Linha de comando do profiler-componente cliente do instrumento do .NET, obter dados da memória
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: d09cc46a-70f5-48f9-aa24-89913e67b359
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: 29406d72fc54e15499a0936a78ebf693f8eca0b3
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85332065"
---
# <a name="how-to-instrument-a-stand-alone-net-framework-component-and-collect-memory-data-with-the-profiler-by-using-the-command-line"></a>Como instrumentar um componente do .NET Framework autônomo e coletar dados de memória com o criador de perfil usando a linha de comando
Este artigo descreve como usar as ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para instrumentar um componente do .NET Framework de um aplicativo autônomo, como um arquivo .exe ou .dll, e coletar informações de memória usando o criador de perfil.

> [!NOTE]
> Para obter o caminho para as ferramentas de criação de perfil, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md). Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de Prompt de Comando ou adicioná-lo ao próprio comando.

 Para coletar dados de memória de um componente do .NET Framework usando o método de instrumentação, você usa a ferramenta [VSInstr.exe](../profiling/vsinstr.md) para gerar uma versão instrumentada do componente e a ferramenta [VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) para inicializar variáveis de ambiente de criação de perfil. Você inicia o criador de perfil usando a ferramenta *VSPerfCmd.exe*.

 Quando o componente instrumentado é executado, os dados de memória são automaticamente coletados para um arquivo de dados. Você pode pausar e retomar a coleta de dados durante a sessão de criação de perfil.

 Para terminar uma sessão de criação de perfil, feche o aplicativo de destino e feche explicitamente o criador de perfil. Na maioria dos casos, recomendamos desmarcar as variáveis de ambiente de criação de perfil no final de uma sessão.

## <a name="start-the-application-with-the-profiler"></a>Iniciar o aplicativo com o criador de perfil

#### <a name="to-attach-the-profiler-to-a-running-net-framework-application"></a>Para anexar o Criador de Perfil a um aplicativo do .NET Framework em execução

1. Abra uma janela de Prompt de Comando.

2. Use a ferramenta **VSInstr** para gerar uma versão instrumentada do aplicativo de destino.

3. Inicialize as variáveis de ambiente de criação de perfil do .NET Framework. Tipo:

    **VSPerfClrEnv** {**/tracegc** &#124; **/tracegclife**}

   - As opções **/tracegc** e **/tracegclife** inicializam as variáveis de ambiente para coletar apenas os dados de alocação de memória ou para coletar os dados de alocação de memória e de tempo de vida do objeto.

       |Opção|Descrição|
       |------------|-----------------|
       |**/tracegc**|Habilita a coleta somente de dados de alocação de memória.|
       |**/tracegclife**|Habilita a coleta de dados de alocação de memória e de tempo de vida do objeto.|

4. Inicie o criador de perfil. Tipo:

    **VSPerfCmd/start: Trace/output:** `OutputFile` [`Options`]

   - A opção [/start](../profiling/start.md)**:trace** inicializa o criador de perfil.

   - A opção [/output](../profiling/output.md)**:** `OutputFile` é necessária com **/Start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.*vsp*).

     É possível usar qualquer uma das opções a seguir com a opção **/start:trace**.

   | Opção | Descrição |
   | - | - |
   | [/User](../profiling/user-vsperfcmd.md) **:**[ `Domain` **\\** ]`UserName` | Especifica o domínio e o nome de usuário da conta que possui o processo analisado. Esta opção será necessária apenas se o processo estiver sendo executado como um usuário diferente do usuário conectado. O proprietário do processo é listado na coluna Nome de Usuário na guia **Processos** do Gerenciador de Tarefas do Windows. |
   | [/CrossSession](../profiling/crosssession.md) | Habilita a criação de perfil de processos em outras sessões. Esta opção será necessária se o aplicativo estiver em execução em uma sessão diferente. A sessão Idenitifer está listada na coluna **ID da sessão** na guia **processos** do Gerenciador de tarefas do Windows. **/CS** pode ser especificado como uma abreviação de **/crosssession**. |
   | [/globaloff](../profiling/globalon-and-globaloff.md) | Para iniciar o criador de perfil com a coleta de dados em pausa, adicione a opção **/globaloff** na linha de comando **/start**. Use **/globalon** para retomar a criação de perfil. |
   | [/WinCounter](../profiling/wincounter.md) **:**`WinCounterPath` | Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil. |
   | [/AutoMark](../profiling/automark.md) **:**`Interval` | Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms. |
   | [/Counter](../profiling/counter.md) **:**`Config` | Coleta informações do contador de desempenho do processador especificado na configuração. As informações do contador são adicionadas aos dados que são coletados em cada evento de criação de perfil. |
   | [eventos](../profiling/events-vsperfcmd.md) **:**`Config` | Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Os eventos ETW são coletados em um separado (.* ETL*). |

5. Inicie o aplicativo de destino na janela do Prompt de Comando.

## <a name="control-data-collection"></a>Controlar a coleta de dados
 Enquanto o aplicativo de destino estiver em execução, você pode controlar a coleta de dados iniciando e parando a gravação de dados no arquivo usando as opções de *VSPerfCmd.exe*. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como a inicialização ou o desligamento do aplicativo.

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados

- Os pares de opções **VSPerfCmd** a seguir iniciam e param a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.

    |Opção|Descrição|
    |------------|-----------------|
    |[/globalon](../profiling/globalon-and-globaloff.md) [/globaloff](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|
    |[/ProcessOn](../profiling/processon-and-processoff.md) **:** `PID` [/ProcessOff](../profiling/processon-and-processoff.md) **:**`PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pela ID de processo (`PID`).|
    |[/ThreadOn](../profiling/threadon-and-threadoff.md) **:** `TID` [/ThreadOff](../profiling/threadon-and-threadoff.md) **:**`TID`|Inicia (**/threadon**) ou interrompe (**/threadoff**) a coleta de dados para o thread especificado pela ID do thread (`TID`).|

## <a name="end-the-profiling-session"></a>Encerrar a sessão de criação de perfil
 Para encerrar uma sessão de criação de perfil, feche o aplicativo que está executando o componente instrumentado e, em seguida, chame a opção **VSPerfCmd** [/shutdown](../profiling/shutdown.md) para desligar o criador de perfil e fechar o arquivo de dados de criação de perfil. O comando **VSPerfClrEnv /off** limpa as variáveis de ambiente da criação de perfil.

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil

1. Feche o aplicativo de destino.

2. Desligue o criador de perfil. Tipo:

     **VSPerfCmd /shutdown**

3. (Opcional) desmarcar as variáveis de ambiente de criação de perfil. Tipo:

     **VSPerfCmd /off**

## <a name="see-also"></a>Veja também
- [Aplicativos Autônomos de Perfil](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [Exibições de dados de memória do .NET](../profiling/dotnet-memory-data-views.md)
