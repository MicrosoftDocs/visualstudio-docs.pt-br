---
title: Ferramentas de Criação de Perfil | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.diagnosticshub.overview
ms.assetid: 0fb6cd5d-e16a-4526-84a5-19e63c625bc5
caps.latest.revision: 26
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 380e98a8cd52fe77486dae245eee910a65a41057
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51782096"
---
# <a name="profiling-tools"></a>Ferramentas de Criação de Perfil
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Ferramentas de Diagnóstico e Criação de Perfil ajudam você a diagnosticar o uso de memória e uso de CPU e outros problemas em nível de aplicativo. Com essas ferramentas, você pode acumular dados (como valores de variáveis, chamadas de função e eventos) ao longo do tempo em que você executar o aplicativo no depurador. Você pode exibir o estado do seu aplicativo em pontos diferentes durante a execução do seu código.  
  
 Confira o resumo na parte inferior para ver quais ferramentas estão disponíveis para o tipo de projeto (por exemplo, área de trabalho, UWP, ASP.NET).  
  
 Você pode acessar as ferramentas de criação de perfil usando **depurar / Windows / Mostrar ferramentas de diagnóstico** usar as ferramentas durante a sessão de depuração, ou usando **depurar / desempenho Profiler...**  fazer uma análise de desempenho com foco.  Consulte [Executando ferramentas de criação de perfil com ou sem o depurador](../profiling/running-profiling-tools-with-or-without-the-debugger.md) para obter mais informações sobre as diferentes abordagens.  
  
 ![DebugDiagnosticsToolsMenu](../profiling/media/debugdiagnosticstoolsmenu.png "DebugDiagnosticsToolsMenu")  
  
 Consulte [O que há de novo nas ferramentas de criação de perfil](../profiling/what-s-new-in-profiling-tools.md) para saber mais sobre as novas funcionalidades desta versão.  
  
 As seções a seguir descrevem as diferentes ferramentas de desempenho que estão disponíveis no Visual Studio.  
  
## <a name="memory-usage"></a>Uso de Memória  
 ![DiagMemorySmall](../profiling/media/diagmemorysmall.png "DiagMemorySmall")  
  
 Localize vazamentos de memória e memória ineficiente enquanto você estiver depurando com a ferramenta **Uso da Memória**. A ferramenta permite que você tire instantâneos do heap de memória gerenciada e do heap de memória nativa. Você pode usar essa ferramenta com aplicativos ASP.NET, aplicativos universais do Windows e aplicativos da área de trabalho. A ferramenta **Uso da Memória** pode ser executada da janela **Ferramentas de Diagnóstico** enquanto você está depurando (**Depurar/Janelas/Mostrar Ferramentas de Diagnóstico**) ou fora do depurador (**Depurar/Criador de Perfil de Desempenho...**). Consulte [Uso da Memória](../profiling/memory-usage.md) e [Uso da Memória sem Depuração](http://msdn.microsoft.com/library/8883bc5f-df86-4f84-aa2b-a21150f499b0) para obter mais informações.  
  
## <a name="cpu-usage"></a>Uso da CPU  
 ![DiagCPUSmall](../profiling/media/diagcpusmall.png "DiagCPUSmall")  
  
 A ferramenta **Uso da CPU** mostra em que a CPU está dedicando tempo a executar código C++, C#/VB e JavaScript.  Você pode usar essa ferramenta com a área de trabalho e aplicativos universais do Windows, bem como aplicativos de serviços de aplicativo do Azure. A ferramenta **Uso de CPU** pode ser executada da janela **Ferramentas de Diagnóstico** enquanto você está depurando (**Depurar/Janelas/Mostrar Ferramentas de Diagnóstico**) ou fora do depurador (**Depurar/Criador de Perfil de Desempenho...**). Ver [uso da CPU](../profiling/cpu-usage.md) para obter mais informações.  
  
## <a name="performance-explorer"></a>Performance Explorer  
 ![PerfTools](../profiling/media/perftools.png "PerfTools")  
  
 O **Gerenciador de Desempenho** (**Depurar/Criador de Perfil/Gerenciador de Desempenho**) permite que você use várias ferramentas diferentes, incluindo **Amostragem de CPU**, **Instrumentação**, **Alocação de Memória .NET** e **Contenção de Recursos**. Você pode usar ferramentas do Gerenciador de Desempenho com aplicativos de área de trabalho e aplicativos ASP.NET, mas não com aplicativos universais do Windows. Para obter mais informações, consulte [Gerenciador de Desempenho](../profiling/performance-explorer.md).  
  
## <a name="gpu-usage"></a>Uso de GPU  
 ![DiagGPUUsage](../profiling/media/diaggpuusage.png "DiagGPUUsage")  
  
 Use a ferramenta [Uso de GPU](../debugger/gpu-usage.md) para compreender melhor a utilização do hardware de alto nível do aplicativo Direct3D. Você pode usar essa ferramenta com aplicativos universais do Windows e aplicativos da área de trabalho, mas não com aplicativos ASP.NET. A ferramenta **Uso de GPU** pode ser executada da janela **Ferramentas de Diagnóstico** enquanto você está depurando (**Depurar/Mostrar Ferramentas de Diagnóstico**) ou fora do depurador (**Depurar/Criador de Perfil de Desempenho...**).  
  
## <a name="application-timeline"></a>Linha do Tempo do Aplicativo  
 ![DiagAppTimeline](../profiling/media/diagapptimeline.png "DiagAppTimeline")  
  
 A ferramenta [Linha do Tempo do Aplicativo](../profiling/application-timeline.md) ajuda a melhorar o desempenho de aplicativos XAML fornecendo uma exibição detalhada do consumo de recursos por esses aplicativos. Você pode usar a **Linha do Tempo do Aplicativo** com aplicativos universais do Windows e aplicativos da área de trabalho, mas não com aplicativos ASP.NET. A ferramenta **Linha do Tempo do Aplicativo** pode ser executada da janela **Ferramentas de Diagnóstico** (**Depurar/Criador de Perfil de Desempenho...**).  
  
## <a name="perftips"></a>PerfTips  
 ![DiagPerfTips](../profiling/media/diagperftips.png "DiagPerfTips")  
  
 Quando o depurador interrompe a execução em um ponto de interrupção ou operação passo a passo, o tempo decorrido entre a interrupção e o ponto de interrupção anterior aparece como uma dica na janela do editor. Essas [PerfTips](../profiling/perftips.md) ajudam você a monitorar e analisar o desempenho de seu aplicativo enquanto você está depurando. Você pode ver **PerfTips** em aplicativos da área de trabalho, universais do Windows e ASP.NET.  
  
## <a name="javascript-memory"></a>Memória JavaScript  
 ![DiagJSMemory](../profiling/media/diagjsmemory.png "DiagJSMemory")  
  
 A ferramenta [Memória JavaScript](../profiling/javascript-memory.md) lhe permite medir, avaliar e direcionar problemas relacionados ao desempenho no seu código por meio da coleta de informações de tempo na entrada e saída de cada função em seu aplicativo. Você pode usar essa ferramenta com aplicativos HTML universais do Windows. A ferramenta **Temporização de Função JavaScript** pode ser executada da janela **Ferramentas de Diagnóstico** (**Depurar/Criador de Perfil de Desempenho...**).  
  
## <a name="html-ui-responsiveness"></a>Capacidade de Resposta da Interface de Usuário HTML  
 ![DiagHTMLResp](../profiling/media/diaghtmlresp.png "DiagHTMLResp")  
  
 A ferramenta [Capacidade de resposta da interface do usuário HTML](../profiling/html-ui-responsiveness.md) ajuda você a isolar problemas de desempenho em seus aplicativos, incluindo a falta de capacidade de resposta, tempo de carregamento lento e atualizações visuais que são menos frequentes do que o esperado. Você pode usar essa ferramenta com aplicativos HTML universais do Windows. A **Capacidade de resposta da interface do usuário HTML** pode ser executada da janela **Ferramentas de Diagnóstico** (**Depurar/Criador de Perfil de Desempenho...**).  
  
## <a name="intellitrace"></a>IntelliTrace  
 ![DiagIntelliTrace](../profiling/media/diagintellitrace.png "DiagIntelliTrace")  
  
 O [IntelliTrace](../debugger/intellitrace.md) lhe permite registrar eventos específicos, examinar os dados na janela **Locais** durante eventos do depurador e chamadas de função e depurar erros difíceis de reproduzir.  O IntelliTrace é principalmente uma ferramenta de depuração, mas ela também fornece informações que podem ser usadas para investigações de desempenho. Você pode usar essa ferramenta no Visual Studio Enterprise somente com aplicativos de área de trabalho, aplicativos universais do Windows e C# ASP.NET. Você pode encontrar o IntelliTrace na janela **Ferramentas de Diagnóstico** enquanto você está depurando (**Depurar/Janelas/Mostrar Ferramentas de Diagnóstico**).  
  
## <a name="profiling-in-production"></a>Criação de perfil na produção  
 A abordagem recomendada para criação de perfil na produção é criar o perfil por meio da [linha de comando usando vsperf.exe](../profiling/using-the-profiling-tools-from-the-command-line.md) para coletar um perfil de CPU. Para suporte à criação de perfil remota no Serviço de Aplicativo do Azure, crie o perfil por meio do [Gerenciador de Servidores ou do Portal Kudu](https://azure.microsoft.com/en-us/blog/remote-profiling-support-in-azure-app-service/).  
  
## <a name="which-tool-should-i-use"></a>Qual ferramenta devo usar?  
 Eis aqui uma tabela que lista as diferentes ferramentas que o Visual Studio oferece e os diferentes tipos de projeto com os quais você poderá usá-las:  
  
|Ferramenta de Desempenho|Área de Trabalho do Windows|Windows Universal/Store|ASP.NET|  
|----------------------|---------------------|------------------------------|-------------|  
|[Uso de Memória](../profiling/memory-usage.md)|sim|sim|no|  
|[Uso da CPU](../profiling/cpu-usage.md)|sim|sim|Somente o serviço de aplicativo do Azure|  
|[Uso de GPU](../debugger/gpu-usage.md)|sim|sim|no|  
|[Linha do tempo do aplicativo](../profiling/application-timeline.md)|sim|sim|no|  
|[PerfTips](../profiling/perftips.md)|sim|sim para XAML, não para HTML|no|  
|[Gerenciador de Desempenho](../profiling/performance-explorer.md)|sim|no|sim|  
|[IntelliTrace](../debugger/intellitrace.md)|Somente .NET Enterprise|Somente .NET Enterprise|Somente .NET Enterprise|  
|[Capacidade de Resposta de interface do usuário em HTML](../profiling/html-ui-responsiveness.md)|no|sim para HTML, não para XAML|no|  
|[Memória JavaScript](../profiling/javascript-memory.md)|no|sim para HTML, não para XAML|no|  
  
## <a name="see-also"></a>Consulte também  
 [Visual Studio IDE](../ide/visual-studio-ide.md)



