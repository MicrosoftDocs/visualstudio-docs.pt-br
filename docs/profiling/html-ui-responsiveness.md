---
title: Analisar a capacidade de resposta de interface do usuário HTML em aplicativos UWP | Microsoft Docs
ms.custom: H1Hack27Feb2017
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- JavaScript
helpviewer_keywords:
- performance, JavaScript [UWP apps]
- performance tools, JavaScript [UWP apps]
- UI Responsiveness Profiler [JavaScript]
- profiler, UI responsiveness [JavaScript]
- profiler, JavaScript [UWP apps]
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- uwp
ms.openlocfilehash: ec3f3be069e92d52071a6b40857f7fac46e8d3e5
ms.sourcegitcommit: bccb05b5b4e435f3c1f7c36ba342e7d4031eb398
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51221042"
---
# <a name="analyze-html-ui-responsiveness-in-universal-windows-apps"></a>Analisar a capacidade de resposta de interface do usuário HTML em Aplicativos Universais do Windows
Este tópico descreve como isolar problemas de desempenho nos aplicativos usando o Criador de Perfil de Capacidade de Resposta da Interface do Usuário, uma ferramenta de desempenho disponível para Aplicativos Universais do Windows.  
  
 O Criador de Perfil de Capacidade de Resposta da Interface de Usuário pode ajudá-lo a isolar problemas com a capacidade de resposta da Interface de Usuário ou com efeitos colaterais da plataforma, que normalmente ocorrem com estes sintomas:  
  
-   Ausência de resposta da interface de usuário. O aplicativo pode demorar a responder se o thread de interface de usuário estiver bloqueado. Algumas coisas que podem bloquear o thread de interface de usuário incluem código JavaScript síncrono, o layout CSS excessivo ou o trabalho de cálculo CSS, solicitações XHR síncronas, coleta de lixo, horas de pintura excessivas ou código JavaScript de processamento intenso.  
  
-   Tempo de carregamento lento do aplicativo ou de uma página. Isso é geralmente causado pelo tempo excessivo gasto no carregamento de recursos.  
  
-   Atualizações visuais que são menos frequentes do que o esperado. Isso ocorrerá se o thread de interface de usuário estiver muito ocupado para manter uma taxa de quadros estável. Por exemplo, se o thread de interface de usuário estiver ocupado, os quadros poderão ser ignorados. Qualquer trabalho do thread sem interface de usuário, como solicitações de rede, decodificação de imagens e pinturas, também pode limitar a frequência de atualizações visuais. (Nem toda pintura é executada no thread de interface de usuário.)  
  
## <a name="run-the-html-ui-responsiveness-tool"></a>Executar a ferramenta de Capacidade de Resposta da Interface do Usuário HTML  
 Use a ferramenta de Capacidade de Resposta de IU em HTML quando tiver um aplicativo UWP de trabalho aberto no Visual Studio.  
  
1.  Se você estiver executando o aplicativo no Visual Studio, na barra de ferramentas **Padrão**, na lista **Iniciar Depuração**, escolha um destino de implantação como **Máquina Local** ou **Dispositivo**.  
  
2.  No menu **Depurar**, escolha **Criador de Perfil de Desempenho**.  
  
     Se você quiser alterar o destino da análise do criador de perfil, escolha **Alterar Destino**.  
  
     ![Alterar destino de análise](../profiling/media/js_tools_target.png "JS_Tools_Target")  
  
     As seguintes opções estão disponíveis para o destino de análise:  
  
    -   **Projeto de Inicialização**. Selecione esta opção para analisar o projeto de inicialização atual. Se você estiver executando o aplicativo em um computador ou dispositivo remoto, use essa configuração, que é o valor padrão.  
  
    -   **Aplicativo em Execução**. Escolha esta opção para selecionar o aplicativo UWP em uma lista de aplicativos em execução. Não é possível usar esta opção ao executar o aplicativo em um computador ou dispositivo remoto.  
  
         Você pode usar esta opção para analisar o desempenho de aplicativos que estão em execução no seu computador quando você não tiver acesso ao código-fonte.  
  
    -   **Aplicativo Instalado**. Escolha esta opção para selecionar um aplicativo instalado que você deseje analisar. Não é possível usar esta opção ao executar o aplicativo em um computador ou dispositivo remoto.  
  
         Você pode usar esta opção para analisar o desempenho de aplicativos instalados no seu computador quando você não tiver acesso ao código-fonte. Esta opção também pode ser útil quando você desejar apenas analisar o desempenho de qualquer aplicativo fora do seu próprio desenvolvimento de aplicativos.  
  
3.  Em **Ferramentas Disponíveis**, selecione **Capacidade de Resposta da Interface do Usuário HTML** e clique em **Iniciar**.  
  
4.  Quando você inicia o Criador de Perfis de Capacidade de Resposta de Interface de Usuário, a janela de Controle de Conta de Usuário pode solicitar sua permissão para executar o Visual Studio ETW Collector.exe. Escolha **Sim**.  
  
     Interaja com o aplicativo para testar o cenário de desempenho relevante. Para um fluxo de trabalho detalhado, consulte [Isolar um problema de capacidade de resposta da interface do usuário](#Workflow) e [Isolar um problema de taxa de transferência visual](#IsolateVisualThroughput).  
  
5.  Alterne para o Visual Studio pressionando Alt+Tab.  
  
6.  Para interromper a criação de perfil do aplicativo e exibir os dados coletados pelo criador de perfil, selecione **Parar de coletar**.  
  
## <a name="isolate-an-issue"></a>Isolar um problema  
 A seção a seguir fornece sugestões para ajudá-lo a isolar problemas de desempenho. Para obter uma explicação passo a passo sobre como identificar e corrigir problemas de desempenho por meio de um aplicativo de teste de desempenho de amostra, consulte [Passo a passo: melhorando a capacidade de resposta da interface do usuário (HTML)](../profiling/walkthrough-improving-ui-responsiveness-html.md).  
  
###  <a name="Workflow"></a> Isolar um problema de capacidade de resposta da interface do usuário  
 Estas etapas fornecem um fluxo de trabalho sugerido que pode ajudá-lo a usar o Criador de Perfis de Capacidade de Resposta de Interface de Usuário de forma mais eficaz:  
  
1.  Abra o aplicativo no Visual Studio.  
  
2.  Teste seu aplicativo quanto a problemas de capacidade de resposta da interface de usuário. (Pressione **Ctrl**+**F5** para iniciar o aplicativo sem depuração.)  
  
     Se você encontrar um problema, continue testando para limitar o período em que ocorre o problema ou tente identificar gatilhos que provocam esse comportamento.  
  
3.  Volte para o Visual Studio (pressione **Alt**+**Tab**) e interrompa o aplicativo (**Shift**+**F5**).  
  
4.  Opcionalmente, adicione marcas de usuário ao seu código usando [Marcar código para análise](#ProfileMark).  
  
    > [!TIP]
    >  As marcas de usuário podem ajudá-lo a identificar o problema de capacidade de resposta durante a exibição de dados do criador de perfil visual. Por exemplo, você pode incluir uma marca de usuário no início e no fim de uma seção de código que está causando um problema de capacidade de resposta.  
  
5.  Execute o Criador de Perfil de Capacidade de Resposta da Interface de Usuário seguindo as instruções na seção anterior.  
  
6.  Coloque o aplicativo no estado que resulta em um problema de capacidade de resposta da interface do usuário.  
  
7.  Mude para o Visual Studio (pressione Alt+Tab) e selecione **Parar de coletar** na guia do criador de perfil do Criador de Perfil de Capacidade de Resposta da Interface do Usuário.  
  
8.  Se você tiver adicionado marcas de usuário, elas aparecerão na opção [Exibir a linha do tempo da sessão de diagnóstico](#Ruler) do criador de perfil. A ilustração a seguir mostra uma única marca de usuário usada para especificar uma operação específica em seu código.  
  
     ![Régua de diagnóstico mostrando uma marca de usuário](../profiling/media/js_htmlvizprofiler_usermark.png "JS_HTMLVizProfiler_UserMark")  
  
9. Identifique uma área de interesse na linha de tempo e nos gráficos do criador de perfil usando marcas de usuário, eventos de ciclo de vida do aplicativo ou dados visíveis nos gráficos. Veja a seguir algumas diretrizes para ajudá-lo a analisar e usar os dados dos gráficos:  
  
    -   Use a opção [Exibir a linha do tempo da sessão de diagnóstico](#Ruler) para exibir [Marcar código para análise](#ProfileMark), eventos de ciclo de vida do aplicativo, a linha do tempo associada a esses eventos e a linha do tempo para dados nos outros gráficos.  
  
    -   Use o [Gráfico da utilização da CPU](#CPUUtilization) para exibir informações gerais sobre a atividade da CPU e o tipo de trabalho com o qual ela está lidando durante um determinado período de tempo. Períodos de atividade excessiva da CPU têm maior probabilidade de causar problemas de capacidade de resposta e quadros ignorados.  
  
    -   Se você estiver desenvolvendo um jogo ou um aplicativo de mídia avançado, use a opção [Exibir representação visual da taxa de transferência (FPS)](#VisualThroughput) para identificar períodos nos quais a taxa de quadros caiu.  
  
10. Selecione a área de interesse em um dos gráficos clicando em uma parte e arrastando o ponteiro para fazer uma seleção (ou usando a tecla Tab e as teclas de seta). Quando você seleciona um período fazendo uma seleção, o gráfico de detalhes da linha do tempo no painel inferior do criador de perfis muda para mostrar somente o período selecionado.  
  
     A ilustração a seguir mostra o gráfico de utilização da CPU com uma área de interesse realçada.  
  
     ![Gráfico de utilização de CPU](../profiling/media/js_htmlvizprof_cpu_util.png "JS_HTMLVizProf_CPU_Util")  
  
11. Use a opção [Exibir detalhes da linha de tempo](#TimelineDetails) para obter informações detalhadas sobre os eventos que são realizados com muita frequência ou demorando muito tempo para terminar. Por exemplo, procure o seguinte:  
  
    -   Ouvintes de eventos, temporizadores e retornos de chamada de quadro de animação. Dependendo do evento específico, os dados fornecidos podem incluir a ID dos elementos DOM modificados, o nome das propriedades CSS modificadas, um link para o local de origem e o nome do evento associado ou a função callback.  
  
    -   Eventos de layout ou de script que resultaram em elementos de renderização, como chamadas a `window.getComputedStyles`. O elemento DOM associado para o evento é fornecido.  
  
    -   Páginas ou recursos de URL que são carregados pelo aplicativo, como avaliações de script para eventos de análise de HTML. É fornecido o nome do arquivo ou do recurso.  
  
    -   Outros eventos especificados em [Referência do criador de perfil](#profiler-event-reference).  
  
    > [!TIP]
    >  A maioria das informações úteis do criador de perfil aparece no gráfico de detalhes da linha do tempo.  
  
12. Com uma área selecionada no gráfico de utilização da CPU ou de taxa de transferência visual (FPS), escolha **Ampliar** (o botão ou o menu de contexto) para obter informações mais detalhadas. A linha do tempo do gráfico muda para mostrar somente o período selecionado.  
  
13. Depois de ampliar, selecione uma parte da utilização da CPU ou do gráfico Taxa de Transferência Visual. Quando você faz uma seleção, o gráfico de detalhes da linha do tempo no painel inferior do criador de perfis muda para mostrar somente o período selecionado.  
  
###  <a name="IsolateVisualThroughput"></a> Isolar um problema de taxa de transferência visual  
 Períodos de utilização excessiva da CPU podem resultar em taxas de quadros baixas ou inconsistentes. Se você desenvolve jogos e aplicativos de mídia avançados, o gráfico de taxa de transferência visual pode fornecer dados mais importantes do que o gráfico de utilização da CPU.  
  
 Para isolar um problema de taxa de transferência visual, siga as etapas descritas na seção anterior, mas use o gráfico de taxa de transferência visual como um dos pontos de dados chave.  
  
###  <a name="ProfileMark"></a> Marcar código para análise  
 Para ajudar a isolar uma seção do código de aplicativo associada aos dados que aparecem nos gráficos, você pode adicionar uma chamada de função ao aplicativo para instruir o criador de perfil a inserir uma marca de perfil — um triângulo invertido — na linha do tempo no momento em que a função for executada. Qualquer marca de usuário que você adicione aparecerá na linha do tempo para o gráfico de utilização da CPU, o gráfico de taxa de transferência visual e o gráfico de detalhes da linha do tempo.  
  
 Para adicionar uma marca de usuário, adicione o seguinte código ao aplicativo. Este exemplo usa “obtendo dados” como a descrição do evento.  
  
```javascript  
if (performance && performance.mark) {  
    performance.mark("getting data");  
}  
  
```  
  
 A descrição do evento aparece como uma dica de ferramenta quando você posiciona o ponteiro do mouse sobre a marca de usuário. Você pode adicionar quantas marcas de usuário forem necessárias.  
  
> [!NOTE]
>  `console.timeStamp`, um comando do Chrome, também é mostrado como uma marca de usuário.  
  
 A ilustração a seguir mostra a régua de diagnóstico com uma única marca de usuário e sua dica de ferramenta.  
  
 ![Régua de diagnóstico mostrando uma marca de usuário](../profiling/media/js_htmlvizprofiler_usermark.png "JS_HTMLVizProfiler_UserMark")  
  
 Você também pode criar eventos gerados por ferramenta na exibição dos detalhes da linha do tempo para ver quanto tempo se passa entre duas marcas de usuário. O código a seguir adiciona uma segunda marca de usuário e uma medida do tempo decorrido entre a execução de duas marcas de usuário (o código anterior mostra a primeira marca de usuário).  
  
```javascript  
if (performance.mark && performance.measure) {  
    performance.mark("data retrieved");  
    performance.measure("data measure", "getting data", "data retrieved");  
}  
```  
  
 Se a segunda marca de usuário não for especificada, o `performance.measure` usa um carimbo de data/hora como segunda marca de usuário. A primeira marca de usuário é obrigatória.  
  
 A medição da duração aparece como um evento de **Medida do usuário** na exibição de detalhes da linha do tempo e mostra informações detalhadas quando selecionada.  
  
 ![Evento de medida do usuário na exibição de detalhes da linha do tempo](../profiling/media/js_htmlvizprofiler_user_measure.png "JS_HTMLVizProfiler_User_Measure")  
  
## <a name="analyze-data"></a>Analisar dados  
 As seções a seguir fornecem informações para ajudar a interpretar os dados que aparecem no criador de perfil.  
  
###  <a name="Ruler"></a> Exibir a linha do tempo da sessão de diagnóstico  
 A régua na parte superior do criador de perfil mostra a linha do tempo para informações analisadas. Essa linha do tempo se aplica tanto para o gráfico de utilização da CPU quanto para o gráfico de taxa de transferência visual.  
  
 Esta é a aparência da sessão de diagnóstico com uma dica de ferramenta exibida para vários eventos de ciclo de vida do aplicativo:  
  
 ![Régua da sessão de diagnóstico](../profiling/media/js_htmlvizprof_ruler.png "JS_HTMLVizProf_Ruler")  
  
 A linha do tempo mostra quando ocorrem os eventos de ciclo de vida do aplicativo, como o evento de ativação, e mostra marcas de usuário (triângulos com a marca de usuário) que você pode adicionar ao seu código. Você pode selecionar os eventos para mostrar dicas de ferramenta com mais informações. Para obter mais informações sobre as marcas de usuário, consulte [Marcar código para análise](#ProfileMark) neste tópico.  
  
 Eventos de ciclo de vida do aplicativo aparecem como símbolos de diamante. Esses são os eventos DOM, que incluem o seguinte:  
  
-   Os eventos `DOMContentLoaded` e `Load`, que normalmente ocorrem no manipulador de eventos ativado no seu código. Uma dica de ferramenta para o evento mostra o evento e a URL especificados.  
  
-   Um evento de navegação, que ocorre quando você navega para outra página. Uma dica de ferramenta para o evento mostra a URL da página de destino.  
  
###  <a name="CPUUtilization"></a> Exibir a utilização da CPU  
 O gráfico de utilização da CPU permite identificar períodos em que há uma atividade excessiva da CPU. Ele fornece informações sobre o consumo médio do aplicativo na CPU durante um período. As informações são codificadas por cores para representar as seguintes categorias específicas: **Carregamento**, **Script**, **coleta de lixo (GC)**, **Estilo**, **Renderização** e **Decodificação de imagem**. Para obter mais informações sobre essas categorias, consulte [Referência de eventos do criador de perfil](#profiler-event-reference) mais adiante, neste tópico.  
  
 O gráfico da utilização da CPU mostra a quantidade de tempo gasto em todos os threads de aplicativo, combinando valores de utilização da CPU para uma ou mais CPUs em um único valor de porcentagem. O valor da utilização da CPU poderá exceder 100 por cento quando mais de uma CPU estiver sendo usada.  
  
> [!NOTE]
>  A utilização da CPU não aparece no gráfico.  
  
 Este exemplo mostra a aparência do gráfico da utilização da CPU:  
  
 ![Gráfico de utilização de CPU](../profiling/media/js_htmlvizprof_cpu_util.png "JS_HTMLVizProf_CPU_Util")  
  
 Use este gráfico para:  
  
- Identificar áreas de interesse geral.  
  
- Escolha um período específico a ser exibido no gráfico de detalhes da linha do tempo. Para escolher um período, selecione em uma parte do gráfico e arraste o ponteiro para fazer uma seleção.  
  
- Obtenha uma exibição mais detalhada de um período selecionado clicando no botão **Ampliar**.  
  
  Para obter mais informações sobre como usar o grafo , consulte [Isolar um problema de capacidade de resposta da interface do usuário](#Workflow) neste tópico.  
  
###  <a name="VisualThroughput"></a> Exibir a taxa de transferência visual (FPS)  
 O gráfico de taxa de transferência visual permite que você identifique períodos em que a taxa de quadros cai. Ele mostra os quadros por segundo (FPS) para o aplicativo. Este gráfico é mais útil para o desenvolvimento de jogos e de aplicativos de mídia avançados.  
  
 O valor de FPS exibido pode diferir da taxa de quadros real. Tenha estas informações em mente quando for examinar dados nesse gráfico:  
  
- O gráfico mostra o FPS que o aplicativo é capaz de atingir em qualquer tempo específico. Quando o aplicativo estiver ocioso, a taxa de FPS será a mesma que a taxa de atualização do monitor.  
  
- O gráfico a seguir mostra a taxa de FPS real se o aplicativo estiver executando um trabalho que exija atualizações visuais.  
  
- O gráfico a seguir mostrará o valor zero se os quadros forem ignorados.  
  
  Este exemplo mostra a aparência do gráfico Taxa de Transferência Visual:  
  
  ![Gráfico de taxa de transferência Visual](../profiling/media/js_htmlvizprof_vizthru.png "JS_HTMLVizProf_VizThru")  
  
  Use o gráfico Taxa de Transferência Visual para:  
  
- Identificar áreas de interesse geral.  
  
- Escolha um período específico a ser exibido no gráfico de detalhes da linha do tempo. Para escolher um período, selecione em uma parte do gráfico e arraste o ponteiro para fazer uma seleção.  
  
- Obtenha uma exibição mais detalhada de um período selecionado clicando no botão **Ampliar**.  
  
###  <a name="TimelineDetails"></a> Exibir detalhes da linha de tempo  
 O gráfico de detalhes da linha do tempo aparece no painel inferior do Criador de Perfil de Capacidade de Resposta da Interface de Usuário. Ele fornece informações sequenciais e hierárquicas sobre eventos que consumiram a maioria do tempo da CPU durante períodos selecionados. Esse grafo pode ajudá-lo a determinar o que disparou um evento específico e, em alguns casos, como o evento é remapeado para o código-fonte. Esse gráfico também ajuda a determinar o tempo necessário para pintar atualizações visuais na tela.  
  
 O gráfico mostra o trabalho de threads de interface de usuário e trabalha em threads de plano de fundo que podem contribuir para a lentidão das atualizações visuais. O gráfico não mostra o trabalho JavaScript JIT, o trabalho de GPU assíncrono, o trabalho executado fora do processo do host (como o trabalho RuntimeBroker.exe e dwm.exe) ou o trabalho para as áreas do Windows Runtime que não foram instrumentadas para criação de perfil (como o E/S de disco).  
  
> [!TIP]
>  Quando ocorre um evento em um thread de plano de fundo, a ID do thread aparece entre colchetes ao lado do nome do evento.  
  
 Este exemplo mostra a aparência do gráfico de detalhes da linha do tempo quando o ouvinte de eventos para um evento de clique DOM é selecionado:  
  
 ![Gráfico de detalhes da linha do tempo](../profiling/media/js_htmlvizprof_timelinedet.png "JS_HTMLVizProf_TimelineDet")  
  
 Nesta ilustração, o manipulador de eventos **spinAction** na coluna **Nome do evento** é um link que, quando selecionado, levará você ao manipulador de eventos no código-fonte. No painel direito, a propriedade **Callback function** fornece o mesmo link ao código-fonte. Outras propriedades também fornecem informações sobre o evento, como o elemento DOM associado.  
  
 Se você selecionar uma parte da linha do tempo para o gráfico de utilização da CPU e de taxa de transferência visual (FPS), o gráfico de detalhes da linha do tempo mostrará as informações detalhadas para o período selecionado.  
  
 Os eventos no gráfico de detalhes da linha do tempo são codificados por cores para representar as mesmas categorias de trabalho mostradas no gráfico de utilização da CPU. Para obter mais informações sobre as categorias de evento e eventos específicos, consulte [Referência de eventos do criador de perfil](#profiler-event-reference) neste tópico.  
  
 Use o gráfico de detalhes da linha do tempo para:  
  
-   Exibir a hora de início, a duração, e a hora de término aproximadas para um evento no modo de exibição de linha do tempo e de grade. O gráfico dos detalhes da linha do tempo pode mostrar períodos que variam de 30 milissegundos a 30 segundos no modo de exibição de grade, dependendo do estado do zoom. Para valores de duração:  
  
    -   Os tempos inclusivos representam a duração do evento incluindo os filhos do evento. No modo de exibição de grade, esse valor aparece primeiro.  
  
    -   Os tempos exclusivos representam a duração do evento não incluindo os filhos do evento. No modo de exibição de grade, esse valor aparece entre parênteses.  
  
-   Expanda um evento na hierarquia para exibir os filhos do evento. Os filhos do evento são outros eventos que são gerados pelo evento pai. Por exemplo, um evento DOM pode ter ouvintes de evento que aparecem como filhos. Um ouvinte de eventos pode ter outros eventos resultantes dele, como um evento de layout.  
  
-   Classifique os eventos por hora de início (o padrão) ou duração. Use a lista **Classificar por** para selecionar um método de classificação.  
  
-   Veja detalhes para cada evento no painel de detalhes (painel direito). As propriedades variam de acordo com o evento específico, como mostram os exemplos a seguir:  
  
    -   Para temporizadores, ouvintes de evento (eventos DOM) e retornos de chamada do quadro de animação, a propriedade **Callback function** fornece um link para o local do código-fonte juntamente com o nome do manipulador de eventos ou função de retorno de chamada.  
  
    -   Para timers, ouvintes de eventos (eventos DOM), eventos de layout e retornos de chamada de quadro de animação, um resumo codificado por cores do evento selecionado e todos os seus filhos aparecem na seção **Resumo do tempo inclusivo** (o anel codificado por cor). Cada fatia codificada por cor da imagem representa um tipo de evento. As dicas de ferramenta fornecem o nome do tipo de evento.  
  
    > [!TIP]
    >  O gráfico de detalhes da linha do tempo e o **Resumo de tempo inclusivo** podem ajudá-lo a identificar áreas para otimização. Se uma dessas exibições mostrar grandes números de pequenas tarefas, o evento poderá ser um candidato à otimização. Por exemplo, um aplicativo pode estar atualizando elementos DOM com frequência, resultando em um grande número de eventos de layout e análise de HTML. Você poderá otimizar o desempenho processando esse trabalho em lotes.  
  
###  <a name="FilterTimelineDetails"></a> Filtrar detalhes da linha do tempo  
 Você pode filtrar a exibição nos detalhes da linha do tempo para um evento particular selecionando **Filtrar para evento** no menu de contexto de um evento específico. Quando você escolhe essa opção, a linha do tempo e a exibição de grade têm como escopo o evento selecionado A seleção no gráfico de uso da CPU também tem como escopo o evento especial.  
  
 ![Filtragem de linha do tempo para um evento](../profiling/media/js_htmlvizprofiler_filtertoevent.png "JS_HTMLVizProfiler_FilterToEvent")  
  
###  <a name="FilterEvents"></a> Filtrar eventos  
 Você pode filtrar alguns eventos do gráfico de detalhes da linha do tempo para reduzir o ruído nos dados ou para eliminar dados que não são interessantes para seu cenário de desempenho. É possível filtrar por nome ou por duração de evento, ou ainda, pelos filtros específicos descritos aqui.  
  
 Desmarque a opção **Atividade em segundo plano** do ícone de filtro no painel inferior para filtrar a decodificação de imagem, o download especulativo e os eventos GC. Como esses eventos não são muito acionáveis, eles ficam ocultos por padrão.  
  
 ![Filtrando eventos na linha do tempo](../profiling/media/js_htmlvizprofiler_event_filter.png "JS_HTMLVizProfiler_Event_Filter")  
  
 Para filtrar os eventos de solicitação HTTP, desmarque a opção **Tráfego de rede** do ícone de filtro no painel inferior. Por padrão, esses eventos são mostrados no gráfico de detalhes da linha do tempo.  
  
 Para filtrar a atividade do thread da interface do usuário, desmarque a opção **Atividade da interface do usuário**.  
  
> [!TIP]
>  Desmarque esta opção e marque a opção Tráfego de rede para investigar problemas relacionados à latência de rede.  
  
 Para filtrar as medidas do usuário, desmarque a opção **Medidas do usuário**. As medidas do usuário são eventos de nível superior, sem filhos.  
  
###  <a name="GroupFrames"></a> Agrupar eventos por quadro  
 Você pode agrupar os eventos que aparecem na exibição dos detalhes da linha do tempo em quadros individuais. Tais eventos de quadros são eventos gerados por ferramenta e representam contêineres de evento de nível superior, para todo o trabalho de thread da interface do usuário que ocorre entre os eventos de pintura. Para habilitar esta exibição, selecione **Agrupar eventos de nível superior por quadro**.  
  
 ![Agrupar eventos de nível superior por quadro](../profiling/media/js_htmlvizprofiler_frame_grouping_button.png "JS_HTMLVizProfiler_Frame_Grouping_Button")  
  
 Ao agrupar os eventos por quadro, cada um dos eventos de nível superior na exibição de detalhes da linha do tempo representa um quadro.  
  
 ![Eventos de linha do tempo agrupados por quadro](../profiling/media/js_htmlvizprofiler_frame_grouping.png "JS_HTMLVizProfiler_Frame_Grouping")  
  
## <a name="save-a-diagnostic-session"></a>Salvar uma sessão de diagnóstico  
 No Visual Studio, você pode salvar uma sessão de diagnóstico ao fechar a guia associada à sessão. As sessões salvas podem ser reabertas mais tarde.  
  
## <a name="profiler-event-reference"></a>Referência de evento do criador de perfil  
 Os eventos do Criador de Perfis são categorizados e codificados por cor no Criador de Perfis de Capacidade de Resposta de Interface de Usuário. Essas são as categorias de evento:  
  
- **Carregamento.** Indica o tempo gasto para recuperar recursos do aplicativo e analisar HTML e CSS quando o aplicativo é carregado pela primeira vez. Isso pode incluir solicitações de rede.  
  
- **Geração de script.** Indica a análise de tempo gasto e o JavaScript em execução. Isso inclui eventos DOM, temporizadores, avaliação de script e trabalho de quadro de animação. Inclui o código do usuário e o código da biblioteca.  
  
- **GC.** Indica o tempo gasto na coleta de lixo.  
  
- **Estilização.** Indica o tempo gasto analisando o CSS e calculando a apresentação e o layout do elemento.  
  
- **Renderização.** Indica o tempo gasto na pintura da tela.  
  
- **Decodificação de imagem.** Indica o tempo gasto com a descompactação e a decodificação de imagens.  
  
  Para o script e as categorias de estilo, o Criador de Perfis de Capacidade de Resposta de Interface de Usuário pode fornecer dados que você pode manipular no gráfico de detalhes da linha de tempo. Caso identifique problemas de script, você pode executar o criador de perfis de amostragem de CPU com o criador de perfis de Capacidade de Resposta da Interface de Usuário. Opcionalmente, você poderia usar o criador de perfis de função do Visual Studio para obter dados mais detalhados. Para obter mais informações, consulte [Memória JavaScript](../profiling/javascript-memory.md).  
  
  Para as outras categorias de evento, talvez você possa identificar os efeitos colaterais da plataforma resultantes da adição de funcionalidades ao seu aplicativo, mas nesses casos você não poderá resolver determinados problemas de desempenho usando o Criador de Perfis de Capacidade de Resposta de Interface de Usuário.  
  
  Esta tabela mostra os eventos e suas descrições:  
  
|evento|Categoria do evento|Ocorre quando|  
|-----------|--------------------|-----------------|  
|Análise de CSS|Carregando|Um novo conteúdo CSS foi encontrado e foi feita uma tentativa de analisar o conteúdo CSS.|  
|Análise de HTML|Carregando|Um novo conteúdo HTML foi encontrado e foi feita uma tentativa de analisa-lo em nós e de inseri-lo na árvore DOM.|  
|Solicitação HTTP|Carregando|Um recurso remoto foi encontrado no DOM, ou uma XMLHttpRequest foi criada resultando em uma solicitação HTTP.|  
|Download especulativo|Carregando|O conteúdo HTML da página foi pesquisado para obter os recursos necessários de modo que as solicitações HTTP subsequentes para os recursos pudessem ser agendadas rapidamente.|  
|Função de retorno de chamada do quadro de animação|Script|O navegador estava prestes a renderizar outro quadro e isso disparou uma função de retorno de chamada fornecida pelo aplicativo.|  
|Evento DOM|Script|Um evento DOM ocorreu e foi executado.<br /><br /> A propriedade `context` para o evento DOM, como `DOMContentLoaded` ou `click` é mostrada entre parênteses.|  
|Ouvinte de eventos|Script|Um ouvinte de evento foi chamado e executado.|  
|Ouvinte de consulta de mídia|Script|Uma consulta de mídia registrada foi invalidada, resultando na execução dos seus ouvintes associados.|  
|Observador de mutação|Script|Um ou mais elementos DOM observados foram modificados, resultando na execução de um retorno de chamada associado do MutationObserver.|  
|Avaliação de script|Script|Um novo elemento SCRIPT foi encontrado no DOM e foi feita uma tentativa de analisar e executar o script.|  
|Temporizador|Script|Um temporizador agendado teve o tempo decorrido, e isso resultou na execução de sua função associada de retorno de chamada.|  
|Função de retorno de chamada assíncrona do Tempo de Execução do Windows|Script|Uma operação assíncrona que disparou uma função de retorno de chamada `Promise` foi concluída por um objeto do Tempo de Execução do Windows.|  
|Evento do Tempo de Execução do Windows|Script|Um evento ocorrido em um objeto do Tempo de Execução do Windows disparou um ouvinte registrado.|  
|Coleta de lixo|GC|O tempo foi gasto na coleta de memória para objetos que não estão mais em uso.|  
|Cálculo CSS|Estilo|Foram feitas alterações no DOM que exigiram que as propriedades de estilo de todos os elementos afetados fossem recalculadas.|  
|Layout|Estilo|Foram feitas alterações no DOM que exigiram que o tamanho e/ou a posição de todos os elementos afetados fossem recalculados.|  
|Pintura|Renderização|Foram feitas alterações visuais no DOM além de uma tentativa de renderizar novamente partes da página.|  
|Renderizar camada|Renderização|Foram feitas alterações visuais em um fragmento do DOM (chamado de camada) renderizado independentemente, e as alterações exigiram que uma parte da página fosse renderizada.|  
|Decodificação de imagem|Decodificação de Imagem|Foi incluída uma imagem no DOM e foi feita uma tentativa de descompactar decodificar a imagem do seu formato original para bitmap.|  
|Quadro|N/D|Foram feitas alterações visuais no DOM, o que exigiu que todas as partes afetadas da página fossem redesenhadas. Este é um evento gerado por ferramenta usado para agrupamento.|  
|Medida do usuário|N/D|Um cenário específico do aplicativo foi medido usando o método `performance.measure`. Este é um evento gerado por ferramenta usado para analisar códigos.|  
  
## <a name="additional-information"></a>Informações adicionais  
  
-   Assista a [este vídeo](https://channel9.msdn.com/Events/Build/2013/3-316) da conferência Build 2013 sobre o criador de perfil de Capacidade de Resposta de Interface do Usuário.  
  
-   Leia as dicas de desempenho para aplicativos UWP criados para o Windows usando JavaScript. Para obter mais informações, consulte [Melhores práticas para aplicativos UWP usando JavaScript](/previous-versions/windows/apps/hh465194\(v\=win.10\)).  
  
-   Para obter informações sobre o modelo e desempenho de execução de código de thread único, consulte [Executando código](/previous-versions/windows/apps/hh781217\(v\=win.10\)).  
  
## <a name="see-also"></a>Consulte também  
 [Introdução às ferramentas de criação de perfil](../profiling/profiling-feature-tour.md)