---
title: Executar ferramentas de criação de perfil com ou sem o depurador | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 3fcdccad-c1bd-4c67-bcec-bf33a8fb5d63
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e8d088978e166f24f624b8ae05cdeb04137d8135
ms.sourcegitcommit: 54c65f81a138fc1e8ff1826f7bd9dcec710618cc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2018
ms.locfileid: "51948706"
---
# <a name="run-profiling-tools-with-or-without-the-debugger"></a>Executar ferramentas de criação de perfil com ou sem o depurador

O Visual Studio oferece uma opção de medida de desempenho e ferramentas de criação de perfil. Algumas ferramentas, como **Uso da CPU** e **Uso de Memória**, podem ser executadas com ou sem o depurador e nas configurações de build de Versão ou Depuração. Ferramentas **Criador de Perfil de Desempenho** como **Linha do Tempo do Aplicativo** podem ser executadas nos builds de Depuração ou de Versão. Ferramentas integradas ao depurador como a janela **Ferramentas de Diagnóstico** e a guia **Eventos** são executadas somente durante as sessões de depuração.  

>[!NOTE]
>É possível usar as ferramentas de desempenho de não depurador com o Windows 7 e posterior. O Windows 8 ou posterior é necessário para executar as ferramentas de criação de perfil integradas ao depurador.

O **Criador de Perfil de Desempenho** do não depurador e as **Ferramentas de Diagnóstico** integradas ao depurador fornecem diferentes informações e experiências. Ferramentas integradas ao depurador mostram pontos de interrupção e valores de variável. Ferramentas de não depurador oferecem resultados mais próximos à experiência do usuário final. 

Para ajudar a decidir quais ferramentas e resultados usar, considere os seguintes pontos:

- Problemas de desempenho externos, como E/S de arquivo ou problemas na capacidade de resposta da rede, não terão uma aparência muito diferente nas ferramentas do depurador ou de não depurador. 
- Para problemas causados por chamadas de uso intensivo de CPU, pode haver diferenças de desempenho consideráveis entre builds de Depuração e de Versão. Confira para ver se o problema existe em builds de versão. 
- Se o problema ocorre apenas durante os builds de depuração, você provavelmente não precisa executar as ferramentas de não depurador. Para problemas de build de versão, decida se as ferramentas do depurador ajudarão para uma investigação melhor. 
- Os builds de versão fornecem otimizações como embutimento de constantes e de chamadas de função, remoção de caminhos de código não utilizados e armazenamento de variáveis de maneiras que não possam ser usadas pelo depurador. Os números de desempenho nas ferramentas integradas ao depurador são menos precisos, porque os builds de Depuração não têm essas otimizações. 
- O próprio depurador altera os tempos de desempenho, à medida que realiza operações do depurador necessárias como eventos de exceção de interceptação e de carga de módulo. 
- Os números de desempenho do build de versão nas ferramentas do **Criador de Perfil de Desempenho** são os mais precisos e exatos. Os resultados da ferramenta integrada ao depurador são mais úteis para comparar com outras medidas relacionadas à depuração.

##  <a name="BKMK_Quick_start__Collect_diagnostic_data"></a> Coletar dados de criação de perfil ao depurar  

Quando você inicia a depuração no Visual Studio selecionando **Depurar** > **Iniciar depuração** ou pressionando **F5**, a janela **Ferramentas de Diagnóstico** é exibida por padrão. Para abri-la manualmente, selecione **Depurar** > **Janelas** > **Mostrar Ferramentas de Diagnóstico**. A janela **Ferramentas de Diagnóstico** mostra informações sobre eventos, memória do processo e uso da CPU.  

![Ferramentas de Diagnóstico](../profiling/media/diagnostictools-update1.png "Ferramentas de Diagnóstico")  

- Use o ícone **Configurações** na barra de ferramentas para selecionar se deseja exibir **Uso de Memória**, **Análise da interface do usuário** e **Uso da CPU**. 
  
- Selecione **Configurações** na lista suspensa **Configurações** para abrir **Páginas de propriedades de Ferramentas de Diagnóstico** com mais opções. 
  
- Se você estiver executando o Visual Studio Enterprise, poderá habilitar ou desabilitar o IntelliTrace em Visual Studio **Ferramentas** > **Opções** > **IntelliTrace**.  
  
A sessão de diagnóstico termina quando você interrompe a depuração.  
  
Também é possível exibir **Ferramentas de Diagnóstico** para destinos de depuração remota. Para criação de perfil e depuração remota, o Depurador Remoto do Visual Studio deve ser instalado e estar em execução no destino remoto. 
- Para depuração remota e projetos de aplicativo da área de trabalho de criação de perfil, confira [Depuração remota](../debugger/remote-debugging.md). 
- Para depuração remota e aplicativos UWP de criação de perfil, confira [Depurar aplicativos UWP em computadores remotos](../debugger/run-windows-store-apps-on-a-remote-machine.md). 

### <a name="the-events-tab"></a>A guia Eventos

Durante uma sessão de depuração, a guia **Eventos** da janela **Ferramentas de Diagnóstico** lista os eventos de diagnóstico que ocorrem. Os prefixos de categoria: **Ponto de interrupção**, **Arquivo** e outros permitem que você examine rapidamente uma categoria na lista ou ignore as categorias com as quais não se preocupa.  
  
Use a lista suspensa **Filtrar** para filtrar eventos dentro e fora da exibição marcando ou desmarcando a categorias de eventos específicas. 

![Filtro de Evento de Diagnóstico](../profiling/media/diagnosticeventfilter.png "Filtro de Evento de Diagnóstico")  

Use a caixa de pesquisa para localizar uma cadeia de caracteres específica na lista de eventos. Veja os resultados de uma pesquisa pelo "nome" da cadeia de caracteres que correspondeu a quatro eventos:  

![Pesquisa de evento de diagnóstico](../profiling/media/diagnosticseventsearch.png "Pesquisa de eventos de diagnóstico")  

Para obter mais informações, consulte [Pesquisando e filtrando a guia de Eventos na janela de Ferramentas de Diagnóstico](https://blogs.msdn.microsoft.com/devops/2015/11/12/searching-and-filtering-the-events-tab-of-the-diagnostic-tools-window/).  

## <a name="collect-profiling-data-without-debugging"></a>Coletar dados de criação de perfil sem depuração  

Para coletar dados de desempenho sem depuração, é possível executar as ferramentas do **Criador de Perfil de Desempenho**. Algumas ferramentas de criação de perfil requerem privilégios de administrador para serem executadas. É possível iniciar o Visual Studio como administrador ou executar as ferramentas como administrador quando inicia a sessão de diagnóstico.  
   
1. Com um projeto aberto no Visual Studio, selecione **Depurar** > **Criador de Perfil de Desempenho** ou pressione **Alt**+**F2**.  
   
1. Na página de início de diagnóstico, selecione uma ou mais ferramentas para serem executadas. São exibidas apenas as ferramentas que são aplicáveis ao tipo de projeto, o sistema operacional e à linguagem de programação. Selecione **Mostrar todas as ferramentas** para ver também as ferramentas desabilitadas para essa sessão de diagnóstico. Veja aqui como suas escolhas podem parecer para um aplicativo UWP em C#:  
   
   ![Selecionar as ferramentas de diagnóstico](../profiling/media/diag_selecttool.png "DIAG_SelectTool")  
   
1. Para iniciar a sessão de diagnóstico, selecione **Iniciar**.  
   
   Durante a execução da sessão, algumas ferramentas exibem grafos de dados em tempo real na página de ferramentas de diagnóstico.  
   
    ![Coletar dados sobre o Hub Desempenho e Diagnóstico](../profiling/media/pdhub_collectdata.png "Coletar dados do hub")  
   
1. Para encerrar a sessão de diagnóstico, selecione **Interromper coleta**.  
   
   Os dados analisados são exibidos na página **Relatório**.  
  
É possível salvar os relatórios e abri-los na lista **Sessões abertas recentemente** na página de início das ferramentas de diagnóstico.  

![Abrir um arquivo de sessão de diagnóstico salvo](../profiling/media/pdhub_openexistingdiagsession.png "PDHUB_OpenExistingDiagSession")  
  
### <a name="the-profiling-report"></a>O relatório de criação de perfil  
 ![Relatório de ferramentas de diagnóstico](../profiling/media/diag_report.png "DIAG_Report")  
  
|||  
|-|-|  
|![Etapa 1](../profiling/media/procguid_1.png "ProcGuid_1")|A linha de tempo mostra a duração da sessão de criação de perfil, os eventos de ativação de ciclo de vida do aplicativo e as marcas de usuário.|  
|![Etapa 2](../profiling/media/procguid_2.png "ProcGuid_2")|Você pode restringir o relatório a uma parte da linha do tempo arrastando as barras azuis para selecionar uma região da linha do tempo.|  
|![Etapa 3](../profiling/media/procguid_3.png "ProcGuid_3")|Cada ferramenta de diagnóstico exibe um ou mais grafos mestre. Se a sessão de diagnóstico teve mais de uma ferramenta, todos os grafos mestre são exibidos.|  
|![Etapa 4](../profiling/media/procguid_4.png "ProcGuid_4")|É possível recolher e expandir grafos individuais de cada ferramenta.|  
|![Etapa 5](../profiling/media/procguid_6.png "ProcGuid_6")|Quando os dados incluem mais de uma ferramenta, os detalhes da ferramenta são coletados em guias.|  
|![Etapa 6](../profiling/media/procguid_6a.png "ProcGuid_6a")|A metade inferior do relatório mostra uma ou mais exibições de detalhes para cada ferramenta. É possível filtrar a exibição selecionando regiões da linha do tempo.|  
  
## <a name="run-diagnostic-sessions-on-installed-or-running-apps"></a>Executar sessões de diagnóstico em aplicativos instalados ou em execução 

 Além de iniciar o aplicativo a partir do projeto do Visual Studio, você também pode executar sessões de diagnóstico em destinos alternativos. Por exemplo, é possível diagnosticar problemas de desempenho em um aplicativo instalado por meio da Windows Store.  
  
 ![Escolha o destino da análise de ferramentas de diagnóstico](../profiling/media/pdhub_chooseanalysistarget.png "PDHUB_ChooseAnalysisTarget")  
  
 É possível iniciar aplicativos já instalados ou anexar as ferramentas de diagnóstico a aplicativos e processos que já estão em execução. Ao selecionar **Aplicativo em Execução** ou **Aplicativo Instalado**, você seleciona o aplicativo em uma lista que localiza os aplicativos no destino de implantação especificado. Esse destino pode ser um computador remoto ou local. 
  
 ![Escolha um aplicativo em execução ou instalado para diagnóstico](../profiling/media/pdhub_selectrunningapp.png "PDHUB_SelectRunningApp")  
  
## <a name="see-also"></a>Consulte também

Veja a seguir postagens no blogs e artigos do MSDN da equipe de desenvolvimento de diagnóstico:  
 [MSDN Magazine: análise do desempenho durante a depuração no Visual Studio 2015](https://msdn.microsoft.com/magazine/dn973013.aspx)
  
 [MSDN Magazine: uso do IntelliTrace para diagnosticar problemas com mais rapidez](https://msdn.microsoft.com/magazine/dn973014.aspx)
  
 [Postagem do blog: diagnosticar vazamentos de manipulador de eventos com a ferramenta de Uso de Memória no Visual Studio 2015](https://blogs.msdn.microsoft.com/devops/2015/04/29/diagnosing-event-handler-leaks-with-the-memory-usage-tool-in-visual-studio-2015/)
  
 [Vídeo: depuração histórica com o IntelliTrace no Microsoft Visual Studio Ultimate 2015](https://channel9.msdn.com/Events/Ignite/2015/BRK3716)
  
 [Vídeo: depurar problemas de desempenho usando o Visual Studio 2015](https://channel9.msdn.com/Events/Build/2015/3-731)
  
 [PerfTips: informações de desempenho imediatas durante depuração com o Visual Studio](https://blogs.msdn.microsoft.com/devops/2014/08/18/perftips-performance-information-at-a-glance-while-debugging-with-visual-studio/)
  
 [Janela do depurador Ferramentas de Diagnóstico no Visual Studio 2015](https://blogs.msdn.microsoft.com/devops/2015/01/16/diagnostic-tools-debugger-window-in-visual-studio-2015/)
  
 [IntelliTrace no Visual Studio Enterprise 2015](https://blogs.msdn.microsoft.com/devops/2015/01/16/intellitrace-in-visual-studio-ultimate-2015/)
