---
title: Executando ferramentas de criação de perfil com ou sem o depurador | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 3fcdccad-c1bd-4c67-bcec-bf33a8fb5d63
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6fb07e9bc6c308e27e3ad054c5aeb0b12c092054
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85533998"
---
# <a name="running-profiling-tools-with-or-without-the-debugger"></a>Executando ferramentas de criação de perfil com ou sem o depurador
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O Visual Studio agora oferece a opção de ferramentas de desempenho, algumas das quais (por exemplo, **Utilização de CPU** e **Uso de Memória**) podem ser executadas com ou sem o depurador. Ferramentas de desempenho de não depurador não devem ser executadas em configurações de versão, enquanto ferramentas integradas ao depurador destinam-se a ser executadas em configurações de depuração.  
  
## <a name="should-i-run-the-tool-with-or-without-the-debugger"></a>Devo executar a ferramenta com ou sem o depurador?  
 Ferramentas de desempenho integradas ao depurador permitem fazer muitas coisas que as ferramentas de não depurador não podem, como definir pontos de interrupção e inspecionar os valores de variáveis. Ferramentas de não depurador oferecem uma experiência mais próxima da que os usuários do aplicativo lançado verão.  
  
 Essas são algumas perguntas que podem ajudar a decidir qual tipo de ferramenta é o ideal para suas finalidades:  
  
1. O problema foi encontrado enquanto o aplicativo estava sendo desenvolvido ou em uma versão já lançada?  
  
     Se o problema que você está lidando com foi encontrado durante o desenvolvimento, você provavelmente não precisará executar as ferramentas de desempenho em um build de versão. Se ele foi encontrado em uma versão de lançamento, reproduza o problema com uma configuração de versão e decida se o depurador ajudaria ou não a obter mais informações.  
  
2. O problema foi causado pelo uso intensivo de processamento da CPU?  
  
     Muitos problemas ocorrem devido a questões de desempenho externo como E/S do arquivo ou a capacidade de resposta da rede, portanto não faz muita diferença se você executar as ferramentas de desempenho com ou sem o depurador. Se o problema é causado por chamadas de uso intensivo de CPU, a diferença entre as configurações de Versão e Depuração pode ser considerável e você provavelmente deve verificar se o problema existe no build de Versão antes de usar as ferramentas integradas ao depurador  
  
3. Você precisa avaliar com desempenho com precisão ou um número aproximado é aceitável?  
  
     Builds de depuração não têm determinadas otimizações que builds de Versão fornecem, como por exemplo, constantes e chamadas de função embutidas, remoção de caminhos de código não utilizados e armazenamento de variáveis de maneiras que não podem ser usadas pelo depurador. O próprio depurador altera os tempos de desempenho, pois ele executa determinadas operações que são necessárias para depuração (por exemplo, interceptar exceções e eventos de módulo de carga). Por isso, os números de desempenho nas ferramentas integradas ao depurador são precisão apenas na faixa de dezenas de milissegundos. Números de desempenho para as configurações de Versão com as ferramentas de não depurador são muito mais precisos.  
  
## <a name="collect-profiling-data-while-debugging"></a><a name="BKMK_Quick_start__Collect_diagnostic_data"></a> Coletar dados de criação de perfil ao depurar  
 A seção a seguir lida com a depuração local. Você pode descobrir mais sobre a depuração em um dispositivo ou a depuração remota nas próximas seções.  
  
1. Abra o projeto que você deseja depurar e clique em **Depurar / Iniciar Depuração** (ou **Iniciar** na barra de ferramentas ou **F5**).  
  
2. A janela de **ferramentas de diagnóstico** aparece automaticamente, a menos que você a tenha desativado. Para abrir a janela novamente, clique em **Depurar/Windows/Mostrar Ferramentas de Diagnóstico**.  
  
3. Execute os cenários dos quais deseja coletar dados.  
  
    Enquanto você estiver executando a sessão, poderá ver informações sobre eventos, memória de processo e utilização da CPU.  
  
    O gráfico a seguir mostra a janela **Ferramentas de Diagnóstico** no Visual Studio 2015 Atualização 1:  
  
    ![DiagnosticTools&#45;Atualização1](../profiling/media/diagnostictools-update1.png "DiagnosticTools-Atualização1")  
  
4. Você pode optar por ver **Uso de Memória** ou **Utilização de CPU** (ou ambos) com as configurações **Selecionar Ferramentas** na barra de ferramentas. Se você estiver executando o Visual Studio Enterprise, poderá habilitar ou desabilitar o IntelliTrace em **Ferramentas / Opções / IntelliTrace**.  
  
5. A sessão de diagnóstico termina quando você interrompe a depuração.  
  
   No Visual Studio 2015 Atualização 1, a janela **Ferramentas de Diagnóstico** facilita você se concentrar nos eventos que lhe interessam.   Os nomes de evento agora são mostrados com prefixos de categoria (**Gesture**, **Program Output**, **Breakpoint**, **File**, etc.) para que você possa verificar rapidamente a lista para uma determinada categoria ou ignorar as categorias que não lhe interessam.  
  
   A janela agora tem uma caixa de pesquisa para que você possa localizar uma cadeia de caracteres específica em qualquer lugar na lista de eventos. Por exemplo, o gráfico a seguir mostra os resultados de uma pesquisa da cadeia de caracteres "install" que corresponde a quatro eventos:  
  
   ![DiagnosticsEventSearch](../profiling/media/diagnosticseventsearch.png "DiagnosticsEventSearch")  
  
   Você também pode filtrar eventos dentro e fora da exibição na janela. Na lista suspensa **Filtro**, você pode marcar ou desmarcar categorias específicas de eventos:. Os nomes de categoria são os mesmos que os nomes de prefixo.  
  
   ![DiagnosticEventFilter](../profiling/media/diagnosticeventfilter.png "DiagnosticEventFilter")  
  
   Para obter mais informações, consulte [Pesquisando e filtrando a guia de Eventos na janela de Ferramentas de Diagnóstico](https://devblogs.microsoft.com/devops/searching-and-filtering-the-events-tab-of-the-diagnostic-tools-window/).  
  
## <a name="collect-profiling-data-without-debugging"></a>Coletar dados de criação de perfil sem depuração  
 Algumas ferramentas de criação de perfil requerem privilégios de administrador para serem executadas. Você pode abrir o Visual Studio como administrador ou optar por executar as ferramentas como administrador ao iniciar a sessão de diagnóstico.  
  
1. Abra o projeto no Visual Studio.  
  
2. No menu **depurar** , escolha **criador de perfil de desempenho...** (tecla de atalho: Alt + F2).  
  
3. Na página de inicialização de diagnóstico, escolha uma ou mais ferramentas para executar na sessão. São exibidas apenas as ferramentas que são aplicáveis ao tipo de projeto, o sistema operacional e à linguagem de programação. Quando você escolhe uma ferramenta de diagnóstico, as seleções de ferramentas que não podem ser executadas na mesma sessão de diagnóstico são desabilitadas. Veja aqui suas possíveis suas escolhas para um aplicativo Universal do Windows C#:  
  
    ![Selecione as ferramentas de diagnóstico](../profiling/media/diag-selecttool.png "DIAG_SelectTool")  
  
4. Para iniciar a sessão de diagnóstico, clique em **Iniciar**.  
  
5. Execute os cenários para os quais você deseja coletar dados.  
  
    Durante a execução da sessão, algumas ferramentas exibem gráficos de dados em tempo real na página de início das ferramentas de diagnóstico.  
  
    ![Coletar dados sobre o desempenho e diagnóstico pag](../profiling/media/pdhub-collectdata.png "PDHUB_CollectData")  
  
6. Para encerrar a sessão de diagnóstico, clique em **Parar a coleta**.  
  
   Quando você interrompe a coleta de dados em uma sessão de diagnóstico, os dados são analisados e o relatório é exibido na página Diagnóstico.  
  
   Você também pode abrir arquivos de sessão .diagnostic salvos na página de inicialização de ferramentas de diagnóstico.  
  
   ![Abrir um arquivo de sessão de diagnóstico salvo](../profiling/media/pdhub-openexistingdiagsession.png "PDHUB_OpenExistingDiagSession")  
  
## <a name="the-profiling-report"></a>O relatório de criação de perfil  
 ![Relatório de ferramentas de diagnóstico](../profiling/media/diag-report.png "DIAG_Report")  
  
|Imagem|Descrição|  
|-|-|  
|![Etapa 1](../profiling/media/procguid-1.png "ProcGuid_1")|A linha de tempo mostra a duração da sessão de criação de perfil, os eventos de ativação de ciclo de vida do aplicativo e as marcas de usuário.|  
|![Etapa 2](../profiling/media/procguid-2.png "ProcGuid_2")|Você pode restringir o relatório a uma parte da linha do tempo arrastando as barras azuis para selecionar uma região da linha do tempo.|  
|![Etapa 3](../profiling/media/procguid-3.png "ProcGuid_3")|Uma ferramenta exibe um ou mais grafos mestres. Se sua sessão de diagnóstico for criada com várias ferramentas, todos os grafos mestres serão exibidos.|  
|![Etapa 4](../profiling/media/procguid-4.png "ProcGuid_4")|Você pode recolher e expandir os gráficos individuais.|  
|![Etapa 5](../profiling/media/procguid-6.png "ProcGuid_6")|Quando seus dados incluem informações de várias ferramentas, os detalhes da ferramenta são coletados sob as guias.|  
|![Etapa 6](../profiling/media/procguid-6a.png "ProcGuid_6a")|Uma ferramenta poder ter uma ou mais exibições de detalhes. A exibição é filtrada pela região selecionada da linha do tempo.|  
  
## <a name="setting-the-analysis-target-to-another-device"></a>Configurando o destino da análise para outro dispositivo  
 Além de iniciar o aplicativo a partir do projeto do Visual Studio, você também pode executar sessões de diagnóstico em destinos alternativos. Por exemplo, você pode diagnosticar problemas de desempenho em uma versão de seu aplicativo que foi instalado por meio da Windows Store.  
  
 ![Escolher destino de análise de ferramentas de diagnóstico](../profiling/media/pdhub-chooseanalysistarget.png "PDHUB_ChooseAnalysisTarget")  
  
 Você pode iniciar aplicativos já instalados em um dispositivo ou pode anexar as ferramentas de diagnóstico a alguns aplicativos que já estão em execução. Ao escolher **Aplicativo em Execução** ou **Aplicativo Instalado**, você seleciona o aplicativo em uma lista que descobre os aplicativos no destino de implantação especificado.  
  
 ![Escolha um aplicativo em execução ou instalado para diagnóstico](../profiling/media/pdhub-selectrunningapp.png "PDHUB_SelectRunningApp")  
  
 Ao escolher **Internet Explorer**, você especifica a URL e pode alterar o destino da implantação do telefone.  
  
 ![Especifique a URL a ser exibida no Internet Explorer](../profiling/media/pdhub-choosephoneanalysistarget.png "PDHUB_ChoosePhoneAnalysisTarget")  
  
## <a name="remote-debugging"></a>Depuração remota  
 Executar uma sessão de diagnóstico em um computador ou tablet remoto exige que as Ferramentas Remotas do Visual Studio estejam instaladas e em execução no destino remoto. Para aplicativos de área de trabalho, consulte [Depuração remota](../debugger/remote-debugging.md).  Para aplicativos Windows Universal, consulte [Executar aplicativos da Windows Store em um computador remoto](../debugger/run-windows-store-apps-on-a-remote-machine.md).  
  
## <a name="blog-posts-and-msdn-articles-from-the-diagnostics-development-team"></a>Postagens em blogs e artigos do MSDN da equipe de desenvolvimento de Diagnóstico  
 [MSDN Magazine: análise do desempenho durante a depuração no Visual Studio 2015](https://msdn.microsoft.com/magazine/dn973013.aspx)  
  
 [MSDN Magazine: uso do IntelliTrace para diagnosticar problemas com mais rapidez](https://msdn.microsoft.com/magazine/dn973014.aspx)  
  
 [Postagem do blog: diagnosticar vazamentos de manipulador de eventos com a ferramenta de Uso de Memória no Visual Studio 2015](https://devblogs.microsoft.com/devops/diagnosing-event-handler-leaks-with-the-memory-usage-tool-in-visual-studio-2015/)  
  
 [Vídeo: depuração histórica com o IntelliTrace no Microsoft Visual Studio Ultimate 2015](https://channel9.msdn.com/Events/Ignite/2015/BRK3716)  
  
 [Vídeo: depurar problemas de desempenho usando o Visual Studio 2015](https://channel9.msdn.com/Events/Build/2015/3-731)  
  
 [PerfTips: informações de desempenho imediatas durante depuração com o Visual Studio](https://devblogs.microsoft.com/devops/perftips-performance-information-at-a-glance-while-debugging-with-visual-studio/)  
  
 [Janela do depurador Ferramentas de Diagnóstico no Visual Studio 2015](https://devblogs.microsoft.com/devops/diagnostic-tools-debugger-window-in-visual-studio-2015/)  
  
 [IntelliTrace no Visual Studio Enterprise 2015](https://devblogs.microsoft.com/devops/intellitrace-in-visual-studio-ultimate-2015/)
