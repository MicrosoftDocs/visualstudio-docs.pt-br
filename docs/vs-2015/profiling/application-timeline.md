---
title: Linha do tempo do aplicativo | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: df7d854b-0a28-45a9-8a64-c015a4327701
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8d3a8edb0a2bf7809fc125812b5d541ba008547a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51751437"
---
# <a name="application-timeline"></a>Linha do Tempo do Aplicativo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Use o criador de perfil **Linha do Tempo de Aplicativo** para localizar e corrigir problemas de desempenho relacionados à interação com o aplicativo em aplicativos XAML. Essa ferramenta ajuda a melhorar o desempenho de aplicativos XAML fornecendo uma exibição detalhada do consumo de recursos dos aplicativos. Você pode analisar o tempo gasto pelo seu aplicativo para preparar quadros de interface do usuário (layout e renderização), atender a solicitações de rede e de disco e em cenários como Inicialização de Aplicativo, Carregamento de Página e redimensionamento do Windows.  
  
 **Linha do Tempo do Aplicativo** é uma das ferramentas que você pode começar com o comando **Debug / Performance Profiler...**.  
  
 Essa ferramenta substitui a ferramenta de **Capacidade de Resposta da Interface do Usuário XAML** que fazia parte do conjunto de ferramentas de diagnóstico para o Visual Studio 2013.  
  
 Você pode usar essa ferramenta nas seguintes plataformas:  
  
1.  Aplicativos universais do Windows (no Windows 10)  
  
2.  Windows Store 8.1  
  
3.  Windows Phone 8.1 (plataforma XAML Comum)  
  
4.  Windows Presentation Foundation (.Net 4.0 e superiores)  
  
5.  Windows 7  
  
> [!NOTE]
>  Você pode coletar e analisar os dados de uso da CPU e os dados de consumo de energia junto a dados da **ApplicationTimeline**. Consulte [executar ferramentas de criação de perfil sem depuração](http://msdn.microsoft.com/library/e97ce1a4-62d6-4b8e-a2f7-61576437ff01)  
  
##  <a name="BKMK_Collect_Timeline_data_for_your_app"></a> Coletar dados da Linha do Tempo do Aplicativo  
 Você pode criar o perfil de capacidade de resposta de seu aplicativo em seu computador local, dispositivo conectado, emuladores ou simulador do Visual Studio ou em um dispositivo remoto. Ver [executar ferramentas de criação de perfil sem depuração](http://msdn.microsoft.com/library/e97ce1a4-62d6-4b8e-a2f7-61576437ff01).  
  
> [!TIP]
>  Se possível, execute o aplicativo diretamente no dispositivo. O desempenho do aplicativo observado no simulador ou por uma conexão de área de trabalho remota pode não igual ao desempenho real no dispositivo. Por outro lado, a coleta de dados usando as Ferramentas Remotas do Visual Studio não afeta os dados de desempenho.  
  
 Veja a seguir as etapas básicas:  
  
1.  Abra seu aplicativo XAML.  
  
2.  Clique em **Depurar/Criador de Perfil de Desempenho...**. Você deve ver uma lista de ferramentas de criação de perfil na janela .diagsession.  
  
3.  Selecione **Linha do tempo do aplicativo** e, em seguida, clique em **Iniciar** na parte inferior da janela.  
  
    > [!NOTE]
    >  Você pode ver uma janela de Controle de Conta de Usuário solicitando sua permissão para executar VsEtwCollector.exe. Clique em **Sim**.  
  
4.  Execute o cenário cujo perfil você está interessado em criar em seu aplicativo para coletar dados de desempenho.  
  
5.  Para interromper a criação de perfil, volte para a janela .diagsession e clique em **Parar** na parte superior da janela.  
  
     O Visual Studio analisa os dados coletados e exibe os resultados.  
  
     ![Relatório do criador de perfil de linha do tempo](../profiling/media/timeline-base.png "TIMELINE_Base")  
  
##  <a name="BKMK_Analyze_Timeline_profiling_data"></a> Analisar dados de criação de perfil de linha do tempo  
 Depois de coletar os dados para a criação de perfil, você pode usar estas etapas para iniciar a análise:  
  
1.  Examine as informações nos gráficos **Utilização de thread de interface do usuário** e **Taxa de transferência visual (FPS)** e use as barras de navegação da linha do tempo para selecionar o intervalo de tempo que deseja analisar.  
  
2.  Usando as informações nos gráficos **Utilização de thread de interface do usuário** ou **Taxa de transferência visual (FPS)**, examine os detalhes na exibição **Detalhes da linha do tempo** para descobrir as possíveis causas de qualquer aparente falta de capacidade de resposta.  
  
###  <a name="BKMK_Report_scenarios_categories_and_events"></a> Cenários, categorias e eventos de relatório  
 A ferramenta **Linha do Tempo do Aplicativo** exibe dados de tempo para cenários, categorias e eventos relacionados ao desempenho de XAML.  
  
###  <a name="BKMK_Diagnostic_session_timeline"></a> Linha do tempo da sessão de diagnóstico  
 ![Linha do tempo de Desempenho e Diagnóstico](../profiling/media/diaghub-timelinewithusermarks.png "DIAGHUB_TimelineWithUserMarks")  
  
 A régua na parte superior da página mostra a linha do tempo para informações com o perfil criado. Essa linha do tempo aplica-se ao gráfico **Utilização de thread de interface do usuário** e **Taxa de transferência visual**. Você pode restringir o escopo do relatório arrastando as barras de navegação na linha do tempo para selecionar um segmento da linha do tempo.  
  
 A linha do tempo também exibe todas as marcas de usuário inseridas e os eventos de ciclo de vida de ativação do aplicativo.  
  
###  <a name="BKMK_UI_thread_utilization_graph"></a> Gráfico de utilização de thread da interface do usuário  
 ![Gráfico de utilização de CPU](../profiling/media/timeline-cpuutilization.png "TIMELINE_CpuUtilization")  
  
 O gráfico **Utilização do thread da interface do usuário (%)** é um gráfico de barras que exibe a quantidade relativa de tempo gasto em uma categoria durante um período de coleta.  
  
###  <a name="BKMK_Visual_throughput_FPS_graph"></a> Gráfico de taxa de transferência visual (FPS)  
 ![Gráfico de taxa de transferência Visual](../profiling/media/timeline-visualthroughput.png "TIMELINE_VisualThroughput")  
  
 O gráfico de linhas **Taxa de transferência visual (FPS)** mostra FPS (quadros por segundo) na interface do usuário e no thread de composição para o aplicativo.  
  
###  <a name="BKMK_Timeline_details_"></a> Detalhes da linha do tempo  
 A exibição de detalhes é o ponto em que você passará a maior parte do tempo analisando o relatório. Ele mostra uma exibição detalhada da utilização da CPU do seu aplicativo categorizada pelo subsistema de Estrutura da Interface do Usuário ou o componente do sistema que consumiu a CPU.  
  
 Há suporte para os seguintes eventos:  
  
|||  
|-|-|  
|**Parsing**|Tempo gasto analisando arquivos XAML e criando objetos.<br /><br /> Expandir um nó de **Análise** em **Detalhes da linha do tempo** exibe a cadeia de dependências de todos os arquivos XAML analisados como resultado do evento raiz. Isso permitirá identificar a criação de objeto e a análise de arquivos desnecessárias em cenários sensíveis a desempenho e otimizá-los.|  
|**Layout**|Em aplicativos grandes, milhares de elementos podem ser mostrados na tela ao mesmo tempo. Isso pode resultar em uma baixa taxa de quadros de interface do usuário e a capacidade de resposta do aplicativo correspondentemente baixa. O evento Layout determina com precisão o custo de estabelecer cada elemento (ou seja, o tempo gasto em Arrange, Measure, ApplyTemplate, ArrangeOverride e ArrangeOverride) e cria as árvores visuais que participaram de uma passagem do Layout. Você pode usar essa visualização para determinar quais das suas árvores lógicas precisam de remoção ou para avaliar outros mecanismos de adiamento para otimizar sua passagem de layout.|  
|**Render**|Tempo gasto desenhando elementos XAML na tela.|  
|**I/0**|Tempo gasto na recuperação de dados do disco local ou de recursos de rede acessados por meio da [API WinINet (Microsoft Windows Internet)](https://msdn.microsoft.com/library/windows/desktop/aa385331.aspx).|  
|**Código do Aplicativo**|Tempo gasto executando código do aplicativo (usuário) que não está relacionado a análise ou layout.|  
|**Xaml Other**|Tempo gasto executando o código XAML no tempo de execução.|  
  
> [!TIP]
>  Escolha a ferramenta **Uso da CPU** junto com a ferramenta **Linha do Tempo do Aplicativo** ao começar a criar o perfil para exibir os métodos de aplicativo que são executados no thread da interface do usuário. Mover o código do aplicativo de execução longa em um thread em segundo plano pode melhorar a capacidade de resposta da interface do usuário.  
  
####  <a name="BKMK_Customizing_Timeline_details_"></a> Personalizando os detalhes da Linha do Tempo  
 Use a barra de ferramentas **Detalhes da linha do tempo** para classificar, filtrar e especificar as anotações das entradas da exibição **Detalhes da linha do tempo**.  
  
|||  
|-|-|  
|**Classificar por**|Classifique por hora de início ou o duração de eventos.|  
|![Agrupar eventos por quadro](../profiling/media/timeline-groupbyframes.png "TIMELINE_GroupByFrames")|Adiciona ou remove a categoria de **Quadro** de nível superior que agrupa eventos por quadro.|  
|![Filtrar lista de detalhes da Linha do Tempo](../profiling/media/timeline-filter.png "TIMELINE_Filter")|Filtra a lista pelas categorias selecionadas e a duração dos eventos.|  
|![Personalizar informações detalhadas sobre a Linha do Tempo](../profiling/media/timeline-viewsettings.png "TIMELINE_ViewSettings")|Permite especificar as anotações para eventos.|  
  
## <a name="see-also"></a>Consulte também  
 [Blog da equipe WPF: Nova ferramenta de análise de desempenho da interface do usuário para aplicativos WPF](http://blogs.msdn.com/b/wpf/archive/2015/01/16/new-ui-performance-analysis-tool-for-wpf-applications.aspx)   
 [Práticas recomendadas de desempenho para aplicativos da Windows Store usando C++, C# e Visual Basic](http://msdn.microsoft.com/en-us/567bcefa-5da5-4e42-a4b8-1358c71adfa2)   
 [Otimizando o desempenho do aplicativo WPF](http://msdn.microsoft.com/library/ac8c6aa3-3c68-4a24-9827-3b6c829c1ebf)



