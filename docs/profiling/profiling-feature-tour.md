---
title: Medir o desempenho com ferramentas de criação de perfil
description: Dê uma olhada rápida em diferentes ferramentas de diagnóstico disponíveis no Visual Studio.
ms.custom: mvc
ms.date: 05/18/2017
ms.technology: vs-ide-debug
ms.topic: quickstart
helpviewer_keywords:
- diagnostic tools
ms.assetid: d2ee0301-ea78-43d8-851a-71b7b2043d73
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 9f884b92d03027782eed27f4583e06b1141341db
ms.sourcegitcommit: e680e8ac675f003ebcc8f8c86e27f54ff38da662
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2018
ms.locfileid: "49356789"
---
# <a name="quickstart-first-look-at-profiling-tools"></a>Início rápido: primeiro olhar sobre ferramentas de criação de perfil

O Visual Studio fornece uma variedade de ferramentas de criação de perfil para ajudá-lo a diagnosticar diferentes tipos de problemas de desempenho, dependendo do tipo do aplicativo.

As ferramentas de criação de perfil que podem ser acessadas durante uma sessão de depuração estão disponíveis na janela Ferramentas de Diagnóstico. A janela Ferramentas de Diagnóstico é exibida automaticamente, a menos que tenha sido desativada. Para abrir a janela, clique em **Depurar/Windows/Mostrar Ferramentas de Diagnóstico**. Com a janela aberta, é possível selecionar ferramentas para as quais você deseja coletar dados.

![Janela Ferramentas de Diagnóstico](../profiling/media/prof-tour-diagnostic-tools.png "Ferramentas de Diagnóstico")

Durante a depuração, é possível usar a janela **Ferramentas de Diagnóstico** para analisar o uso da CPU e de memória e exibir os eventos que mostram informações relacionadas ao desempenho.

![Exibição do Resumo de Ferramentas de Diagnóstico](../profiling/media/prof-tour-cpu-and-memory-graph.gif "Resumo de Ferramentas de Diagnóstico")

A janela **Ferramentas de Diagnóstico** costuma ser a maneira preferencial para criar perfis de aplicativos, mas para builds de Versão também é possível fazer uma análise post-mortem do aplicativo. Se você quiser obter mais informações sobre diferentes abordagens, confira [Executar ferramentas de criação de perfil com ou sem o depurador](../profiling/running-profiling-tools-with-or-without-the-debugger.md). Para ver o suporte à ferramentas de criação de perfil para tipos diferentes de aplicativo, confira [Qual ferramenta devo usar?](#which-tool-should-i-use).

> [!NOTE]
> Você pode usar as ferramentas post-mortem com o Windows 7 e posteriores. O Windows 8 ou posterior é necessário para executar ferramentas de criação de perfil com o depurador (janela **Ferramentas de Diagnóstico**).

## <a name="analyze-cpu-usage"></a>Analisar o uso de CPU

A ferramenta Uso da CPU é um bom lugar para começar a analisar o desempenho do aplicativo. Ela informará mais sobre os recursos de CPU que o aplicativo está consumindo. Para obter uma explicação mais detalhada da ferramenta Uso da CPU, confira [Guia do iniciante para criação de perfil de desempenho](../profiling/beginners-guide-to-performance-profiling.md).

Na exibição **Resumo** das Ferramentas de Diagnóstico, escolha **Habilitar Criação de Perfil da CPU** (é necessário estar em uma sessão de depuração).

![Habilitar o uso da CPU nas Ferramentas de Diagnóstico](../profiling/media/prof-tour-enable-cpu-profiling.png "Habilitar o Uso da CPU nas Ferramentas de Diagnóstico")

Para usar a ferramenta com mais eficiência, defina dois pontos de interrupção no código: um no início e outro no final da função ou na região de código que você deseja analisar. Examine os dados de criação de perfil quando eles estiverem em pausa no segundo ponto de interrupção.

A exibição **Uso da CPU** mostra uma lista de funções ordenadas pela execução mais longa, com a função de execução mais longa na parte superior. Isso pode ajudar a levá-lo para as funções em que estão ocorrendo gargalos de desempenho.

![Exibição de Uso da CPU das Ferramentas de Diagnóstico](../profiling/media/prof-tour-cpu-usage.png "Uso da CPU das Ferramentas de Diagnóstico")

Clique duas vezes em uma função de interesse e você verá uma exibição "borboleta" de três painéis mais detalhada, com a função selecionada no centro da janela, a função de chamada à esquerda e as funções chamadas à direita. A seção **Corpo da função** também mostra o tempo total (e o percentual de tempo) gasto no corpo da função, excluindo o tempo gasto nas funções de chamada e nas funções chamadas. Esses dados podem ajudá-lo a avaliar se a própria função é um gargalo de desempenho.

![Exibição "borboleta" de Computador Chamado do Chamador das Ferramentas de Diagnóstico](../profiling/media/prof-tour-cpu-usage-caller-callee.png "Exibição de Computador Chamado do Chamador das Ferramentas de Diagnóstico")

## <a name="analyze-memory-usage"></a>Analisar o uso de memória

A janela **Ferramentas de Diagnóstico** também permite avaliar o uso de memória no aplicativo. Por exemplo, é possível examinar o número e tamanho dos objetos no heap. Para obter instruções mais detalhadas para analisar a memória, confira [Analisar uso da memória](../profiling/memory-usage.md).

Para analisar o uso de memória, você precisa obter pelo menos um instantâneo de memória durante a depuração. Em geral, a melhor maneira de analisar a memória é usar dois instantâneos: o primeiro, logo antes de um problema de memória suspeito e o segundo instantâneo, logo após a ocorrência de um problema de memória suspeito. Depois, é possível exibir uma comparação dos dois instantâneos e ver exatamente o que mudou.

![Tirar um instantâneo nas Ferramentas de Diagnóstico](../profiling/media/prof-tour-take-snapshots.gif "Tirar Instantâneo nas Ferramentas de Diagnóstico")

Ao selecionar um dos links a seta, você terá uma exibição diferencial do heap (uma seta vermelha para cima ![Aumento do Uso de Memória](../profiling/media/prof-tour-mem-usage-up-arrow.png "Aumento do Uso de Memória") mostra uma contagem crescente de objetos – à esquerda – ou um tamanho crescente de heap – à direita). Se você clicar no link à direita, terá uma exibição diferencial do heap, ordenada por objetos com maior aumento de tamanho de heap. Isso pode ajudá-lo a identificar problemas de memória. Por exemplo, na ilustração abaixo, os bytes usados por objetos `ClassHandlersStore` aumentaram em 3.492 bytes no segundo instantâneo.

![Exibição Comparação de heap das Ferramentas de Diagnóstico](../profiling/media/prof-tour-mem-usage-diff-heap.png "Exibição Comparação de Heap das Ferramentas de Diagnóstico")

Se você clicar no link à esquerda, na exibição **Uso de Memória**, a exibição do heap será organizada pela contagem de objetos: os objetos de um tipo específico com maior aumento em número são mostrados na parte superior (classificados pela coluna **Comparação de Contagem**).

## <a name="examine-performance-events"></a>Examinar eventos de desempenho

A exibição **Eventos** das Ferramentas de Diagnóstico mostra diferentes eventos que ocorrem durante a depuração, como a configuração de um ponto de interrupção ou uma operação de execução de código em etapas. É possível verificar informações como a duração do evento (medido da última pausa do depurador ou da inicialização do aplicativo). Por exemplo, se você executar o código em etapas (F10, F11), a exibição **Eventos** mostrará a duração de tempo de execução do aplicativo da operação de etapa anterior à etapa atual.

![Exibição Eventos de Ferramentas de Diagnóstico](../profiling/media/prof-tour-events.png "Exibição Eventos de Ferramentas de Diagnóstico")

 > [!NOTE]
 > Se você tiver o Visual Studio Enterprise, também poderá ver [eventos do IntelliTrace](../debugger/intellitrace.md) nessa guia.

Os mesmos eventos também são mostrados no editor de código, que podem ser exibidos como PerfTips.

![Tour pela criação de perfil – PerfTips](../profiling/media/prof-tour-perf-tips.png "Tour pela criação de perfil – PerfTips")

## <a name="examine-ui-performance-and-accessibility-events-uwp"></a>Examinar os eventos de desempenho e de acessibilidade da interface do usuário (UWP)

Nos aplicativos UWP, é possível habilitar a **Análise de interface do usuário** na janela **Ferramentas de Diagnóstico**. A ferramenta pesquisa problemas comuns de desempenho ou de acessibilidade, mostrando-os na exibição **Eventos** durante a depuração. As descrições de eventos fornecem informações que podem ajudar a resolver problemas.

![Exibir eventos de análise da interface do usuário nas ferramentas de diagnóstico](../profiling/media/prof-tour-ui-analysis.png "Exibir eventos de análise da interface do usuário nas Ferramentas de Diagnóstico")

## <a name="post_mortem"></a> Builds de versão de perfil sem o depurador

As ferramentas de criação de perfil como Uso da CPU e Uso da Memória podem ser usadas com o depurador (veja as seções anteriores) ou é possível executar ferramentas de criação de perfil post-mortem usando o Criador de Perfil de Desempenho, cuja função é fornecer análise para builds de **Versão**. No Criador de Perfil de Desempenho, é possível coletar informações de diagnóstico durante a execução do aplicativo e, em seguida, examinar as informações coletadas depois que o aplicativo é interrompido. Para obter mais informações sobre essas diferentes abordagens, confira [Executar ferramentas de criação de perfil com ou sem o depurador](../profiling/running-profiling-tools-with-or-without-the-debugger.md).

![Criador de Perfil de Desempenho](../profiling/media/prof-tour-performance-profiler.png "Criador de Perfil de Desempenho")

Abra o Criador de Perfil de Desempenho escolhendo **Depurar** > **Criador de Perfil de Desempenho**.

A janela permitirá selecionar várias ferramentas de criação de perfil em alguns cenários. Ferramentas como Uso da CPU podem fornecer dados complementares que podem ser usados para ajudar na análise.

## <a name="analyze-resource-consumption-xaml"></a>Analisar o consumo de recursos (XAML)

Em aplicativos XAML, como aplicativos WPF da área de trabalho do Windows e aplicativos UWP, é possível analisar o consumo de recursos usando a ferramenta Linha do Tempo do Aplicativo. Por exemplo, é possível analisar o tempo gasto pelo aplicativo para preparar quadros de interface do usuário (layout e renderização), atender a solicitações de rede e de disco e em cenários como inicialização do aplicativo, carregamento de página e redimensionamento do Windows. Para usar a ferramenta, escolha **Linha do Tempo do Aplicativo** no Criador de Perfil de Desempenho e, em seguida, escolha **Iniciar**. No aplicativo, percorra o cenário com um problema de consumo de recursos suspeito e escolha **Parar coleta** para gerar o relatório.

Taxas de quadros baixas no gráfico **Taxa de transferência visual** podem corresponder aos problemas visuais vistos ao executar o aplicativo. Da mesma forma, números elevados no gráfico **Utilização de thread de interface do usuário** também podem corresponder a problemas de capacidade de resposta da interface do usuário. No relatório, é possível selecionar um período com um problema de desempenho suspeito e, em seguida, examinar as atividades detalhadas de thread de interface do usuário na exibição Detalhes da linha do tempo (painel inferior).

![Ferramenta de criação de perfil de Linha do Tempo do Aplicativo](../profiling/media/prof-tour-application-timeline.gif "Linha do Tempo do Aplicativo de Tour pela Criação de Perfil")

Na exibição Detalhes da linha do tempo, você encontrará informações como o tipo de atividade (ou o elemento de interface do usuário envolvido) junto com a duração da atividade. Por exemplo, na ilustração, um evento **Layout** de um controle Grade usa 57,53 ms.

Para obter mais informações, consulte [Linha do Tempo do Aplicativo](../profiling/application-timeline.md).

## <a name="analyze-gpu-usage-direct3d"></a>Analisar o uso da GPU (Direct3D)

Em aplicativos Direct3D (os componentes Direct3D devem estar no C++), é possível examinar a atividade na GPU e analisar problemas de desempenho. Para obter mais informações, consulte [Uso da GPU](../debugger/gpu-usage.md). Para usar a ferramenta, escolha **Uso da GPU** no Criador de Perfil de Desempenho e, em seguida, escolha **Iniciar**. No aplicativo, percorra o cenário de interesse na criação de perfil e, em seguida, escolha **Parar coleta** para gerar um relatório.

Ao selecionar um período nos gráficos e escolher **Exibir detalhes**, uma exibição detalhada será exibida no painel inferior. Na exibição detalhada, é possível examinar as atividades que estão ocorrendo em cada CPU e GPU. Selecione eventos no painel inferior para obter pop-ups na linha do tempo. Por exemplo, selecione o eventos **Presente** para exibir pop-ups da chamada **Presente**. (As linhas verticais Vsync cinza-claras podem ser usadas como referência para entender se algumas chamadas **Presente** não têm Vsync. Deve haver uma chamada **Presente** entre cada dois Vsyncs para que o aplicativo atinja progressivamente 60 FPS.)

![Ferramenta de criação de perfil de Uso de GPU](../profiling/media/prof-tour-gpu-usage.png "Uso de GPU de Diagnóstico")

Também é possível usar os gráficos para determinar se há gargalos de desempenho limitados à CPU ou à GPU.

## <a name="analyze-performance-javascript-uwp"></a>Analisar o desempenho (JavaScript UWP)

Para aplicativos UWP, é possível usar a ferramenta Memória JavaScript e a ferramenta Capacidade de Resposta de IU em HTML.

A ferramenta Memória JavaScript é semelhante à ferramenta Uso de Memória disponível para outros tipos de aplicativos. É possível usar essa ferramenta para entender o uso de memória e encontrar perdas de memória no aplicativo. Para obter mais detalhes sobre a ferramenta, consulte [Memória JavaScript](../profiling/javascript-memory.md).

![Ferramenta de criação de perfil de Memória JavaScript](../profiling/media/diagjsmemory.png "DiagJSMemory")

Para diagnosticar a capacidade de resposta de IU, tempo de carregamento lento e atualizações visuais lentas em aplicativos UWP, use a ferramenta Capacidade de Resposta de IU em HTML. O uso é semelhante à ferramenta Linha do Tempo do Aplicativo para outros tipos de aplicativos. Para obter mais informações, consulte [Capacidade de resposta de interface do usuário HTML](../profiling/html-ui-responsiveness.md).

![Ferramenta de criação de perfil de capacidade de resposta da interface do usuário HTML](../profiling/media/diaghtmlresp.png "DiagHTMLResp")

## <a name="analyze-network-usage-uwp"></a>Analisar o uso de rede (UWP)

Em aplicativos UWP, é possível analisar as operações de rede executadas usando a API `Windows.Web.Http`. Essa ferramenta pode ajudá-lo a resolver problemas, como problemas de acesso e autenticação, uso de cache incorreto e desempenho insatisfatório de exibição e download. Para usar a ferramenta, escolha **Rede** no Criador de Perfil de Desempenho e, em seguida, escolha **Iniciar**. No aplicativo, percorra o cenário que usa `Windows.Web.Http` e escolha **Parar coleta** para gerar o relatório.

![Ferramenta de criação de perfil de Uso de Rede](../profiling/media/prof-tour-network-usage.png "Uso de Rede de Diagnóstico")

Selecione uma operação na exibição de resumo para exibir mais detalhes.

![Informações detalhadas na ferramenta de Uso de Rede](../profiling/media/prof-tour-network-usage-details.png "Detalhes de Uso de Rede de Diagnóstico")

Para obter mais informações, consulte [Uso de rede](../profiling/network-usage.md).

## <a name="analyze-performance-legacy-tools"></a>Analisar o desempenho (ferramentas herdadas)

Se você precisar de recursos, como instrumentação, que não estão atualmente presentes nas ferramentas Uso da CPU ou Uso de Memória, e estiver executando aplicativos de área de trabalho ou aplicativos ASP.NET, poderá usar o Gerenciador de Desempenho para a criação de perfil. (Sem suporte em aplicativos UWP). Para obter mais informações, consulte [Gerenciador de Desempenho](../profiling/performance-explorer.md).

![Ferramenta de Gerenciador de Desempenho](../profiling/media/prof-tour-performance-explorer.png "Gerenciador de Desempenho")

## <a name="which-tool-should-i-use"></a>Qual ferramenta devo usar?  

Eis aqui uma tabela que lista as diferentes ferramentas que o Visual Studio oferece e os diferentes tipos de projeto com os quais você poderá usá-las:
  
|Ferramenta de Desempenho|Área de Trabalho do Windows|UWP|ASP.NET/ASP.NET Core| 
|----------------------|---------------------|-------------|-------------|  
|[Uso da CPU](../profiling/cpu-usage.md)|sim|sim|sim|
|[Uso de Memória](../profiling/memory-usage.md)|sim|sim|sim| 
|[Uso de GPU](../debugger/gpu-usage.md)|sim|sim|no| 
|[Linha do tempo do aplicativo](../profiling/application-timeline.md)|sim|sim|no|
|[PerfTips](../profiling/perftips.md)|sim|sim para XAML, não para HTML|sim|
|[Gerenciador de Desempenho](../profiling/performance-explorer.md)|sim|no|sim|
|[IntelliTrace](../debugger/intellitrace.md)|.NET com Visual Studio Enterprise somente|.NET com Visual Studio Enterprise somente|.NET com Visual Studio Enterprise somente|
|[Uso de rede](../profiling/network-usage.md)|no|sim|no|
|[Capacidade de Resposta de interface do usuário em HTML](../profiling/html-ui-responsiveness.md)|no|sim para HTML, não para XAML|no| 
|[Memória JavaScript](../profiling/javascript-memory.md)|no|sim para HTML, não para XAML|no|

## <a name="see-also"></a>Consulte também  
 [Depurando no Visual Studio](../debugger/debugging-in-visual-studio.md)
