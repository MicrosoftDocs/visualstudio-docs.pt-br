---
title: 'Linha de comando do criador de perfil: Instrumentar o serviço .NET, obter dados de memória'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 2fa072fc-05fe-4420-99c0-51d2ea3ac4ce
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 2b4e74b6f4e26b3ed797e8df3cbe3f6e33d74d06
ms.sourcegitcommit: 91c7f1b525e0c22d938bc4080ba4ceac2483474f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2019
ms.locfileid: "67032045"
---
# <a name="how-to-instrument-a-net-framework-service-and-collect-memory-data-by-using-the-profiler-command-line"></a>Como: Instrumentar um serviço do .NET Framework e coletar memória de dados usando a linha de comando do criador de perfil
Este artigo descreve como usar as ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para instrumentar um serviço .NET Framework e coletar dados de uso de memória. É possível coletar dados de alocação de memória ou coletar dados de alocação de memória e dados de tempo de vida do objeto.

> [!NOTE]
> Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos UWP também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).
>
> [!NOTE]
> Você não poderá criar o perfil de um serviço com o método de instrumentação se o serviço não puder ser reiniciado após o início do computador, um serviço que inicia quando o sistema operacional for iniciado.
>
> Para obter o caminho para as ferramentas de criação de perfil, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md). Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de Prompt de Comando ou adicioná-lo ao próprio comando.

## <a name="start-the-profiling-session"></a>Iniciar a sessão de criação de perfil
 Para coletar dados de desempenho de um serviço .NET Framework, use a ferramenta [VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) para inicializar as variáveis de ambiente adequadas e a ferramenta [VSInstr.exe](../profiling/vsinstr.md) para criar uma cópia instrumentada do arquivo binário do serviço.

 O computador que hospeda o serviço deve ser reiniciado para configurá-lo para a criação de perfil. Você também deve iniciar o serviço manualmente do Gerenciador de Controle de Serviço. Em seguida, inicie o criador de perfil e inicie o serviço .NET Framework.

 Quando o componente instrumentado é executado, os dados de memória são automaticamente coletados para um arquivo de dados. Você pode pausar e retomar a coleta de dados durante a sessão de criação de perfil.

 Para terminar uma sessão de criação de perfil, feche o serviço e feche explicitamente o criador de perfil. Na maioria dos casos, recomendamos desmarcar as variáveis de ambiente de criação de perfil no final de uma sessão.

#### <a name="to-begin-profiling-a-net-framework-service"></a>Para iniciar a criação de perfil de um serviço do .NET Framework

1. Abra uma janela do prompt de comando.

2. Use a ferramenta **VSInstr** para gerar uma versão instrumentada do binário.

3. Use o Gerenciador de Controle de Serviço para substituir o binário original pela versão instrumentada. Certifique-se de que o Tipo de inicialização do serviço esteja definido como Manual.

4. Inicialize as variáveis de ambiente de criação de perfil. Tipo:

    **VSPerfClrEnv** { **/globaltracegc** &#124; **/globaltracegclife**}

   - **/globaltracegclife** e **/globaltracegclife** habilita a coleta de dados de alocação de memória e dados de tempo de vida do objeto.

       |Opção|DESCRIÇÃO|
       |------------|-----------------|
       |**/globaltracegc**|Coleta somente dados de alocação de memória.|
       |**/globaltracegclife**|Coleta dados de alocação de memória e de tempo de vida do objeto.|

5. Reinicie o computador.

6. Abra uma janela do prompt de comando.

7. Inicie o criador de perfil. Tipo:

    **VSPerfCmd**  [/start](../profiling/start.md) **:trace**  [/output](../profiling/output.md) **:** `OutputFile` [`Options`]

   - A opção **/start: contention** inicializa o criador de perfil.

   - A opção **/output:** `OutputFile` é necessária com **/start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).

     É possível usar qualquer uma das opções a seguir com a opção **/start:sample**.

   > [!NOTE]
   > Normalmente, as opções **/user** e **/crosssession** são necessárias para serviços.

   | Opção | DESCRIÇÃO |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:** [`Domain` **\\** ]`UserName` | Especifica o domínio e o nome de usuário da conta proprietária do processo de trabalho ASP.NET analisado. Esta opção será necessária se o processo estiver sendo executado como um usuário diferente do usuário conectado. O proprietário do processo é listado na coluna Nome de Usuário na guia Processos do Gerenciador de Tarefas do Windows. |
   | [/crosssession](../profiling/crosssession.md) | Habilita a criação de perfil de processos em outras sessões de logon. Esta opção será necessária se o aplicativo ASP.NET estiver em execução em uma sessão diferente. A ID da sessão é listada na coluna **ID da Sessão** na guia **Processos** do Gerenciador de Tarefas do Windows. **/CS** pode ser especificado como uma abreviação de **/crosssession**. |
   | [/waitstart](../profiling/waitstart.md)[ **:** `Interval`] | Especifica o número de segundos para aguardar o criador de perfil inicializar antes de retornar um erro. Se `Interval` não for especificado, o criador de perfil aguardará indefinidamente. Por padrão, **/start** retorna imediatamente. |
   | [/globaloff](../profiling/globalon-and-globaloff.md) | Para iniciar o criador de perfil com a coleta de dados em pausa, adicione a opção **/globaloff** na linha de comando **/start**. Use **/globalon** para retomar a criação de perfil. |
   | [/counter](../profiling/counter.md) **:** `Config` | Coleta informações do contador de desempenho do processador especificado em Config. As informações do contador são adicionadas aos dados coletados em cada evento de criação de perfil. |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil. |
   | [/automark](../profiling/automark.md) **:** `Interval` | Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms. |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Os eventos do ETW são coletados em um arquivo separado (.*etl*). |

8. Se necessário, inicie o serviço.

9. Anexe o criador de perfil ao serviço. Tipo:

     **VSPerfCmd /attach:** `PID`&#124;`ProcessName`

    - Especifique a ID do processo ou o nome do processo do serviço. É possível exibir as IDs de processo e nomes de todos os processos em execução no Gerenciador de Tarefas do Windows.

## <a name="control-data-collection"></a>Controlar a coleta de dados
 Enquanto o serviço estiver em execução, você pode controlar a coleta de dados iniciando e parando a gravação de dados no arquivo usando as opções de *VSPerfCmd.exe*. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como a inicialização ou o desligamento do aplicativo.

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados

- Os pares de opções **VSPerfCmd** a seguir iniciam e interrompem a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.

    |Opção|DESCRIÇÃO|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|Inicia ( **/globalon**) ou interrompe ( **/globaloff**) a coleta de dados para todos os processos.|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|Inicia ( **/processon**) ou interrompe ( **/processoff**) a coleta de dados para o processo especificado pela ID de processo (`PID`).|
    |[/threadon](../profiling/threadon-and-threadoff.md) **:** `TID` [/threadoff](../profiling/threadon-and-threadoff.md) **:** `TID`|Inicia ( **/threadon**) ou interrompe ( **/threadoff**) a coleta de dados para o thread especificado pela ID do thread (`TID`).|

## <a name="end-the-profiling-session"></a>Encerrar a sessão de criação de perfil
 Para encerrar uma sessão de criação de perfil, feche o aplicativo que está executando o componente instrumentado e, em seguida, inicie a opção **VSPerfCmd** [/shutdown](../profiling/shutdown.md) para desligar o criador de perfil e fechar o arquivo de dados de criação de perfil. O comando **VSPerfClrEnv /globaloff** limpa as variáveis de ambiente da criação de perfil.

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil

1. Interrompa o serviço do Gerenciador de Controle de Serviço.

2. Desligue o criador de perfil. Tipo:

     **VSPerfCmd /shutdown**

3. Quando você tiver concluído a criação de todos os perfis, desmarque as variáveis de ambiente de criação de perfil. Tipo:

     **VSPerfClrEnv /globaloff**

     Substitua o módulo instrumentado pelo original. Se necessário, reconfigure o Tipo de inicialização do serviço.

4. Reinicie o computador.

## <a name="see-also"></a>Consulte também
- [Profile services (Serviços de perfil)](../profiling/command-line-profiling-of-services.md)
- [Exibições de dados da memória do .NET](../profiling/dotnet-memory-data-views.md)