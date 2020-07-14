---
title: Medir o uso da CPU em seus aplicativos
description: Analise problemas de desempenho da CPU em seu aplicativo usando as ferramentas de diagnóstico integradas ao depurador.
ms.custom: seodec18
ms.date: 04/03/2019
ms.topic: tutorial
f1_keywords:
- vs.performance.wizard.intropage
helpviewer_keywords:
- Profiling Tools, quick start
- Diagnostics Tools, CPU Usage
- CPU Usage
- Diagnostics Tools
ms.assetid: da2fbf8a-2d41-4654-a509-dd238532d25a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d3a7c5eb8aa489da9ced0803e0f83855734825ff
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537365"
---
# <a name="measure-application-performance-by-analyzing-cpu-usage"></a>Medir o desempenho do aplicativo analisando o uso da CPU

Você pode usar as ferramentas de criação de perfil do Visual Studio para analisar problemas de desempenho em seu aplicativo. Este artigo mostra como usar a guia **uso da CPU** das ferramentas de diagnóstico para obter dados de desempenho para seu aplicativo.

Quando o depurador pausa, a ferramenta **Uso de CPU** coleta informações sobre as funções que estão em execução no aplicativo. A ferramenta lista as funções que estavam executando o trabalho e fornece um gráfico de linha do tempo que você pode usar para se concentrar em segmentos específicos da sessão de amostragem.

O Hub de diagnósticos oferece várias outras opções para executar e gerenciar sua sessão de diagnóstico. Se **Uso de CPU** não fornecer os dados que você precisa, as [outras ferramentas de criação de perfil](../profiling/profiling-feature-tour.md) fornecem diferentes tipos de informações que poderão ser úteis. Em muitos casos, o gargalo de desempenho do aplicativo pode ser causado por algo que não seja a CPU, como memória, interface do usuário de renderização ou tempo de solicitação de rede. O Hub de diagnósticos oferece várias outras opções para registrar e analisar esse tipo de dados.

> [!Important]
> As Ferramentas de Diagnóstico têm suporte para desenvolvimento de .NET no Visual Studio, incluindo o ASP.NET e para desenvolvimento nativo/C++.

Neste artigo, abordaremos a análise do uso de CPU no fluxo de trabalho de depuração normal. Você também pode analisar o uso da CPU sem um depurador anexado ou direcionando a um aplicativo em execução. Para obter mais informações, consulte [executar ferramentas de criação de perfil com ou sem o depurador](../profiling/running-profiling-tools-with-or-without-the-debugger.md). Você também pode usar outra ferramenta de criação de perfil, [PerfTips](../profiling/perftips.md), para percorrer o código e identificar quanto tempo as funções específicas ou os blocos de código são concluídos.

Você pode usar as ferramentas de criação de perfil sem o depurador com o Windows 7 e posteriores. O Windows 8 ou posterior é necessário para executar ferramentas de criação de perfil com o depurador (janela **Ferramentas de Diagnóstico**).

Neste tutorial, você irá:

> [!div class="checklist"]
> * Coletar dados de uso da CPU
> * Analisar os dados de uso da CPU

## <a name="step-1-collect-profiling-data"></a>Etapa 1: Coletar dados de criação de perfil

1. Abra o projeto que deseja depurar no Visual Studio e defina um ponto de interrupção no aplicativo no ponto em que deseja examinar o uso da CPU.

2. Defina um segundo ponto de interrupção no final da função ou da região do código que deseja analisar.

    Definindo dois pontos de interrupção, você pode limitar a coleta de dados às partes do código que deseja analisar.

3. A janela de **ferramentas de diagnóstico** aparece automaticamente, a menos que você a tenha desativado. Para exibir a janela novamente, clique em **depurar**  >  **janelas**  >  **Mostrar ferramentas de diagnóstico**.

4. Você pode optar por ver **Uso de CPU** e/ou [Uso de Memória](../profiling/Memory-Usage.md), com a configuração **Selecionar Ferramentas** na barra de ferramentas. Se estiver executando Visual Studio Enterprise, você também poderá habilitar ou desabilitar o IntelliTrace no **Tools**  >  **Options**  >  **IntelliTrace**opções de ferramentas.

     ![Mostrar ferramentas de diagnóstico](../profiling/media/diag-tools-select-tool.png "DiagToolsSelectTool")

     Vamos observar principalmente a utilização da CPU, portanto verifique se **Uso de CPU** está habilitado (é habilitado por padrão).

5. Clique em **depurar**  >  **Iniciar Depuração** (ou **Iniciar** na barra de ferramentas ou **F5**).

     Quando o aplicativo terminar de ser carregado, a exibição Resumo das Ferramentas de Diagnóstico será exibida. Se você precisar abrir a janela, clique em **depurar**  >  **janelas**  >  **Mostrar ferramentas de diagnóstico**.

     ![Guia Resumo das ferramentas de diagnóstico](../profiling/media/diag-tools-summary-tab.png "DiagToolsSummaryTab")

     Para obter mais informações sobre os eventos, consulte [pesquisando e filtrando a guia eventos da janela ferramentas de diagnóstico](https://devblogs.microsoft.com/devops/searching-and-filtering-the-events-tab-of-the-diagnostic-tools-window/).

6. Execute o cenário que fará com que o primeiro ponto de interrupção seja atingido.

7. Enquanto o depurador estiver em pausa, habilite a coleta dos dados de Uso da CPU e, em seguida, abra a guia **Uso da CPU**.

     ![Ferramentas de diagnóstico Habilitar criação de perfil de CPU](../profiling/media/diag-tools-enable-cpu-profiling.png "DiagToolsEnableCPUProfiling")

     Quando você escolher **Registrar perfil de CPU**, o Visual Studio começará a registrar suas funções e quanto tempo elas levam para ser executadas. Você somente poderá exibir esses dados coletados quando o aplicativo for parado em um ponto de interrupção.

8. Pressione F5 para executar o aplicativo até o segundo ponto de interrupção.

     Agora, você tem dados de desempenho do aplicativo especificamente para a região do código que é executada entre os dois pontos de interrupção.

     O criador de perfil começa a preparar os dados de thread. Aguarde sua conclusão.

     ![Ferramentas de diagnóstico preparando threads](../profiling/media/diag-tools-preparing-data.png "DiagToolsPreparingThreads")

     A ferramenta de Uso de CPU exibe o relatório na guia **Uso da CPU**.

     ![Guia uso de CPU das ferramentas de diagnóstico](../profiling/media/diag-tools-cpu-usage-tab.png "DiagToolsCPUUsageTab")

9. Se você quiser selecionar uma região de código mais específica para analisar, selecione uma região na linha do tempo da CPU (deve ser uma região que mostre dados de criação de perfil).

     ![Ferramentas de diagnóstico selecionando um segmento de tempo](../profiling/media/diag-tools-select-time-segment.png "DiagToolsSelectTimeSegment")

     Neste ponto, você pode começar a analisar os dados.

     > [!TIP]
     >  Ao tentar identificar problemas de desempenho, faça várias medições. O desempenho naturalmente varia de execução para execução, e os caminhos de código normalmente são executados mais lentamente na primeira vez em que são executados devido a um trabalho de inicialização única, como o carregamento de DLLs, métodos de compilação JIT e inicialização de caches. Ao fazer várias medições, você obtém uma ideia melhor do intervalo e da mediana da métrica que está sendo mostrada, que permite que você compare a primeira vez em comparação com o desempenho de estado estável de uma área de código.

## <a name="step-2-analyze-cpu-usage-data"></a>Etapa 2: Analisar os dados de uso de CPU

Recomendamos que você comece a analisar os dados examinando a lista de funções em Uso da CPU, identificando as funções que fazem a maior parte do trabalho e, em seguida, fazendo uma análise mais detalhada de cada uma.

1. Na lista de funções, examine as funções que fazem a maior parte do trabalho.

    ![Lista de funções de uso de CPU das ferramentas de diagnóstico](../profiling/media/diag-tools-cpu-usage-function-list.png "DiagToolsCPUUsageFunctionList")

    > [!TIP]
    > As funções são listadas em ordem, começando com as que fazem a maior parte do trabalho (elas não ficam na ordem de chamada). Isso ajuda a identificar rapidamente as funções com execução mais longa.

2. Na lista de funções, clique duas vezes em uma das funções do aplicativo que está trabalhando muito.

    Quando você clica duas vezes em uma função, a exibição **Chamador/Computador Chamado** é aberta no painel esquerdo.

    ![Exibição Chamador/Computador Chamado das Ferramentas de Diagnóstico](../profiling/media/diag-tools-caller-callee.png "DiagToolsCallerCallee")

    Nesta exibição, a função selecionada aparece no título e na caixa **Função Atual** (GetNumber, neste exemplo). A função que chamou a função atual é mostrada à esquerda em **Funções Chamadoras** e todas as funções chamadas pela função atual são mostradas na caixa **Funções Chamadas** à direita. (Você pode selecionar cada uma das caixas para alterar a função atual.)

    Essa exibição mostra o tempo total (ms) e o percentual do tempo de execução geral do aplicativo que a função levou para ser concluída.
    **Corpo da Função** também mostra a quantidade total de tempo (e o percentual de tempo) gasta no corpo da função, excluindo o tempo gasto nas funções chamadoras e chamadas. (Neste exemplo, 2367 de 2389 ms foram gastos no corpo da função e os 22 ms restantes foram gastos em código externo chamado por essa função).

    > [!TIP]
    > Valores altos em **Corpo da Função** podem indicar um gargalo de desempenho dentro da própria função.

3. Para ver uma exibição de nível superior mostrando a ordem em que as funções são chamadas, selecione **Árvore de Chamadas** na lista suspensa, na parte superior do painel.

    Cada área enumerada na figura está relacionada a uma etapa do procedimento.

    ::: moniker range=">=vs-2019"
    ![Árvore de chamadas de ferramentas de diagnóstico](../profiling/media/vs-2019/diag-tools-call-tree.png "DiagToolsCallTree")
    ::: moniker-end
    ::: moniker range="vs-2017"
    ![Árvore de chamadas de ferramentas de diagnóstico](../profiling/media/diag-tools-call-tree.png "DiagToolsCallTree")
    ::: moniker-end

    |Imagem|Descrição|
    |-|-|
    |![Etapa 1](../profiling/media/ProcGuid_1.png "ProcGuid_1")|O nó de nível superior nas árvores de chamada de uso da CPU é um pseudo-nó|
    |![Etapa 2](../profiling/media/ProcGuid_2.png "ProcGuid_2")|Na maioria dos aplicativos, quando a opção [Mostrar Código Externo](#view-external-code) está desabilitada, o nó de segundo nível é um nó **[Código Externo]** que contém o código do sistema e da estrutura que inicia e para o aplicativo, desenha a interface do usuário, controla o agendamento de thread e fornece ao aplicativo outros serviços de nível inferior.|
    |![Etapa 3](../profiling/media/ProcGuid_3.png "ProcGuid_3")|Os filhos do nó de segundo nível são métodos e rotinas assíncronas do código de usuário que são chamados ou criados pelo sistema de segundo nível e código do framework.|
    |![Etapa 4](../profiling/media/ProcGuid_4.png "ProcGuid_4")|Os nós filhos de um método só contêm dados das chamadas do método pai. Quando **Mostrar Código Externo** é desabilitado, os métodos de aplicativo também podem conter um nó **[Código Externo]**.|

    Aqui há mais informações sobre os valores de coluna:

    - **Total de CPU** indica quanto trabalho foi feito pela função e por todas as funções chamadas por ela. Valores altos de total de CPU apontam para as funções que são mais dispendiosas em geral.

    - **Própria CPU** indica quanto trabalho foi feito pelo código no corpo da função, exceto o trabalho realizado pelas funções que foram chamadas por ele. Valores altos de **Própria CPU** podem indicar um gargalo de desempenho dentro da própria função.

    - **Módulos** O nome do módulo que contém a função ou o número de módulos que contêm as funções em um nó [Código Externo].

    ::: moniker range=">=vs-2019"
    Para ver as chamadas de função que usam a maior porcentagem de CPU no modo de exibição de árvore de chamadas, clique em **Expandir Afunilamento**.

    ![Caminho de aquecimento das ferramentas de diagnóstico](../profiling/media/vs-2019/diag-tools-hot-path.png "DiagToolsHotPath")
    ::: moniker-end

    > [!NOTE]
    > Se você visualizar o código na árvore de chamadas marcado como código "interrompido" ou "pilha inexplorável", isso indica que os eventos ETW (Rastreamento de Eventos para Windows) provavelmente foram descartados. Tente coletar o mesmo rastreamento uma segunda vez para resolver o problema.

## <a name="view-external-code"></a>Exibir código externo

O código externo são funções nos componentes do sistema e da estrutura executadas pelo código escrito. O código externo inclui funções que iniciam e param o aplicativo, elaboram a interface do usuário, controlam a segmentação e fornecem ao aplicativo outros serviços de nível inferior. Na maioria dos casos, você não está interessado em código externo, portanto, a ferramenta Uso de CPU reúne as funções externas de um método de usuário em um nó **[External Code]**.

Se você quiser exibir os caminhos de chamada do código externo, escolha **Mostrar Código Externo** na lista **Filtrar exibição** e, em seguida, escolha **Aplicar**.

![Escolha o modo de exibição de filtro e, em seguida, mostrar código externo](../profiling/media/diag-tools-show-external-code.png "DiagToolsShowExternalCode")

Saiba que muitas correntes de chamada de código externo são muito aninhadas, de forma que a largura da coluna Nome da Função pode exceder a largura da tela de todos os monitores de computador, exceto dos maiores. Quando isso acontece, os nomes de função são mostrados como **[...] **.

Use a caixa de pesquisa para localizar um nó que você esteja procurando e use a barra de rolagem horizontal para exibir os dados.

> [!TIP]
> Se você analisar um código externo que chama funções do Windows, deverá garantir que tem os arquivos .*pdb* mais atuais. Sem esses arquivos, as exibições de relatório listarão nomes de funções do Windows criptografadas e difíceis de entender. Para obter mais informações sobre como verificar se você tem os arquivos necessários, consulte especificar o [símbolo (. pdb) e os arquivos de origem no depurador](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como coletar e analisar dados de uso da CPU. Se você já concluiu o [Introdução às ferramentas de criação de perfil](../profiling/profiling-feature-tour.md), obtenha uma visão geral de como analisar o uso de memória em seus aplicativos.

> [!div class="nextstepaction"]
> [Uso de memória de perfil no Visual Studio](../profiling/memory-usage.md)
