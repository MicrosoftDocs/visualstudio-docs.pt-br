---
title: Anexar o criador de perfil no aplicativo web ASP.NET para obter estatísticas de aplicativo
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 3725ddbe-ce91-4469-991e-8c5ed048c618
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- aspnet
ms.openlocfilehash: 2944a6b84a7262c44b92584a41b25e8c7a751e17
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85329412"
---
# <a name="how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-application-statistics-by-using-the-command-line"></a>Como anexar o criador de perfil a um aplicativo Web ASP.NET para coletar estatísticas do aplicativo usando a linha de comando
Este artigo descreve como usar as ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para anexar o criador de perfil a um aplicativo Web ASP.NET e coletar estatísticas de desempenho usando o método de amostragem.

> [!NOTE]
> Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos UWP também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).
>
> Adicionar dados de interação de camada a uma execução de criação de perfil requer procedimentos específicos com ferramentas de criação de perfil de linha de comando. Confira [Coletar dados de interação de camada](../profiling/adding-tier-interaction-data-from-the-command-line.md).
>
> Para obter o caminho para as ferramentas de criação de perfil, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md). Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de Prompt de Comando ou adicioná-lo ao próprio comando.

 Para coletar dados de desempenho de um aplicativo Web ASP .NET, as variáveis de ambiente apropriadas devem ser inicializadas e o computador que hospeda o aplicativo Web ASP .NET deve ser reiniciado para configurar o servidor Web para criação de perfil.

 Anexe o criador de perfil ao processo de trabalho do ASP.NET que hospeda seu Web site. Quando criador de perfil estiver anexado ao aplicativo, você poderá pausar e retomar a coleta de dados.

 Para concluir uma sessão de criação de perfil, o criador de perfil deve ser desanexado do aplicativo analisado e desligado explicitamente. Na maioria dos casos, recomendamos desmarcar as variáveis de ambiente de criação de perfil no final de uma sessão.

## <a name="start-the-profiler-and-attach-to-an-aspnet-web-application"></a>Iniciar o criador de perfil e anexá-lo a um aplicativo Web ASP.NET

#### <a name="to-attach-the-profiler-to-an-aspnet-web-application"></a>Para anexar o criador de perfil a um aplicativo Web ASP.NET

1. Abra una janela de prompt de comando.

2. Inicialize as variáveis de ambiente de criação de perfil. Tipo:

    **VSPerfClrEnv /globalsampleon** [**/samplelineoff**]

   - **/globalsampleon** habilita a amostragem.

   - **/samplelineoff** desabilita a atribuição de dados coletados a linhas específicas do código-fonte. Quando essa opção for especificada, os dados serão atribuídos somente a funções.

3. Reinicie o computador.

4. Inicie o criador de perfil. Tipo:**VSPerfCmd** [/Start](../profiling/start.md)**: exemplo** [/output](../profiling/output.md)**:** `OutputFile` [ `Options` ]

   - A opção **/Start: sample** Inicializa o criador de perfil.

   - A opção **/output:** `OutputFile` é necessária com **/Start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).

     É possível usar qualquer uma das opções a seguir com a opção **/start:sample**.

   > [!NOTE]
   > Normalmente, as opções **/user** e **/crosssession** são necessárias para aplicativos ASP.NET.

   | Opção | Descrição |
   | - | - |
   | [/User](../profiling/user-vsperfcmd.md) **:**[ `Domain` **\\** ]`UserName` | Especifica o domínio e o nome de usuário da conta proprietária do processo de trabalho ASP.NET analisado. Esta opção será necessária se o processo estiver sendo executado como um usuário diferente do usuário conectado. O proprietário do processo é listado na coluna **Nome de Usuário** na guia **Processos** do Gerenciador de Tarefas do Windows. |
   | [/CrossSession](../profiling/crosssession.md) | Habilita a criação de perfil de processos em outras sessões de logon. Esta opção será necessária se o aplicativo ASP.NET estiver em execução em uma sessão diferente. O identificador da sessão é listado na coluna ID da Sessão na guia Processos do Gerenciador de Tarefas do Windows. **/CS** pode ser especificado como uma abreviação de **/crosssession**. |
   | [/WinCounter](../profiling/wincounter.md) **:**`WinCounterPath` | Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil. |
   | [/AutoMark](../profiling/automark.md) **:**`Interval` | Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O padrão é 500 ms. |
   | [/Events](../profiling/events-vsperfcmd.md) **:**`Config` | Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Eventos de ETW são coletados em um arquivo separado (.etl). |

5. Inicie o aplicativo Web ASP .NET normalmente.

6. Anexe o criador de perfil ao processo de trabalho do ASP.NET. Tipo:**VSPerfCmd** [/Attach](../profiling/attach.md)**:**{ `PID`&#124;`ProcName` } [ `Sample Event` ] [[/TargetCLR](../profiling/targetclr.md)**:** `Version` ]

   - `PID` especifica a ID de processo do processo de trabalho do ASP.NET; `ProcName` especifica o nome do processo de trabalho. É possível exibir as IDs de processo e nomes de todos os processos em execução no Gerenciador de Tarefas do Windows.

   - Por padrão, os dados de desempenho têm amostra obtida a cada 10.000.000 ciclos de relógio de processador não interrompidos. Significa aproximadamente 100 vezes por segundo em um processador 1GH. Você pode especificar uma das opções **VSPerfCmd** a seguir para alterar o intervalo de ciclo de relógio ou especificar um evento de amostragem diferente.

   |Evento de exemplo|Descrição|
   |------------------|-----------------|
   |[/timer](../profiling/timer.md) **:**`Interval`|Altera o intervalo de amostragem para o número de ciclos de relógio não interrompidos especificados pelo `Interval`.|
   |[/PF](../profiling/pf.md)[**:** `Interval` ]|Altera o evento de amostragem para falhas de página. Se `Interval` for especificado, define o número de falhas de página entre as amostras. O padrão é 10.|
   |[/Sys](../profiling/sys-vsperfcmd.md)[ `:``Interval` ]|Altera o evento de amostragem para chamadas do sistema do processo para o kernel do sistema operacional (syscalls). Se `Interval` for especificado, define o número de chamadas entre as amostras. O padrão é 10.|
   |[/Counter](../profiling/counter.md) **:**`Config`|Altera o evento de amostragem e o intervalo para o contador de desempenho do processador e o intervalo especificado em `Config`.|
   |[/TargetCLR](../profiling/targetclr.md) **:**`Version`|Especifica a versão do CLR (Common Language Runtime) a ser analisada quando mais de uma versão de tempo de execução for carregada em um aplicativo.|

   - **targetclr:** `Version` especifica a versão do CLR analisada quando mais de uma versão do runtime for carregada em um aplicativo. Opcional.

## <a name="control-data-collection"></a>Controlar a coleta de dados
 Quando o aplicativo estiver em execução, você pode controlar a coleta de dados iniciando e parando a gravação de dados no arquivo usando as opções de *VSPerfCmd.exe*. Controlar a coleta de dados permite coletar dados de uma parte específica da execução do programa, como a inicialização ou o desligamento do aplicativo.

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados

- Os pares de opções **VSPerfCmd** a seguir iniciam e param a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.

    |Opção|Descrição|
    |------------|-----------------|
    |[/GLOBALON/GLOBALOFF](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|
    |[/ProcessOn](../profiling/processon-and-processoff.md) **:** `PID` **/ProcessOff:**`PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo especificado pelo `PID`.|
    |[/Attach](../profiling/attach.md) **:**{ `PID`&#124;`ProcName` } [/Detach](../profiling/detach.md)[**:**{ `PID`&#124;`ProcName` }]|**/attach** começa a coletar dados para o processo especificado por `PID` ou pelo nome de processo (ProcName). **/detach** interrompe a coleta de dados para o processo especificado ou para todos os processos se nenhum processo específico for especificado.|

## <a name="end-the-profiling-session"></a>Encerrar a sessão de criação de perfil
 Para encerrar uma sessão de criação de perfil, feche o [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] aplicativo Web e use o comando serviços de informações da Internet (IIS) **iisreset** para fechar o [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] processo de trabalho. Chame a opção **VSPerfCmd** [/shutdown](../profiling/shutdown.md) para desligar o criador de perfil e fechar o arquivo de dados de criação de perfil.

 O comando **VSPerfClrEnv /globaloff** limpa as variáveis de ambiente da criação de perfil. Você deve reiniciar o computador para que as novas configurações de ambiente sejam aplicadas.

 O comando **VSPerfClrEnv /globaloff** limpa as variáveis de ambiente de criação de perfil, mas a configuração do sistema não é redefinida até que o computador seja reiniciado.

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil

1. Siga um destes procedimentos para desanexar o criador de perfil do aplicativo de destino:

   - Digite **VSPerfCmd/Detach**

      -ou-

   - Feche o processo de trabalho [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)].

2. Desligue o criador de perfil. Digite:**VSPerfCmd** [/shutdown](../profiling/shutdown.md)

3. (Opcional) desmarcar as variáveis de ambiente de criação de perfil. Tipo:

    **VSPerfCmd /globaloff**

4. Reinicie o computador.

## <a name="see-also"></a>Veja também
- [Criar o perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [Exibições de dados do método de amostragem](../profiling/profiler-sampling-method-data-views.md)
