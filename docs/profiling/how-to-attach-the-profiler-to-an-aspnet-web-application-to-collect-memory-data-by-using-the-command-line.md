---
title: Anexar o criador de perfil a um aplicativo ASP.NET para coletar dados de memória
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: d608f85a-41ae-4ca7-85e6-b96624dbc83c
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- aspnet
ms.openlocfilehash: edf9fec93b8fed4e89e5e7cf0525d4f11ed326fa
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85329341"
---
# <a name="how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-memory-data-by-using-the-command-line"></a>Como anexar o criador de perfil a um aplicativo Web ASP.NET para coletar dados da memória usando a linha de comando
Este artigo descreve como usar as ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para anexar o criador de perfil a um aplicativo Web do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] e coletar dados sobre o número e o tamanho das alocações de memória do .NET Framework. Também é possível coletar dados sobre o tempo de vida de objetos de memória do .NET Framework.

> [!NOTE]
> Para obter o caminho para as ferramentas de criação de perfil, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md). Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de Prompt de Comando ou adicioná-lo ao próprio comando.

 Para coletar dados de desempenho de um aplicativo Web [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)], você deve usar a ferramenta [VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) para inicializar as variáveis de ambiente apropriadas no computador que hospeda o aplicativo Web [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)]. Em seguida, você deve reiniciar o computador para configurar o servidor Web para criação de perfil.

 Você deverá, então, usar a ferramenta [VSPerfCmd.exe](../profiling/vsperfcmd.md) para anexar o criador de perfil ao processo de trabalho [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] que hospeda seu site da Web. Quando criador de perfil estiver anexado ao aplicativo, você poderá pausar e retomar a coleta de dados.

 Para concluir uma sessão de criação de perfil, o Criador de perfil não pode mais estar anexado ao aplicativo e o Criador de perfil deve ser desligado explicitamente. Na maioria dos casos, recomendamos desmarcar as variáveis de ambiente de criação de perfil no final de uma sessão.

## <a name="attach-the-profiler"></a>Anexar o criador de perfil

#### <a name="to-attach-the-profiler-to-an-aspnet-web-application"></a>Para anexar o criador de perfil a um aplicativo Web ASP.NET

1. Abra uma janela de Prompt de Comando.

2. Inicialize as variáveis de ambiente de criação de perfil. Tipo:

    **VSPerfClrEnv** {**/globalsamplegc** &#124; **/globalsamplegclife**} [**/samplelineoff**]

   - As opções **/globalsamplegc** e **/globalsamplegclife** especificam o tipo de dados de memória a serem coletados.

        Especifique uma e apenas uma das seguintes opções.

       |Opção|Descrição|
       |------------|-----------------|
       |**/globalsamplegc**|Habilita a coleta de dados de alocação de memória.|
       |**/globalsamplegclife**|Habilita a coleta de dados de alocação de memória e de dados de tempo de vida do objeto.|

   - A opção **/samplelineoff** desabilita a atribuição dos dados coletados para linhas específicas do código-fonte. Se essa opção for especificada, os dados serão atribuídos no nível da função.

3. Reinicie o computador para definir a nova configuração do ambiente.

4. Abra uma janela de Prompt de Comando. Se necessário, defina a variável do ambiente do criador de perfil.

5. Inicie o criador de perfil. Tipo:

    **VSPerfCmd**  [/Start](../profiling/start.md) **: exemplo**  [/output](../profiling/output.md) **:** `OutputFile` [ `Options` ]

   - A opção **/Start: sample** Inicializa o criador de perfil.

   - A opção **/output:** `OutputFile` é necessária com **/Start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).

     É possível usar qualquer uma das opções a seguir com a opção **/start:sample**.

   > [!NOTE]
   > Normalmente, as opções **/user** e **/crosssession** são necessárias para aplicativos ASP.NET.

   | Opção | Descrição |
   | - | - |
   | [/User](../profiling/user-vsperfcmd.md) **:**[ `Domain` **\\** ]`UserName` | Especifica o domínio e o nome de usuário da conta proprietária do processo de trabalho ASP.NET analisado. Esta opção será necessária se o processo estiver sendo executado como um usuário diferente do usuário conectado. O proprietário do processo é listado na coluna Nome de Usuário na guia Processos do Gerenciador de Tarefas do Windows. |
   | [/CrossSession](../profiling/crosssession.md) | Habilita a criação de perfil de processos em outras sessões de logon. Esta opção será necessária se o aplicativo ASP.NET estiver em execução em uma sessão diferente. O identificador da sessão é listado na coluna ID da Sessão na guia Processos do Gerenciador de Tarefas do Windows. **/CS** pode ser especificado como uma abreviação de **/crosssession**. |
   | [/WaitStart](../profiling/waitstart.md) [**:** `Interval` ] | Especifica o número de segundos para aguardar o criador de perfil inicializar antes de retornar um erro. Se `Interval` não for especificado, o criador de perfil aguardará indefinidamente. Por padrão, **/start** retorna imediatamente. |
   | [/WinCounter](../profiling/wincounter.md) **:**`WinCounterPath` | Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil. |
   | [/AutoMark](../profiling/automark.md) **:**`Interval` | Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms. |
   | [/Events](../profiling/events-vsperfcmd.md) **:**`Config` | Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Eventos de ETW são coletados em um arquivo separado (.etl). |

6. Inicie o aplicativo Web [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] normalmente.

7. Anexe o criador de perfil ao processo de trabalho [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)]. Tipo:

    **VSPerfCmd**[/Attach](../profiling/attach.md) **:**{ `PID`&#124;`ProcName` } [[/TargetCLR](../profiling/targetclr.md)**:** `Version` ]  

   - A ID do processo `(PID)` especifica a ID ou o nome do processo de trabalho [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)]. É possível exibir as IDs de processo de todos os processos em execução no Gerenciador de Tarefas do Windows.

   - **/TargetCLR:** `Version` Especifica a versão do Common Language Runtime (CLR) para o perfil quando mais de uma versão do tempo de execução é carregada em um aplicativo.

## <a name="control-data-collection"></a>Controlar a coleta de dados
 Enquanto o aplicativo estiver em execução, você poderá controlar a coleta de dados iniciando e interrompendo a gravação dos dados no arquivo de dados do criador de perfil usando as opções de **VSPerfCmd.exe**. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como a inicialização ou o desligamento do aplicativo.

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados

- Os pares de opções **VSPerfCmd** a seguir iniciam e param a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.

    |Opção|Descrição|
    |------------|-----------------|
    |[/GLOBALON/GLOBALOFF](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|
    |[/ProcessOn](../profiling/processon-and-processoff.md) **:** `PID` [/ProcessOff](../profiling/processon-and-processoff.md) **:**`PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pelo `PID`.|
    |**/Attach:**{ `PID`&#124;`ProcName` } [/Detach](../profiling/detach.md)[**:**{ `PID`&#124;: `ProcName` }]|**/attach** começa a coletar dados para o processo especificado pela ID de processo ou pelo nome de processo. **/detach** interrompe a coleta de dados para o processo especificado ou para todos os processos se nenhum processo específico for especificado.|

## <a name="end-the-profiling-session"></a>Encerrar a sessão de criação de perfil
 Para terminar uma sessão de criação de perfil, o criador de perfil deve ser desanexado do aplicativo Web. É possível interromper a coleta de dados de um aplicativo analisado com o método de amostragem reiniciando o processo de trabalho [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ou invocando a opção **VSPerfCmd /detach**. Chame então a opção **VSPerfCmd** [/shutdown](../profiling/shutdown.md) para desligar o criador de perfil e fechar o arquivo de dados de criação de perfil. O comando **VSPerfClrEnv /globaloff** limpa as variáveis de ambiente de criação de perfil, mas a configuração do sistema não é redefinida até que o computador seja reiniciado.

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil

1. Realize uma das etapas a seguir para desanexar o criador de perfil do aplicativo de destino:

   - Digite **VSPerfCmd** [/detach](../profiling/detach.md)

      -ou-

   - Feche o processo de trabalho [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)]. Tipo:

     **IISReset /stop**

2. Desligue o criador de perfil. Tipo:

    **VSPerfCmd /shutdown**

3. (Opcional) desmarcar as variáveis de ambiente de criação de perfil. Tipo:

    **VSPerfCmd /globaloff**

4. Reinicie o computador. Se necessário, reinicie o ISS (Serviços de Informações da Internet). Tipo:

    **IISReset /start**

## <a name="see-also"></a>Veja também
- [Criar o perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [Exibições de dados de memória do .NET](../profiling/dotnet-memory-data-views.md)
