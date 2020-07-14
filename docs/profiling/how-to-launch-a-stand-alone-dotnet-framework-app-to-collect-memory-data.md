---
title: Linha de comando do profiler-abrir aplicativo .NET Framework cliente, obter dados de memória
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 3bc53041-91b7-4ad0-8413-f8bf2c4b3f5e
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: 6378ea021d089027c19d28e927d5772ef5f35e0f
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85327694"
---
# <a name="how-to-launch-a-stand-alone-net-framework-application-with-the-profiler-to-collect-memory-data-by-using-the-command-line"></a>Como iniciar um aplicativo .NET Framework autônomo com o criador de perfil para coletar dados de memória usando a linha de comando
Este tópico descreve como usar as ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para iniciar um aplicativo autônomo (cliente) do .NET Framework e coletar dados de memória.

 Uma sessão de criação de perfil tem três partes:

- Iniciar o aplicativo usando o criador de perfil.

- Coletar dados de criação de perfil.

- Encerrar a sessão de criação de perfil.

> [!NOTE]
> Para obter o caminho para as ferramentas de criação de perfil, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md). Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de Prompt de Comando ou adicioná-lo ao próprio comando.

## <a name="start-the-application-with-the-profiler"></a>Iniciar o aplicativo com o criador de perfil
 Para iniciar um aplicativo de destino usando o criador de perfil, use as opções **VSPerfCmd.exe/start** e **/launch** para inicializar o criador de perfil e iniciar o aplicativo. Você pode especificar **/start** e **/launch** e suas opções respectivas em uma linha de comando.

 Você também pode adicionar a opções de **/globaloff** para pausar a coleta de dados no início do aplicativo de destino. Depois, você usa **/globalon** para começar a coletar dados.

#### <a name="to-start-an-application-by-using-the-profiler"></a>Para iniciar um aplicativo usando o criador de perfil

1. Abra uma janela de Prompt de Comando.

2. Inicie o criador de perfil. Tipo:

    **VSPerfCmd/start: exemplo/output:** `OutputFile` [`Options`]

   - A opção [/start](../profiling/start.md)**:sample** inicializa o criador de perfil.

   - A opção [/output](../profiling/output.md)**:** `OutputFile` é necessária com **/Start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).

     É possível usar qualquer uma das opções a seguir com a opção **/start:sample**.

   | Opção | Descrição |
   | - | - |
   | [/WinCounter](../profiling/wincounter.md) **:**`WinCounterPath` | Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil. |
   | [/AutoMark](../profiling/automark.md) **:**`Interval` | Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms. |

3. Inicie o aplicativo de destino. Tipo:

    **VSPerfCmd**  [/Launch](../profiling/launch.md) **:** `appName` **/GC:**{**alocação**&#124;**tempo de vida**} [ `Options` ]

   - A opção [/GC](../profiling/gc-vsperfcmd.md)**:** `Keyword` é necessária para coletar dados de memória .NET Framework. O parâmetro de palavra-chave especifica se serão coletados dados de alocação de memória ou se serão coletados dados de alocação de memória e dados de tempo de vida do objeto.

     |Palavra-chave|Descrição|
     |-------------|-----------------|
     |**alocação**|Coleta somente dados de alocação de memória.|
     |**existência**|Coleta de dados de alocação de memória e de tempo de vida do objeto.|

     É possível usar qualquer uma das opções a seguir com a opção **/launch**.

   |Opção|Descrição|
   |------------|-----------------|
   |[/args](../profiling/args.md) **:**`Arguments`|Especifica uma cadeia de caracteres que contém os argumentos de linha de comando a serem passados para o aplicativo de destino.|
   |[/console](../profiling/console.md)|Inicia o aplicativo de destino de linha de comando em uma janela separada.|
   |[/Events](../profiling/events-vsperfcmd.md) **:**`Config`|Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Eventos de ETW são coletados em um arquivo separado (.etl).|
   |[/TargetCLR](../profiling/targetclr.md) **:**`Version`|Especifica a versão do CLR (Common Language Runtime) a ser analisada quando mais de uma versão de tempo de execução for carregada em um aplicativo.|

## <a name="control-data-collection"></a>Controlar a coleta de dados
 Quando o aplicativo de destino estiver em execução, você pode controlar a coleta de dados iniciando e interrompendo a gravação de dados no arquivo usando as opções de *VSPerfCmd.exe*. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como a inicialização ou o desligamento do aplicativo.

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados

- Os pares de opções a seguir iniciam e interrompem a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.

    |Opção|Descrição|
    |------------|-----------------|
    |[/GLOBALON/GLOBALOFF](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|
    |[/ProcessOn](../profiling/processon-and-processoff.md) **:** `PID` [ProcessOff](../profiling/processon-and-processoff.md) **:**`PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pela ID de processo (`PID`).|
    |[/Attach](../profiling/attach.md) **:** `PID` [/Detach](../profiling/detach.md)|**/attach** começa a coletar dados para o processo que é especificado pela `PID` (a ID do processo). **/detach** interrompe a coleta de dados para todos os processos.|

- Também é possível usar a opção **VSPerfCmd.exe**[/mark](../profiling/mark.md) para inserir uma marca de criação de perfil no arquivo de dados. O comando **/mark** adiciona um identificador, um carimbo de data/hora e uma cadeia de caracteres de texto opcional definida pelo usuário. As marcas podem ser usadas para filtrar os dados.

## <a name="end-the-profiling-session"></a>Encerrar a sessão de criação de perfil
 Para concluir uma sessão de criação de perfil, o criador de perfil deve ser desanexado de todos os processos analisados e o criador de perfil deve ser desligado explicitamente. É possível desanexar o criador de perfil de um aplicativo que foi analisado usando o método de amostragem ao fechar o aplicativo ou chamar a opção **VSPerfCmd /detach**. Depois, você chama a opção **VSPerfCmd /shutdown** para desligar o criador de perfil e fechar o arquivo de dados de criação de perfil. O comando **VSPerfClrEnv /off** limpa as variáveis de ambiente da criação de perfil.

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil

1. Realize uma das etapas a seguir para desanexar o criador de perfil do aplicativo de destino:

    - Feche o aplicativo de destino.

         -ou-

    - Digite **VSPerfCmd/Detach**

2. Desligue o criador de perfil. Tipo:

     **VSPerfCmd**  [/Shutdown](../profiling/shutdown.md)

## <a name="see-also"></a>Veja também
- [Aplicativos Autônomos de Perfil](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [Exibições de dados de memória do .NET](../profiling/dotnet-memory-data-views.md)
