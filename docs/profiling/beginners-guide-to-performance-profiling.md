---
title: Medir o uso da CPU em seus aplicativos
description: Analise problemas de desempenho da CPU em seu aplicativo usando as ferramentas de diagnóstico integradas ao depurador.
ms.custom: mvc
ms.date: 02/27/2017
ms.technology: vs-ide-debug
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 966697652e969c3d6de9f3c17f52f88e84c89bb8
ms.sourcegitcommit: bccb05b5b4e435f3c1f7c36ba342e7d4031eb398
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51220671"
---
# <a name="profile-application-performance-in-visual-studio"></a>Analisar desempenho de aplicativos no Visual Studio
Você pode usar as ferramentas de criação de perfil do Visual Studio para analisar problemas de desempenho em seu aplicativo. Este procedimento mostra como usar a guia **Uso de CPU** das Ferramentas de Diagnóstico para obter dados de desempenho do seu aplicativo. As Ferramentas de Diagnóstico têm suporte para desenvolvimento de .NET no Visual Studio, incluindo o ASP.NET e para desenvolvimento nativo/C++.
  
Quando o depurador pausa, a ferramenta **Uso de CPU** coleta informações sobre as funções que estão em execução no aplicativo. A ferramenta lista as funções que estavam executando o trabalho e fornece um gráfico de linha do tempo que você pode usar para se concentrar em segmentos específicos da sessão de amostragem.

O Hub de diagnósticos oferece várias outras opções para executar e gerenciar sua sessão de diagnóstico. Se **Uso de CPU** não fornecer os dados que você precisa, as [outras ferramentas de criação de perfil](../profiling/profiling-feature-tour.md) fornecem diferentes tipos de informações que poderão ser úteis. Em muitos casos, o gargalo de desempenho do aplicativo pode ser causado por algo que não seja a CPU, como memória, interface do usuário de renderização ou tempo de solicitação de rede. O Hub de diagnósticos oferece várias outras opções para registrar e analisar esse tipo de dados.

| | |
|---------|---------|
| ![ícone de câmera para vídeo](../install/media/video-icon.png "Assistir a um vídeo") | [Assista a um vídeo](https://mva.microsoft.com/en-US/training-courses-embed/getting-started-with-visual-studio-2017-17798/Profiling-with-Diagnostics-Tools-in-Visual-Studio-2017-daHnzMD6D_9211787171) sobre como usar as ferramentas de diagnóstico que mostra como analisar o uso da CPU e como analisar o uso de memória. |

Neste artigo, abordaremos a análise do uso de CPU no fluxo de trabalho de depuração normal. Você também pode analisar o uso da CPU sem um depurador conectado ou direcionando um aplicativo em execução. Para saber mais, confira [Coletar dados de criação de perfil sem depuração](../profiling/running-profiling-tools-with-or-without-the-debugger.md#collect-profiling-data-without-debugging) em [Executando ferramentas de criação de perfil com ou sem o depurador](../profiling/running-profiling-tools-with-or-without-the-debugger.md).

Você pode usar as ferramentas de criação de perfil sem o depurador com o Windows 7 e posteriores. O Windows 8 ou posterior é necessário para executar ferramentas de criação de perfil com o depurador (janela **Ferramentas de Diagnóstico**).

Neste tutorial, você irá:

> [!div class="checklist"]
> * Coletar dados de uso da CPU
> * Analisar os dados de uso da CPU
  
## <a name="step-1-collect-profiling-data"></a>Etapa 1: Coletar dados de criação de perfil 
  
1.  Abra o projeto que deseja depurar no Visual Studio e defina um ponto de interrupção no aplicativo no ponto em que deseja examinar o uso da CPU.

2.  Defina um segundo ponto de interrupção no final da função ou da região do código que deseja analisar.

    > [!TIP]
    > Definindo dois pontos de interrupção, você pode limitar a coleta de dados às partes do código que deseja analisar.
  
3.  A janela **Ferramentas de Diagnóstico** é exibida automaticamente, a menos que tenha sido desativada. Para abrir a janela novamente, clique em **Depurar** > **Windows** > **Mostrar Ferramentas de Diagnóstico**.

4.  Você pode optar por ver **Uso de CPU** e/ou [Uso de Memória](../profiling/Memory-Usage.md), com a configuração **Selecionar Ferramentas** na barra de ferramentas. Se você estiver executando o Visual Studio Enterprise, poderá também habilitar ou desabilitar o IntelliTrace em **Ferramentas** > **Opções** > **IntelliTrace**.

     ![Mostrar Ferramentas de Diagnósticos](../profiling/media/DiagToolsSelectTool.png "DiagToolsSelectTool")

     Vamos observar principalmente a utilização da CPU, portanto verifique se **Uso de CPU** está habilitado (é habilitado por padrão).

5.  Clique em **Depurar** > **Iniciar Depuração** (ou em **Iniciar** na barra de ferramentas ou em **F5**).

     Quando o aplicativo terminar de ser carregado, a exibição Resumo das Ferramentas de Diagnóstico será exibida.

     ![Guia Resumo das Ferramentas de Diagnóstico](../profiling/media/DiagToolsSummaryTab.png "DiagToolsSummaryTab")

     Para obter mais informações sobre os eventos, confira [Searching and filtering the Events tab of the Diagnostic Tools window](https://blogs.msdn.microsoft.com/devops/2015/11/12/searching-and-filtering-the-events-tab-of-the-diagnostic-tools-window/) (Pesquisando e filtrando a guia Eventos da janela Ferramentas de Diagnóstico).

6.  Execute o cenário que fará com que o primeiro ponto de interrupção seja atingido.

7.  Enquanto o depurador estiver em pausa, habilite a coleta dos dados de Uso da CPU e, em seguida, abra a guia **Uso da CPU**.

     ![Ferramentas de Diagnóstico, Habilitar a Criação de Perfil de CPU](../profiling/media/DiagToolsEnableCPUProfiling.png "DiagToolsEnableCPUProfiling")

     Quando você escolher **Registrar perfil de CPU**, o Visual Studio começará a registrar suas funções e quanto tempo elas levam para ser executadas. Você somente poderá exibir esses dados coletados quando o aplicativo for parado em um ponto de interrupção.

8.  Pressione F5 para executar o aplicativo até o segundo ponto de interrupção.

     Agora, você tem dados de desempenho do aplicativo especificamente para a região do código que é executada entre os dois pontos de interrupção.

9.  Selecione a região que você deseja analisar na linha do tempo da CPU (precisa ser uma região que mostre dados de criação de perfil).

     ![Ferramentas de Diagnóstico, Selecionando um Segmento de Tempo](../profiling/media/DiagToolsSelectTimeSegment.png "DiagToolsSelectTimeSegment")

     O criador de perfil começa a preparar os dados de thread. Aguarde sua conclusão.

     ![Ferramentas de Diagnóstico, Preparando Threads](../profiling/media/DiagToolsPreparingThreads.png "DiagToolsPreparingThreads")
  
     A ferramenta de Uso de CPU exibe o relatório na guia **Uso da CPU**.
  
     ![Guia Uso da CPU da Ferramentas de Diagnóstico](../profiling/media/DiagToolsCPUUsageTab.png "DiagToolsCPUUsageTab")

     Neste ponto, você pode começar a analisar os dados.

## <a name="step-2-analyze-cpu-usage-data"></a>Etapa 2: Analisar os dados de uso de CPU

Recomendamos que você comece a analisar os dados examinando a lista de funções em Uso da CPU, identificando as funções que fazem a maior parte do trabalho e, em seguida, fazendo uma análise mais detalhada de cada uma.

1. Na lista de funções, examine as funções que fazem a maior parte do trabalho.

    ![Lista de Funções de Uso de CPU das Ferramentas de Diagnóstico](../profiling/media/DiagToolsCPUUsageFunctionList.png "DiagToolsCPUUsageFunctionList")

    > [!TIP]
    > As funções são listadas em ordem, começando com as que fazem a maior parte do trabalho (elas não ficam na ordem de chamada). Isso ajuda a identificar rapidamente as funções com execução mais longa.

2. Na lista de funções, clique duas vezes em uma das funções do aplicativo que está trabalhando muito.

    Quando você clica duas vezes em uma função, a exibição **Chamador/Computador Chamado** é aberta no painel esquerdo. 

    ![Exibição Chamador/Computador Chamado da Chamada das Ferramentas de Diagnóstico](../profiling/media/DiagToolsCallerCallee.png "DiagToolsCallerCallee")

    Nesta exibição, a função selecionada aparece no título e na caixa **Função Atual** (GetNumber, neste exemplo). A função que chamou a função atual é mostrada à esquerda em **Função Chamadora** e todas as funções chamadas pela função atual são mostradas na caixa **Funções Chamadas** à direita. (Você pode selecionar cada uma das caixas para alterar a função atual.)

    Essa exibição mostra o tempo total (ms) e o percentual do tempo de execução geral do aplicativo que a função levou para ser concluída.
    **Corpo da Função** também mostra a quantidade total de tempo (e o percentual de tempo) gasta no corpo da função, excluindo o tempo gasto nas funções chamadoras e chamadas. (Neste exemplo, 3713 de 3729 ms foram gastos no corpo da função e os 16 ms restantes foram gastos em código externo chamado por essa função).

    > [!TIP]
    > Valores altos em **Corpo da Função** podem indicar um gargalo de desempenho dentro da própria função.

3. Se você quiser ver uma exibição de nível superior mostrando a ordem em que as funções são chamadas, selecione **Árvore de Chamadas** na lista suspensa, na parte superior do painel.
 
    Cada área enumerada na figura está relacionada a uma etapa do procedimento.
  
    ![Árvore de Chamadas das Ferramentas de Diagnóstico](../profiling/media/DiagToolsCallTree.png "DiagToolsCallTree")
  
|||
|-|-|
|![Etapa 1](../profiling/media/ProcGuid_1.png "ProcGuid_1")|O nó de nível superior nas árvores de chamada de uso da CPU é um pseudo-nó|  
|![Etapa 2](../profiling/media/ProcGuid_2.png "ProcGuid_2")|Na maioria dos aplicativos, quando a opção [Mostrar Código Externo](#view-external-code) está desabilitada, o nó de segundo nível é um nó **[Código Externo]** que contém o código do sistema e da estrutura que inicia e para o aplicativo, desenha a interface do usuário, controla o agendamento de thread e fornece ao aplicativo outros serviços de nível inferior.|  
|![Etapa 3](../profiling/media/ProcGuid_3.png "ProcGuid_3")|Os filhos do nó de segundo nível são métodos e rotinas assíncronas do código de usuário que são chamados ou criados pelo sistema de segundo nível e código do framework.|
|![Etapa 4](../profiling/media/ProcGuid_4.png "ProcGuid_4")|Os nós filhos de um método só contêm dados das chamadas do método pai. Quando **Mostrar Código Externo** é desabilitado, os métodos de aplicativo também podem conter um nó **[Código Externo]**.|

Aqui há mais informações sobre os valores de coluna:

- **Total de CPU** indica quanto trabalho foi feito pela função e por todas as funções chamadas por ela. Valores altos de total de CPU apontam para as funções que são mais dispendiosas em geral.
  
- **Própria CPU** indica quanto trabalho foi feito pelo código no corpo da função, exceto o trabalho realizado pelas funções que foram chamadas por ele. Valores altos de **Própria CPU** podem indicar um gargalo de desempenho dentro da própria função.

- **Módulos** O nome do módulo que contém a função ou o número de módulos que contêm as funções em um nó [Código Externo].

## <a name="view-external-code"></a>Exibir código externo

O código externo são funções nos componentes do sistema e da estrutura executadas pelo código escrito. O código externo inclui funções que iniciam e param o aplicativo, elaboram a interface do usuário, controlam a segmentação e fornecem ao aplicativo outros serviços de nível inferior. Na maioria dos casos, você não está interessado em código externo, portanto, a ferramenta Uso de CPU reúne as funções externas de um método de usuário em um nó **[External Code]**.
  
Se você quiser exibir os caminhos de chamada do código externo, escolha **Mostrar Código Externo** na lista **Filtrar exibição** e, em seguida, escolha **Aplicar**.  
  
![Escolha Filtrar Exibição, em seguida, Mostrar Código Externo](../profiling/media/DiagToolsShowExternalCode.png "DiagToolsShowExternalCode")  
  
Saiba que muitas correntes de chamada de código externo são muito aninhadas, de forma que a largura da coluna Nome da Função pode exceder a largura da tela de todos os monitores de computador, exceto dos maiores. Quando isso acontece, os nomes de função são mostrados como **[...]** .
  
Use a caixa de pesquisa para localizar um nó que você esteja procurando e use a barra de rolagem horizontal para exibir os dados.

> [!TIP]
> Se você analisar um código externo que chama funções do Windows, deverá garantir que tem os arquivos .*pdb* mais atuais. Sem esses arquivos, as exibições de relatório listarão nomes de funções do Windows criptografadas e difíceis de entender. Para saber mais sobre como garantir que você tem os arquivos necessários, confira [Especificar arquivos de símbolo (.pdb) e de origem no depurador](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como coletar e analisar dados de uso da CPU. Se você já concluiu o [Introdução às ferramentas de criação de perfil](../profiling/profiling-feature-tour.md), obtenha uma visão geral de como analisar o uso de memória em seus aplicativos.

> [!div class="nextstepaction"]
> [Analisar o uso de memória no Visual Studio](../profiling/memory-usage.md) 
