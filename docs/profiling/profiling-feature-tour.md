---
title: Medir o desempenho com ferramentas de criação de perfil
description: Dê uma olhada rápida em diferentes ferramentas de diagnóstico disponíveis no Visual Studio.
ms.custom: mvc
ms.date: 06/03/2020
ms.topic: quickstart
helpviewer_keywords:
- diagnostic tools
ms.assetid: d2ee0301-ea78-43d8-851a-71b7b2043d73
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7c1f2583b0624691405ec3ef5a88aa11cb796327
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85816678"
---
# <a name="first-look-at-profiling-tools"></a>Introdução às ferramentas de criação de perfil

O Visual Studio fornece uma variedade de ferramentas de criação de perfil para ajudá-lo a diagnosticar diferentes tipos de problemas de desempenho, dependendo do tipo do aplicativo. Neste artigo, vamos dar uma olhada rápida nas ferramentas de criação de perfil mais comuns.

## <a name="view-performance-while-debugging"></a>Exibir o desempenho durante a depuração

As ferramentas de criação de perfil que podem ser acessadas durante uma sessão de depuração estão disponíveis na janela Ferramentas de Diagnóstico. A janela Ferramentas de Diagnóstico é exibida automaticamente, a menos que tenha sido desativada. Para abrir a janela, clique em **Depurar/Windows/Mostrar Ferramentas de Diagnóstico**. Com a janela aberta, é possível selecionar ferramentas para as quais você deseja coletar dados.

![Janela de Ferramentas de Diagnóstico](../profiling/media/prof-tour-diagnostic-tools.png "Ferramentas de Diagnóstico")

Durante a depuração, é possível usar a janela **Ferramentas de Diagnóstico** para analisar o uso da CPU e de memória e exibir os eventos que mostram informações relacionadas ao desempenho.

![Exibição de resumo Ferramentas de Diagnóstico](../profiling/media/prof-tour-cpu-and-memory-graph.gif "Resumo de Ferramentas de Diagnóstico")

A janela de **ferramentas de diagnóstico** é uma maneira comum de criar o perfil de aplicativos, mas para compilações de versão, você também pode fazer uma análise pós-morte de seu aplicativo em vez disso. Para obter mais informações sobre abordagens diferentes, consulte [executar ferramentas de criação de perfil com ou sem o depurador](../profiling/running-profiling-tools-with-or-without-the-debugger.md). Para ver o suporte à ferramentas de criação de perfil para tipos diferentes de aplicativo, confira [Qual ferramenta devo usar?](#which-tool-should-i-use).

> [!NOTE]
> Você pode usar as ferramentas post-mortem com o Windows 7 e posteriores. O Windows 8 ou posterior é necessário para executar ferramentas de criação de perfil com o depurador (janela **Ferramentas de Diagnóstico**).

## <a name="examine-performance-using-perftips"></a>Examinar o desempenho usando o PerfTips

Geralmente, a maneira mais fácil de exibir informações de desempenho é usar o [PerfTips](../profiling/perftips.md). Usando o PerfTips, você pode exibir informações de desempenho ao interagir com seu código. É possível verificar informações como a duração do evento (medido da última pausa do depurador ou da inicialização do aplicativo). Por exemplo, se você percorrer código (F10, F11), PerfTips mostrará a duração do tempo de execução do aplicativo da operação de etapa anterior para a etapa atual.

![PerfTips do Tour de criação de perfil](../profiling/media/prof-tour-perf-tips.png "PerfTips do Tour de criação de perfil")

Você pode usar o PerfTips para examinar quanto tempo leva para um bloco de código ser executado ou quanto tempo leva para que uma única função seja concluída.

PerfTips mostram os mesmos eventos que também aparecem na exibição de **eventos** do ferramentas de diagnóstico. No modo de exibição **eventos** , você pode exibir eventos diferentes que ocorrem durante a depuração, como a configuração de um ponto de interrupção ou uma operação de depuração de código.

![Exibição de eventos de Ferramentas de Diagnóstico](../profiling/media/prof-tour-events.png "Ferramentas de Diagnóstico exibir eventos")

 > [!NOTE]
 > Se você tiver o Visual Studio Enterprise, também poderá ver [eventos do IntelliTrace](../debugger/intellitrace.md) nessa guia.

## <a name="analyze-cpu-usage"></a>Analisar o uso de CPU

A ferramenta Uso da CPU é um bom lugar para começar a analisar o desempenho do aplicativo. Ela informará mais sobre os recursos de CPU que o aplicativo está consumindo. Para obter uma explicação mais detalhada da ferramenta de uso da CPU, consulte [medir o desempenho do aplicativo analisando o uso da CPU](../profiling/beginners-guide-to-performance-profiling.md).

Na exibição **Resumo** das Ferramentas de Diagnóstico, escolha **Habilitar Criação de Perfil da CPU** (é necessário estar em uma sessão de depuração).

![Habilitar o uso da CPU no Ferramentas de Diagnóstico](../profiling/media/prof-tour-enable-cpu-profiling.png "Ferramentas de Diagnóstico habilitar o uso da CPU")

Uma maneira de usar a ferramenta é definir dois pontos de interrupção no seu código, um no início e outro no final da função ou a região do código que você deseja analisar. Examine os dados de criação de perfil quando eles estiverem em pausa no segundo ponto de interrupção.

A exibição **Uso da CPU** mostra uma lista de funções ordenadas pela execução mais longa, com a função de execução mais longa na parte superior. Isso pode ajudar a levá-lo para as funções em que estão ocorrendo gargalos de desempenho.

![Ferramentas de Diagnóstico exibição de uso da CPU](../profiling/media/prof-tour-cpu-usage.png "Uso Ferramentas de Diagnóstico da CPU")

Clique duas vezes em uma função de interesse e você verá uma exibição "borboleta" de três painéis mais detalhada, com a função selecionada no centro da janela, a função de chamada à esquerda e as funções chamadas à direita. A seção **Corpo da função** também mostra o tempo total (e o percentual de tempo) gasto no corpo da função, excluindo o tempo gasto nas funções de chamada e nas funções chamadas. Esses dados podem ajudá-lo a avaliar se a própria função é um gargalo de desempenho.

![Ferramentas de Diagnóstico exibição do chamador chamado "borboleta"](../profiling/media/prof-tour-cpu-usage-caller-callee.png "Exibição de chamada do chamador Ferramentas de Diagnóstico Caller")

## <a name="analyze-memory-usage"></a>Analisar o uso de memória

A janela de **ferramentas de diagnóstico** também permite que você avalie o uso de memória em seu aplicativo usando a ferramenta de **uso de memória** . Por exemplo, é possível examinar o número e tamanho dos objetos no heap. Para obter instruções mais detalhadas para analisar a memória, confira [Analisar uso da memória](../profiling/memory-usage.md). Outra ferramenta de análise de memória, a [ferramenta de alocação de objeto .net](../profiling/dotnet-alloc-tool.md), ajuda a identificar padrões de alocação e anomalias em seu código .net.

Para analisar o uso de memória com o uso de memória integrada ao depurador também, você precisa pegar pelo menos um instantâneo de memória. Em geral, a melhor maneira de analisar a memória é usar dois instantâneos: o primeiro, logo antes de um problema de memória suspeito e o segundo instantâneo, logo após a ocorrência de um problema de memória suspeito. Depois, é possível exibir uma comparação dos dois instantâneos e ver exatamente o que mudou.

![Tirar um instantâneo no Ferramentas de Diagnóstico](../profiling/media/prof-tour-take-snapshots.gif "Ferramentas de Diagnóstico tirar instantâneos")

Quando você seleciona um dos links de seta, você recebe uma exibição diferencial do heap (um aumento de uso de ![memória](../profiling/media/prof-tour-mem-usage-up-arrow.png "Aumento de uso de memória") de seta para cima vermelho mostra uma contagem de objetos crescente (esquerda) ou um tamanho de heap crescente (direita)). Se você clicar no link à direita, terá uma exibição diferencial do heap, ordenada por objetos com maior aumento de tamanho de heap. Isso pode ajudá-lo a identificar problemas de memória. Por exemplo, na ilustração abaixo, os bytes usados por objetos `ClassHandlersStore` aumentaram em 3.492 bytes no segundo instantâneo.

![Exibição de comparação de Ferramentas de Diagnóstico heap](../profiling/media/prof-tour-mem-usage-diff-heap.png "Exibição de comparação de Ferramentas de Diagnóstico heap")

Se você clicar no link à esquerda, na exibição **Uso de Memória**, a exibição do heap será organizada pela contagem de objetos: os objetos de um tipo específico com maior aumento em número são mostrados na parte superior (classificados pela coluna **Comparação de Contagem**).

## <a name="profile-release-builds-without-the-debugger"></a><a name="post_mortem"></a>Compilações de versão de perfil sem o depurador

As ferramentas de criação de perfil como Uso da CPU e Uso da Memória podem ser usadas com o depurador (veja as seções anteriores) ou é possível executar ferramentas de criação de perfil post-mortem usando o Criador de Perfil de Desempenho, cuja função é fornecer análise para builds de **Versão**. No Criador de Perfil de Desempenho, é possível coletar informações de diagnóstico durante a execução do aplicativo e, em seguida, examinar as informações coletadas depois que o aplicativo é interrompido. Para obter mais informações sobre essas diferentes abordagens, confira [Executar ferramentas de criação de perfil com ou sem o depurador](../profiling/running-profiling-tools-with-or-without-the-debugger.md). Ferramentas adicionais, como a [ferramenta de alocação de objeto .net](../profiling/dotnet-alloc-tool.md) , também estão disponíveis no criador de perfil de desempenho.

![Criador de Perfil de Desempenho](../profiling/media/prof-tour-performance-profiler.png "Criador de Perfil de Desempenho")

Abra o criador de perfil de desempenho escolhendo **debug**  >  **Performance Profiler** (ou **ALT + F2**).

A janela permitirá que você selecione [várias ferramentas de criação de perfil](../profiling/use-multiple-profiler-tools-simultaneously.md) em alguns cenários. Ferramentas como Uso da CPU podem fornecer dados complementares que podem ser usados para ajudar na análise. Você também pode usar o [criador de perfil de linha de comando](../profiling/profile-apps-from-command-line.md) para habilitar cenários que envolvem várias ferramentas de criação de perfil.

## <a name="analyze-resource-consumption-xaml"></a>Analisar o consumo de recursos (XAML)

Em aplicativos XAML, como aplicativos WPF da área de trabalho do Windows e aplicativos UWP, é possível analisar o consumo de recursos usando a ferramenta Linha do Tempo do Aplicativo. Por exemplo, é possível analisar o tempo gasto pelo aplicativo para preparar quadros de interface do usuário (layout e renderização), atender a solicitações de rede e de disco e em cenários como inicialização do aplicativo, carregamento de página e redimensionamento do Windows. Para usar a ferramenta, escolha **Linha do Tempo do Aplicativo** no Criador de Perfil de Desempenho e, em seguida, escolha **Iniciar**. No aplicativo, percorra o cenário com um problema de consumo de recursos suspeito e escolha **Parar coleta** para gerar o relatório.

Taxas de quadros baixas no gráfico **Taxa de transferência visual** podem corresponder aos problemas visuais vistos ao executar o aplicativo. Da mesma forma, números elevados no gráfico **Utilização de thread de interface do usuário** também podem corresponder a problemas de capacidade de resposta da interface do usuário. No relatório, é possível selecionar um período com um problema de desempenho suspeito e, em seguida, examinar as atividades detalhadas de thread de interface do usuário na exibição Detalhes da linha do tempo (painel inferior).

![Ferramenta de criação de perfil Linha do Tempo do Aplicativo](../profiling/media/prof-tour-application-timeline.gif "Linha do Tempo do Aplicativo de Tour de criação de perfil")

Na exibição detalhes do cronograma, você pode encontrar informações como o tipo de atividade (ou o elemento de interface do usuário envolvido) junto com a duração da atividade. Por exemplo, na ilustração, um evento **Layout** de um controle Grade usa 57,53 ms.

Para obter mais informações, consulte [Linha do Tempo do Aplicativo](../profiling/application-timeline.md).

::: moniker range=">=vs-2019"

## <a name="examine-application-events"></a>Examinar eventos do aplicativo

O [Visualizador de eventos](../profiling/events-viewer.md) genéricos permite que você exiba a atividade do seu aplicativo por meio de uma lista de eventos, como carregamento de módulo, início de thread e configurações do sistema, para ajudar a diagnosticar melhor como seu aplicativo está sendo executado diretamente no criador de perfil do Visual Studio. Essa ferramenta está disponível no criador de perfil de desempenho. Abra o criador de perfil de desempenho escolhendo **debug**  >  **Performance Profiler** (ou **ALT + F2**).

A ferramenta mostra cada evento em uma exibição de lista. As colunas fornecem informações sobre cada evento, como o nome do evento, o carimbo de data/hora e a ID do processo.

![Rastreamento de Visualizador de Eventos](../profiling/media/eventviewertrace.png "Rastreamento de Visualizador de Eventos")

## <a name="analyze-asynchronous-code-net"></a>Analisar código assíncrono (.NET)

A [ferramenta Async do .net](../profiling/analyze-async.md) permite que você analise o desempenho do código assíncrono em seu aplicativo. Essa ferramenta está disponível no criador de perfil de desempenho. Abra o criador de perfil de desempenho escolhendo **debug**  >  **Performance Profiler** (ou **ALT + F2**).

A ferramenta mostra cada operação assíncrona em um modo de exibição de lista. Você pode ver informações como hora de início, hora de término e tempo total para uma operação assíncrona.

![Ferramenta Async do .NET interrompida](../profiling/media/async-tool-opened.png "Ferramenta Async do .NET interrompida")

## <a name="analyze-database-performance-net-core"></a>Analisar o desempenho do banco de dados (.NET Core)

Para aplicativos .NET Core que usam ADO.NET ou Entity Framework Core, a [ferramenta de banco de dados](../profiling/analyze-database.md) permite que você registre as consultas de banco de dados que seu aplicativo faz durante uma sessão de diagnóstico. Em seguida, você pode analisar informações sobre consultas individuais para encontrar locais onde o desempenho do aplicativo pode ser melhorado. Essa ferramenta está disponível no criador de perfil de desempenho. Abra o criador de perfil de desempenho escolhendo **debug**  >  **Performance Profiler** (ou **ALT + F2**).

A ferramenta mostra cada consulta em um modo de exibição de lista. Você pode ver informações como a hora de início e a duração da consulta.

![Alocação](./media/db-gotosource.png "Alocação")

::: moniker-end

## <a name="examine-ui-performance-and-accessibility-events-uwp"></a>Examinar os eventos de desempenho e de acessibilidade da interface do usuário (UWP)

Em seus aplicativos UWP, você pode habilitar a **análise da interface do usuário** na janela **ferramentas de diagnóstico** . A ferramenta pesquisa problemas comuns de desempenho ou de acessibilidade, mostrando-os na exibição **Eventos** durante a depuração. As descrições de eventos fornecem informações que podem ajudar a resolver problemas.

![Exibir eventos de análise de interface do usuário nas ferramentas de diagnóstico](../profiling/media/prof-tour-ui-analysis.png "Ferramentas de Diagnóstico exibir eventos de análise de interface do usuário")

## <a name="analyze-gpu-usage-direct3d"></a>Analisar o uso da GPU (Direct3D)

Em aplicativos Direct3D (os componentes Direct3D devem estar no C++), é possível examinar a atividade na GPU e analisar problemas de desempenho. Para obter mais informações, consulte [Uso da GPU](/visualstudio/debugger/graphics/gpu-usage). Para usar a ferramenta, escolha **Uso da GPU** no Criador de Perfil de Desempenho e, em seguida, escolha **Iniciar**. No aplicativo, percorra o cenário de interesse na criação de perfil e, em seguida, escolha **Parar coleta** para gerar um relatório.

Ao selecionar um período nos gráficos e escolher **Exibir detalhes**, uma exibição detalhada será exibida no painel inferior. Na exibição detalhada, é possível examinar as atividades que estão ocorrendo em cada CPU e GPU. Selecione eventos no painel inferior para obter pop-ups na linha do tempo. Por exemplo, selecione o eventos **Presente** para exibir pop-ups da chamada **Presente**. (As linhas verticais Vsync cinza-claras podem ser usadas como referência para entender se algumas chamadas **Presente** não têm Vsync. Deve haver uma chamada **Presente** entre cada dois Vsyncs para que o aplicativo atinja progressivamente 60 FPS.)

![Ferramenta de criação de perfil de uso de GPU](../profiling/media/prof-tour-gpu-usage.png "Uso de GPU de diagnóstico")

Também é possível usar os gráficos para determinar se há gargalos de desempenho limitados à CPU ou à GPU.

::: moniker range="vs-2017"
## <a name="analyze-performance-javascript-uwp"></a>Analisar o desempenho (JavaScript UWP)

Para aplicativos UWP, é possível usar a ferramenta Memória JavaScript e a ferramenta Capacidade de Resposta de IU em HTML.

A ferramenta Memória JavaScript é semelhante à ferramenta Uso de Memória disponível para outros tipos de aplicativos. É possível usar essa ferramenta para entender o uso de memória e encontrar perdas de memória no aplicativo. Para obter mais detalhes sobre a ferramenta, consulte [Memória JavaScript](../profiling/javascript-memory.md).

![Ferramenta de criação de perfil de memória JavaScript](../profiling/media/diagjsmemory.png "DiagJSMemory")

Para diagnosticar a capacidade de resposta de IU, tempo de carregamento lento e atualizações visuais lentas em aplicativos UWP, use a ferramenta Capacidade de Resposta de IU em HTML. O uso é semelhante à ferramenta Linha do Tempo do Aplicativo para outros tipos de aplicativos. Para obter mais informações, consulte [Capacidade de resposta de interface do usuário HTML](../profiling/html-ui-responsiveness.md).

![Ferramenta de criação de perfil de capacidade de resposta da interface do usuário HTML](../profiling/media/diaghtmlresp.png "DiagHTMLResp")
::: moniker-end

::: moniker range="vs-2017"
## <a name="analyze-network-usage-uwp"></a>Analisar o uso de rede (UWP)

Em aplicativos UWP, é possível analisar as operações de rede executadas usando a API `Windows.Web.Http`. Essa ferramenta pode ajudá-lo a resolver problemas, como problemas de acesso e autenticação, uso de cache incorreto e desempenho insatisfatório de exibição e download. Para usar a ferramenta, escolha **Rede** no Criador de Perfil de Desempenho e, em seguida, escolha **Iniciar**. No aplicativo, percorra o cenário que usa `Windows.Web.Http` e escolha **Parar coleta** para gerar o relatório.

![Ferramenta de criação de perfil de uso de rede](../profiling/media/prof-tour-network-usage.png "Uso de rede de diagnóstico")

Selecione uma operação na exibição de resumo para exibir mais detalhes.

![Informações detalhadas na ferramenta de uso de rede](../profiling/media/prof-tour-network-usage-details.png "Detalhes de uso da rede de diagnóstico")

Para obter mais informações, consulte [Uso de rede](../profiling/network-usage.md).
::: moniker-end

## <a name="analyze-performance-legacy-tools"></a>Analisar o desempenho (ferramentas herdadas)

::: moniker range="vs-2017"
Se você precisar de recursos, como instrumentação, que não estão atualmente presentes nas ferramentas Uso da CPU ou Uso de Memória, e estiver executando aplicativos de área de trabalho ou aplicativos ASP.NET, poderá usar o Gerenciador de Desempenho para a criação de perfil. (Sem suporte em aplicativos UWP). Para obter mais informações, consulte [Gerenciador de Desempenho](../profiling/performance-explorer.md).
::: moniker-end

::: moniker range=">=vs-2019"
No Visual Studio 2019, a Gerenciador de desempenho herdada e as ferramentas de criação de perfil relacionadas, como o assistente de desempenho, foram dobradas no criador **Debug**de perfil de desempenho, que você pode abrir usando o  >  **criador de perfis de desempenho**de depuração. No criador de perfil de desempenho, as ferramentas de diagnóstico disponíveis dependem do destino escolhido e do projeto de inicialização aberto atual. A ferramenta de uso da CPU fornece a funcionalidade de amostragem anteriormente suportada no assistente de desempenho. A ferramenta de instrumentação fornece a capacidade de criação de perfil instrumentada (para contagens e durações de chamada precisas) que estava no assistente de desempenho. As ferramentas de memória adicionais também aparecem no criador de perfil de desempenho.
::: moniker-end

![Ferramenta de Gerenciador de Desempenho](../profiling/media/prof-tour-performance-explorer.png "Performance Explorer")

## <a name="which-tool-should-i-use"></a>Qual ferramenta devo usar?

Eis aqui uma tabela que lista as diferentes ferramentas que o Visual Studio oferece e os diferentes tipos de projeto com os quais você poderá usá-las:

::: moniker range=">=vs-2019"
|Ferramenta de Desempenho|Área de trabalho do Windows|UWP|ASP.NET/ASP.NET Core|
|----------------------|---------------------|-------------|-------------|
|[PerfTips](../profiling/perftips.md)|sim|sim|sim|
|[Uso da CPU](../profiling/cpu-usage.md)|sim|sim|sim|
|[Uso de Memória](../profiling/memory-usage.md)|sim|sim|sim|
|[Alocação de objeto .NET](../profiling/dotnet-alloc-tool.md)|Sim (somente .NET)|sim|sim|
|[Uso de GPU](/visualstudio/debugger/graphics/gpu-usage)|sim|sim|não|
|[Linha do tempo do aplicativo](../profiling/application-timeline.md)|sim|sim|não|
|[Visualizador de eventos](../profiling/events-viewer.md)|sim|sim|sim|
|[.NET Async](../profiling/analyze-async.md)|Sim (somente .NET)|sim|sim|
|[Backup de banco de dados](../profiling/analyze-database.md)|Sim (somente no .NET Core)|não|Sim (somente ASP.NET Core)|
|[Performance Explorer](../profiling/performance-explorer.md)|não|não|não|
|[IntelliTrace](../debugger/intellitrace.md)|.NET com Visual Studio Enterprise somente|.NET com Visual Studio Enterprise somente|.NET com Visual Studio Enterprise somente|
::: moniker-end

::: moniker range="vs-2017"
|Ferramenta de Desempenho|Área de trabalho do Windows|UWP|ASP.NET/ASP.NET Core|
|----------------------|---------------------|-------------|-------------|
|[Uso da CPU](../profiling/cpu-usage.md)|sim|sim|sim|
|[Uso de Memória](../profiling/memory-usage.md)|sim|sim|sim|
|[Uso de GPU](/visualstudio/debugger/graphics/gpu-usage)|sim|sim|não|
|[Linha do tempo do aplicativo](../profiling/application-timeline.md)|sim|sim|não|
|[PerfTips](../profiling/perftips.md)|sim|sim para XAML, não para HTML|sim|
|[Performance Explorer](../profiling/performance-explorer.md)|sim|não|sim|
|[IntelliTrace](../debugger/intellitrace.md)|.NET com Visual Studio Enterprise somente|.NET com Visual Studio Enterprise somente|.NET com Visual Studio Enterprise somente|
|[Uso da rede](../profiling/network-usage.md)|não|sim|não|
|[Capacidade de resposta da interface do usuário HTML](../profiling/html-ui-responsiveness.md)|não|sim para HTML, não para XAML|não|
|[Memória JavaScript](../profiling/javascript-memory.md)|não|sim para HTML, não para XAML|não|
::: moniker-end


## <a name="see-also"></a>Veja também
- [Depurando no Visual Studio](../debugger/debugger-feature-tour.md)
