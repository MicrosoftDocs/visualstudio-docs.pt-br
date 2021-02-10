---
title: Linha de comando do profiler – serviço .NET do instrumento, detalhes de obter tempo
description: Saiba como usar as ferramentas de linha de comando do Visual Studio Ferramentas de Criação de Perfil para coletar dados de tempo detalhados para um serviço de .NET Framework.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: 9f318fc979d4562c355a9613f67a351452b04ddc
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99942614"
---
# <a name="how-to-instrument-a-net-service-and-collect-detailed-timing-data-by-using-the-profiler-command-line"></a>Como instrumentar um serviço do .NET e coletar dados de tempo detalhados usando a linha de comando do criador de perfil

Este artigo descreve como usar as ferramentas da linha de comando das Ferramentas de Criação de Perfil do Visual Studio para instrumentar um serviço .NET Framework e coletar dados de tempo detalhados.

> [!NOTE]
> Você não pode analisar um serviço com o método de instrumentação se o serviço não puder ser reiniciado após o início do computador, um serviço que inicia somente quando o sistema operacional for iniciado.
>
> Para obter o caminho para as ferramentas de criação de perfil, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md). Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de Prompt de Comando ou adicioná-lo ao próprio comando.
>
> A adição de dados de interação de camada a uma execução de criação de perfil requer procedimentos específicos com ferramentas de criação de perfil de linha de comando. Confira [Coletar dados de interação de camada](../profiling/adding-tier-interaction-data-from-the-command-line.md).

Para coletar dados de tempo detalhados de um serviço .NET Framework usando o método de instrumentação, use a ferramenta [VSInstr.exe](../profiling/vsinstr.md) para gerar uma versão instrumentada do componente. Em seguida, substitua a versão do serviço não instrumentada pela versão instrumentada, certificando-se de que o serviço esteja configurado para iniciar manualmente. Depois, use a ferramenta [VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) para inicializar as variáveis de ambiente de criação de perfil global e reinicie o computador host. Em seguida, inicie o criador de perfil.

Quando o serviço é iniciado, os dados de tempo são automaticamente coletados para um arquivo de dados. Você pode pausar e retomar a coleta de dados durante a sessão de criação de perfil.

Para concluir uma sessão de criação de perfil, desligue o serviço e depois desligue explicitamente o criador de perfil. Na maioria dos casos, recomendamos desmarcar as variáveis de ambiente de criação de perfil no final de uma sessão.

## <a name="start-the-application-with-the-profiler"></a>Iniciar o aplicativo com o criador de perfil

1. Abra una janela de prompt de comando.

2. Use a ferramenta **VSInstr** para gerar uma versão instrumentada do binário.

3. Substitua o binário original pela versão instrumentada. No Gerenciador de Controle de Serviço Windows, certifique-se de que o Tipo de inicialização do serviço esteja definido como Manual.

4. Inicialize as variáveis de ambiente de criação de perfil do .NET Framework. Tipo:

     **VSPerfClrEnv /globaltraceon**

5. Reinicie o computador.

6. Abra una janela de prompt de comando.

7. Inicie o criador de perfil. Tipo:

     **VSPerfCmd/start: Trace/output:** `OutputFile` [`Options`]

   - A opção [/start](../profiling/start.md)**:trace** inicializa o criador de perfil.

   - A opção [/output](../profiling/output.md)**:** `OutputFile` é necessária com **/Start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.*vsp*).

     É possível usar qualquer uma das opções a seguir com a opção **/start:trace**.

     > [!NOTE]
     > Normalmente, as opções **/user** e **/crosssession** são necessárias para serviços de criação de perfil.

     | Opção | Descrição |
     | - | - |
     | [/User](../profiling/user-vsperfcmd.md) **:**[ `Domain` **\\** ]`UserName` | Especifica o domínio e o nome de usuário da conta que possui o processo analisado. Esta opção é necessária apenas se o processo estiver sendo executado como um usuário diferente do usuário conectado. O proprietário do processo é listado na coluna **Nome de Usuário** na guia **Processos** do Gerenciador de Tarefas do Windows. |
     | [/CrossSession](../profiling/crosssession.md) | Habilita a criação de perfil de processos em outras sessões. Esta opção será necessária se o aplicativo estiver em execução em uma sessão diferente. A ID da sessão é listada na coluna **ID da Sessão** na guia **Processos** do Gerenciador de Tarefas do Windows. **/CS** pode ser especificado como uma abreviação de **/crosssession**. |
     | [/WaitStart](../profiling/waitstart.md)[**:** `Interval` ] | Especifica o número de segundos para aguardar o criador de perfil inicializar antes de retornar um erro. Se `Interval` não for especificado, o criador de perfil aguardará indefinidamente. Por padrão, **/start** retorna imediatamente. |
     | [/globaloff](../profiling/globalon-and-globaloff.md) | Para iniciar o criador de perfil com a coleta de dados em pausa, adicione a opção **/globaloff** na linha de comando **/start**. Use **/globalon** para retomar a criação de perfil. |
     | [/Counter](../profiling/counter.md) **:**`Config` | Coleta informações do contador de desempenho do processador especificado em configuração. As informações do contador são adicionadas aos dados coletados em cada evento de criação de perfil. |
     | [/WinCounter](../profiling/wincounter.md) **:**`WinCounterPath` | Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil. |
     | [/AutoMark](../profiling/automark.md) **:**`Interval` | Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms. |
     | [/Events](../profiling/events-vsperfcmd.md) **:**`Config` | Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Os eventos ETW são coletados em um separado (.*ETL*). |

8. Inicie o serviço do Gerenciador de Controle de Serviço Windows.

## <a name="control-data-collection"></a>Controlar a coleta de dados

Quando o serviço estiver em execução, você pode usar as opções *VSPerfCmd.exe* para iniciar e parar a gravação de dados no arquivo de dados do criador de perfil. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como a inicialização ou o desligamento do serviço.

- Os pares de opções **VSPerfCmd** a seguir iniciam e param a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.

    |Opção|Descrição|
    |------------|-----------------|
    |[/GLOBALON/GLOBALOFF](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|
    |[/ProcessOn](../profiling/processon-and-processoff.md) **:** `PID` [/ProcessOff](../profiling/processon-and-processoff.md) **:**`PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pela ID de processo (`PID`).|
    |[/ThreadOn](../profiling/threadon-and-threadoff.md) **:** `TID` [/ThreadOff](../profiling/threadon-and-threadoff.md) **:**`TID`|Inicia (**/threadon**) ou interrompe (**/threadoff**) a coleta de dados para o thread especificado pela ID do thread (`TID`).|

## <a name="end-the-profiling-session"></a>Encerrar a sessão de criação de perfil

Para encerrar uma sessão de criação de perfil, interrompa o serviço que está executando o componente instrumentado e, em seguida, chame a opção **VSPerfCmd** [/shutdown](../profiling/shutdown.md) para desligar o criador de perfil e fechar o arquivo de dados de criação de perfil. O comando **VSPerfClrEnv /globaloff** limpa as variáveis de ambiente da criação de perfil.

Você deve reiniciar o computador para que as novas configurações de ambiente sejam aplicadas.

1. Interrompa o serviço do Gerenciador de Controle de Serviço.

2. Desligue o criador de perfil. Tipo:

     **VSPerfCmd /shutdown**

3. Quando você tiver concluído a criação de todos os perfis, desmarque as variáveis de ambiente de criação de perfil. Tipo:

     **VSPerfClrEnv /globaloff**

4. Substitua o módulo instrumentado pelo original. Se necessário, reconfigure o Tipo de inicialização do serviço.

5. Reinicie o computador.

## <a name="see-also"></a>Confira também

[Serviços](../profiling/command-line-profiling-of-services.md) 
 de perfil [Exibições de dados do método de instrumentação](../profiling/instrumentation-method-data-views.md)
