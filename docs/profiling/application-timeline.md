---
title: Analisar o consumo de recursos em aplicativos XAML
ms.custom: seodec18
ms.date: 11/01/2018
ms.topic: conceptual
ms.assetid: df7d854b-0a28-45a9-8a64-c015a4327701
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- uwp
ms.openlocfilehash: 0bb76de0d62ab504090d9ac1864ba7ee5627f69d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537274"
---
# <a name="analyze-resource-consumption-and-ui-thread-activity-xaml"></a>Analisar o consumo de recursos e a Atividade de Thread de Interface do Usuário (XAML)

Use o criador de perfil **Linha do Tempo de Aplicativo** para localizar e corrigir problemas de desempenho relacionados à interação com o aplicativo em aplicativos XAML. Essa ferramenta ajuda a melhorar o desempenho de aplicativos XAML mostrando uma exibição detalhada do consumo de recursos dos aplicativos. Você pode analisar o tempo gasto pelo seu aplicativo para preparar quadros de interface do usuário (layout e renderização), atender a solicitações de rede e de disco e em cenários como Inicialização de Aplicativo, Carregamento de Página e redimensionamento do Windows.

**Linha do Tempo do Aplicativo** é uma das ferramentas que você pode começar com o comando **Debug** > **Performance Profiler**.

Essa ferramenta substitui a ferramenta de **Capacidade de Resposta da Interface do Usuário XAML** que fazia parte do conjunto de ferramentas de diagnóstico para o Visual Studio 2013.

Você pode usar essa ferramenta nas seguintes plataformas:

- Aplicativos universais do Windows (no Windows 10)
- Windows 8.1
- Windows Presentation Foundation (.Net 4.0 e superiores)
- Windows 7

> [!NOTE]
> Você pode coletar e analisar os dados de uso da CPU e os dados de consumo de energia junto a dados da **ApplicationTimeline**. Consulte [Executar Ferramentas de Criação de Perfil com ou sem o depurador](../profiling/running-profiling-tools-with-or-without-the-debugger.md).

## <a name="collect-application-timeline-data"></a>Coletar dados da Linha do Tempo do Aplicativo

Você pode criar o perfil de capacidade de resposta de seu aplicativo em seu computador local, dispositivo conectado, emuladores ou simulador do Visual Studio ou em um dispositivo remoto. Consulte [Executar Ferramentas de Criação de Perfil com ou sem o depurador](../profiling/running-profiling-tools-with-or-without-the-debugger.md).

> [!TIP]
> Se possível, execute o aplicativo diretamente no dispositivo. O desempenho do aplicativo observado no simulador ou por uma conexão de área de trabalho remota pode não igual ao desempenho real no dispositivo. Por outro lado, a coleta de dados usando as Ferramentas Remotas do Visual Studio não afeta os dados de desempenho.

Veja a seguir as etapas básicas:

1. Abra seu aplicativo XAML.

2. Clique em **Depurar/Criador de Perfil de Desempenho**. Você deve ver uma lista de ferramentas de criação de perfil na janela .diagsession.

3. Selecione **Linha do tempo do aplicativo** e, em seguida, clique em **Iniciar** na parte inferior da janela.

   ![Ferramenta de Linha do Tempo do Aplicativo selecionada](../profiling/media/apptimelineselect.png "Ferramenta de Linha do Tempo do Aplicativo")

   > [!NOTE]
   > Talvez você veja uma janela Controle de Conta de Usuário solicitando sua permissão para executar *VsEtwCollector.exe*. Clique em **Sim**.

4. Execute o cenário cujo perfil você está interessado em criar em seu aplicativo para coletar dados de desempenho.

5. Para interromper a criação de perfil, volte para a janela .diagsession e clique em **Parar** na parte superior da janela.

   O Visual Studio analisa os dados coletados e exibe os resultados.

   ![Cronograma relatório do criador de perfil](../profiling/media/timeline_base.png "TIMELINE_Base")

## <a name="analyze-timeline-profiling-data"></a>Analisar dados de criação de perfil de linha do tempo

Depois de coletar os dados para a criação de perfil, você pode usar estas etapas para iniciar a análise:

1. Exiba as informações nos grafos **Utilização de thread de interface do usuário** e **Taxa de transferência visual (FPS)** e use as barras de navegação da linha do tempo para selecionar o intervalo de tempo que deseja analisar.

2. Usando as informações nos grafos **Utilização de thread de interface do usuário** ou **Taxa de transferência visual (FPS)**, examine os detalhes na exibição **Detalhes da linha do tempo** para localizar as possíveis causas de qualquer aparente falta de capacidade de resposta.

### <a name="report-scenarios-categories-and-events"></a><a name="BKMK_Report_scenarios_categories_and_events"></a> Cenários, categorias e eventos de relatório

A ferramenta **Linha do Tempo do Aplicativo** exibe dados de tempo para cenários, categorias e eventos relacionados ao desempenho de XAML.

### <a name="diagnostic-session-timeline"></a><a name="BKMK_Diagnostic_session_timeline"></a> Linha do tempo da sessão de diagnóstico

![Linha do tempo de desempenho e diagnóstico](../profiling/media/diaghub_timelinewithusermarks.png "DIAGHUB_TimelineWithUserMarks")

A régua na parte superior da página mostra a linha do tempo para informações com o perfil criado. Essa linha do tempo aplica-se ao gráfico **Utilização de thread de interface do usuário** e **Taxa de transferência visual**. Você pode restringir o escopo do relatório arrastando as barras de navegação na linha do tempo para selecionar um segmento da linha do tempo.

A linha do tempo também exibe todas as marcas de usuário inseridas e os eventos de ciclo de vida de ativação do aplicativo.

### <a name="ui-thread-utilization-graph"></a><a name="BKMK_UI_thread_utilization_graph"></a> Gráfico de utilização de thread da interface do usuário

![Gráfico de utilização da CPU](../profiling/media/timeline_cpuutilization.png "TIMELINE_CpuUtilization")

O gráfico **Utilização do thread da interface do usuário (%)** é um gráfico de barras que exibe a quantidade relativa de tempo gasto em uma categoria durante um período de coleta.

### <a name="visual-throughput-fps-graph"></a><a name="BKMK_Visual_throughput_FPS_graph"></a> Gráfico de taxa de transferência visual (FPS)

![Gráfico de taxa de transferência visual](../profiling/media/timeline_visualthroughput.png "TIMELINE_VisualThroughput")

O gráfico de linhas **Taxa de transferência visual (FPS)** mostra FPS (quadros por segundo) na interface do usuário e no thread de composição para o aplicativo.

### <a name="timeline-details"></a><a name="BKMK_Timeline_details_"></a> Detalhes da linha do tempo

A exibição de detalhes é o ponto em que você passa a maior parte do tempo analisando o relatório. Ela mostra o uso da CPU por seu aplicativo categorizado pelo subsistema de Estrutura da Interface do Usuário ou pelo componente do sistema que consumiu a CPU.

Há suporte para os seguintes eventos:

|Nome|Descrição|
|-|-|
|**Parsing**|Tempo gasto analisando arquivos XAML e criando objetos.<br /><br /> Expandir um nó de **Análise** em **Detalhes da linha do tempo** exibe a cadeia de dependências de todos os arquivos XAML analisados devido ao evento raiz. Essa dica permite identificar a criação de objeto e a análise de arquivos desnecessárias em cenários sensíveis a desempenho e otimizá-los.|
|**Layout**|Em aplicativos grandes, milhares de elementos podem ser mostrados na tela ao mesmo tempo. Essa exibição pode resultar em uma baixa taxa de quadros de interface do usuário e a capacidade de resposta do aplicativo correspondentemente baixa. O evento Layout determina com precisão o custo de estabelecer cada elemento (ou seja, o tempo gasto em Arrange, Measure, ApplyTemplate, ArrangeOverride e MeasureOverride). Ele também cria as árvores visuais que participaram de uma passagem de layout. É possível usar essa visualização para determinar quais árvores lógicas serão removidas ou para avaliar outros mecanismos de adiamento para otimizar sua passagem de layout.|
|**Render**|Tempo gasto desenhando elementos XAML na tela.|
|**I/0**|Tempo gasto na recuperação de dados do disco local ou de recursos de rede acessados por meio da [API WinINet (Microsoft Windows Internet)](/windows/desktop/WinInet/portal).|
|**Código do Aplicativo**|Tempo gasto executando código do aplicativo (usuário) que não está relacionado à análise ou ao layout.|
|**Xaml Other**|Tempo gasto executando o código XAML no runtime.|

> [!TIP]
> Escolha a ferramenta **Uso da CPU** junto com a ferramenta **Linha do Tempo do Aplicativo** ao começar a criar o perfil para exibir os métodos de aplicativo que são executados no thread da interface do usuário. Mover o código do aplicativo de execução longa em um thread em segundo plano pode melhorar a capacidade de resposta da interface do usuário.

#### <a name="customizing-timeline-details"></a><a name="BKMK_Customizing_Timeline_details_"></a> Personalizando os detalhes da Linha do Tempo

Use a barra de ferramentas **Detalhes da linha do tempo** para classificar, filtrar e especificar as anotações das entradas da exibição **Detalhes da linha do tempo**.

|Nome|Descrição|
|-|-|
|**Classificar por**|Classifique por hora de início ou o duração de eventos.|
|![Agrupar eventos por quadro](../profiling/media/timeline_groupbyframes.png "TIMELINE_GroupByFrames")|Adiciona ou remove a categoria de **Quadro** de nível superior que agrupa eventos por quadro.|
|![Filtrar lista de detalhes da linha do tempo](../profiling/media/timeline_filter.png "TIMELINE_Filter")|Filtra a lista pelas categorias selecionadas e a duração dos eventos.|
|![Personalizar informações de linha do tempo](../profiling/media/timeline_viewsettings.png "TIMELINE_ViewSettings")|Permite especificar as anotações para eventos.|

## <a name="see-also"></a>Confira também

- [Blog da equipe do WPF: nova ferramenta de análise de desempenho da interface do usuário para aplicativos do WPF](https://blogs.msdn.microsoft.com/wpf/2015/01/16/new-ui-performance-analysis-tool-for-wpf-applications/)
- [Melhores práticas de desempenho para aplicativos UWP em C++, C# e Visual Basic](/previous-versions/windows/apps/hh750313\(v\=win.10\))
- [Otimizar o desempenho do aplicativo WPF](/dotnet/framework/wpf/advanced/optimizing-wpf-application-performance)
- [Criação de perfis no Visual Studio](../profiling/index.yml)
- [Introdução às ferramentas de criação de perfil](../profiling/profiling-feature-tour.md)
