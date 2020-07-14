---
title: Executar ferramentas de criação de perfil com ou sem o depurador | Microsoft Docs
ms.date: 5/26/2020
ms.topic: conceptual
ms.assetid: 3fcdccad-c1bd-4c67-bcec-bf33a8fb5d63
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 45632967c39348e8dc78dc3e2fb95227dcd86d7d
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85285875"
---
# <a name="run-profiling-tools-with-or-without-the-debugger"></a>Executar ferramentas de criação de perfil com ou sem o depurador

O Visual Studio oferece uma opção de medida de desempenho e ferramentas de criação de perfil. Algumas ferramentas, como uso de CPU e uso de memória, podem ser executadas com ou sem o depurador e no lançamento ou depuração de configurações de compilação. As ferramentas do criador de perfil de desempenho como Linha do Tempo do Aplicativo podem ser executadas em compilações de depuração ou versão. Ferramentas integradas ao depurador, como a janela Ferramentas de Diagnóstico e a guia eventos, são executadas somente durante sessões de depuração.

>[!NOTE]
>É possível usar as ferramentas de desempenho de não depurador com o Windows 7 e posterior. O Windows 8 ou posterior é necessário para executar as ferramentas de criação de perfil integradas ao depurador.

O Criador de Perfil de Desempenho do não depurador e as Ferramentas de Diagnóstico integradas ao depurador fornecem diferentes informações e experiências. Ferramentas integradas ao depurador mostram pontos de interrupção e valores de variável. Ferramentas de não depurador oferecem resultados mais próximos à experiência do usuário final.

Para ajudar a decidir quais ferramentas e os resultados usar, considere o seguinte:

- Problemas de desempenho externos, como E/S de arquivo ou problemas na capacidade de resposta da rede, não terão uma aparência muito diferente nas ferramentas do depurador ou de não depurador.
- Para problemas causados por chamadas com uso intensivo de CPU, pode haver diferenças consideráveis de desempenho entre compilações de versão e depuração. Verifique se o problema existe nas compilações de versão.
- Se o problema ocorrer somente durante compilações de depuração, você provavelmente não precisará executar as ferramentas de não depurador. Para problemas de compilação de versão, decida se as ferramentas do depurador ajudarão a investigar ainda mais.
- Os builds de versão fornecem otimizações como embutimento de constantes e de chamadas de função, remoção de caminhos de código não utilizados e armazenamento de variáveis de maneiras que não possam ser usadas pelo depurador. Os números de desempenho nas ferramentas integradas ao depurador são menos precisos, pois as compilações de depuração não têm essas otimizações.
- O próprio depurador altera os tempos de desempenho, pois ele precisa de operações do depurador, como interceptar eventos de carregamento de exceção e módulo.
- Os números de desempenho do build de versão nas ferramentas do Criador de Perfil de Desempenho são os mais precisos e exatos. Os resultados da ferramenta integrada ao depurador são mais úteis para comparar com outras medidas relacionadas à depuração.

## <a name="collect-profiling-data-while-debugging"></a><a name="BKMK_Quick_start__Collect_diagnostic_data"></a> Coletar dados de criação de perfil ao depurar

Quando você inicia a depuração no Visual Studio selecionando **depurar**  >  **Iniciar Depuração**ou pressionando **F5**, a janela **ferramentas de diagnóstico** é exibida por padrão. Para abri-lo manualmente, selecione **depurar**  >  **janelas**  >  **Mostrar ferramentas de diagnóstico**. A janela **Ferramentas de Diagnóstico** mostra informações sobre eventos, memória do processo e uso da CPU.

![Captura de tela da janela de Ferramentas de Diagnóstico](../profiling/media/diagnostictoolswindow.png " Janela Ferramentas de Diagnóstico")

- Use o ícone **Configurações** na barra de ferramentas para selecionar se deseja exibir **Uso de Memória**, **Análise da interface do usuário** e **Uso da CPU**.

- Selecione **configurações** na lista suspensa **configurações** para abrir as **páginas de propriedades do ferramentas de diagnóstico** com mais opções.

- Se estiver executando Visual Studio Enterprise, você poderá habilitar ou desabilitar o IntelliTrace acessando **ferramentas**  >  **Opções**  >  **IntelliTrace**.

A sessão de diagnóstico termina quando você interrompe a depuração.

### <a name="the-events-tab"></a>A guia Eventos

Durante uma sessão de depuração, a guia Eventos da janela Ferramentas de Diagnóstico lista os eventos de diagnóstico que ocorrem. O *ponto de interrupção*de prefixos de categoria, *arquivo*e outros, permitem que você examine rapidamente a lista em busca de uma categoria ou ignore as categorias das quais você não se importa.

Use a lista suspensa **filtro** para filtrar eventos dentro e fora do modo de exibição, selecionando ou desmarcando categorias específicas de eventos.

![Captura de tela do filtro de eventos de diagnóstico](../profiling/media/diagnosticeventfilter.png "Filtro de eventos de diagnóstico")

Use a caixa de pesquisa para localizar uma cadeia de caracteres específica na lista de eventos. Aqui estão os resultados de uma pesquisa do *nome* da cadeia de caracteres que correspondeu a quatro eventos:

![Captura de tela da pesquisa de eventos de diagnóstico](../profiling/media/diagnosticseventsearch.png "Pesquisa de eventos de diagnóstico")

Para obter mais informações, consulte [Pesquisando e filtrando a guia de Eventos na janela de Ferramentas de Diagnóstico](https://devblogs.microsoft.com/devops/searching-and-filtering-the-events-tab-of-the-diagnostic-tools-window/).

## <a name="collect-profiling-data-without-debugging"></a>Coletar dados de criação de perfil sem depuração

Para coletar dados de desempenho sem depuração, é possível executar as ferramentas do Criador de Perfil de Desempenho.

1. Com um projeto aberto no Visual Studio, defina a configuração da solução como **liberar**e selecione **depurador local do Windows**   (ou **computador local**) como o destino de implantação.

1. Selecione **debug**  >  **Performance Profiler**ou pressione **ALT** + **F2**.

1. Na página inicialização das ferramentas de diagnóstico, selecione uma ou mais ferramentas para executar. Somente as ferramentas aplicáveis ao tipo de projeto, ao sistema operacional e à linguagem de programação são mostradas. Selecione **Mostrar todas as ferramentas** para ver também as ferramentas desabilitadas para essa sessão de diagnóstico.

   ![Captura de tela das ferramentas de diagnóstico](../profiling/media/diaghubsummarypage.png "DIAG_SelectTool")

1. Para iniciar a sessão de diagnóstico, selecione **Iniciar**.

   Enquanto a sessão está em execução, algumas ferramentas mostram grafos de dados em tempo real na página ferramentas de diagnóstico, bem como controles para pausar e retomar a coleta de dados.

    ![Captura de tela da coleta de dados no Hub de desempenho e diagnóstico](../profiling/media/diaghubcollectdata.png "Coletar dados do Hub")

1. Para encerrar a sessão de diagnóstico, selecione **Interromper coleta**.

   Os dados analisados aparecem na página do **relatório** .

Você pode salvar os relatórios e abri-los na lista de **sessões abertas recentemente** na página de inicialização ferramentas de diagnóstico.

![Captura de tela de Ferramentas de Diagnóstico lista de sessões abertas recentemente](../profiling/media/diaghubopenexistingdiagsession.png "PDHUB_OpenExistingDiagSession")

## <a name="collect-profiling-data-from-the-command-line"></a>Coletar dados de criação de perfil da linha de comando

Para medir os dados de desempenho da linha de comando, você pode usar VSDiagnostics.exe, que está incluído com o Visual Studio ou o Ferramentas Remotas. Isso é útil para capturar rastreamentos de desempenho em sistemas nos quais o Visual Studio não está instalado ou para gerar scripts da coleção de rastreamentos de desempenho. Ao usar VSDiagnostics.exe, você começa uma sessão de diagnóstico que captura e armazena dados de criação de perfil até que a ferramenta seja interrompida. Nesse ponto, esses dados são exportados para um arquivo. diagsession e você pode abrir esse arquivo no Visual Studio para analisar os resultados.

### <a name="launch-an-application"></a>Iniciar um aplicativo

1. Abra um prompt de comando e altere para o diretório com VSDiagnostics.exe:

   ```
   <Visual Studio Install Folder>\Team Tools\DiagnosticsHub\Collector\
   ```

2. Inicie VSDiagnostics.exe com o seguinte comando:

   ```
   VSDiagnostics.exe start <id> /launch:<appToLaunch> /loadConfig:<configFile>
   ```

   Você deve incluir os seguintes argumentos:

   - \<id\>: Identifica a sessão de coleta. A ID precisa ser um número entre 1 e 255.
   - \<appToLaunch\>: O arquivo executável a ser iniciado e perfil.
   - \<configFile\>: O arquivo de configuração para o agente de coleta que você deseja iniciar.

3. Para interromper a coleta e exibir seus resultados, siga as etapas na seção "parar coleta" mais adiante neste artigo.

### <a name="attach-to-an-existing-application"></a>Anexar a um aplicativo existente

1. Abra um aplicativo, como o bloco de notas e, em seguida, abra o **Gerenciador de tarefas** para obter sua ID de processo (PID). No Gerenciador de tarefas, localize o PID na guia **detalhes**   .
2. Abra um prompt de comando e altere para o diretório com o executável do agente de coleta. Normalmente, está aqui:

   ```
   <Visual Studio installation folder>\2019\Preview\Team Tools\DiagnosticsHub\Collector\
   ```

3. Inicie o arquivo de VSDiagnostics.exe digitando o comando a seguir.

   ```
   VSDiagnostics.exe start <id> /attach:<pid> /loadConfig:<configFile>
   ```

   Você deve incluir os seguintes argumentos:

   - \<id\>: Identifica a sessão de coleta. A ID precisa ser um número entre 1 e 255.
   - \<pid\>: O PID do processo no qual você deseja criar o perfil, que nesse caso é o PID encontrado na etapa 1.
   - \<configFile\>: O arquivo de configuração para o agente de coleta que você deseja iniciar. Para obter mais informações, consulte [arquivos de configuração para agentes](../profiling/profile-apps-from-command-line.md).

4. Para interromper a coleta e exibir seus resultados, siga as etapas na próxima seção.

### <a name="stop-collection"></a>Parar coleta

1. Pare a sessão de coleta e envie a saída para um arquivo, digitando o comando a seguir.

   ```
   VSDiagnostics.exe stop <id> /output:<path to file>
   ```

2. Acesse a saída de arquivo do comando anterior e abra-a no Visual Studio para examinar as informações coletadas.

## <a name="agent-configuration-files"></a> Arquivos de configuração do Agente

Os agentes de coleta são componentes intercambiáveis que coletam tipos diferentes de dados, dependendo do que você está tentando medir.
Para sua conveniência, você pode armazenar essas informações em um arquivo de configuração do agente. O arquivo de configuração é um arquivo. JSON que contém, no mínimo, o nome do arquivo. dll e seu CLSID de COM. Estes são os arquivos de configuração de exemplo que podem ser encontrados na seguinte pasta:

```
<Visual Studio installation folder>\Team Tools\DiagnosticsHub\Collector\AgentConfigs\
```

Consulte os links a seguir para baixar e exibir os arquivos de configuração do agente:

- https://aka.ms/vs/diaghub/agentconfig/cpubase
- https://aka.ms/vs/diaghub/agentconfig/cpuhigh
- https://aka.ms/vs/diaghub/agentconfig/cpulow
- https://aka.ms/vs/diaghub/agentconfig/database
- https://aka.ms/vs/diaghub/agentconfig/dotnetasyncbase
- https://aka.ms/vs/diaghub/agentconfig/dotnetallocbase
- https://aka.ms/vs/diaghub/agentconfig/dotnetalloclow

As configurações de os (base/alta/baixa) correspondem aos dados coletados para a ferramenta de criação de perfil de [uso da CPU](../profiling/cpu-usage.md) .
As configurações de DotNetObjectAlloc (base/baixa) correspondem aos dados coletados para a [ferramenta de alocação de objeto .net](../profiling/dotnet-alloc-tool.md).

As configurações Base/Baixa/Alta referem-se à taxa de amostragem. Por exemplo, Baixa representa 100 amostras/segundo e Alta, 4.000 amostras/segundo.
Para que a ferramenta VSDiagnostics.exe funcione com um agente de coleta, ela requer uma DLL e um CLSID COM para o agente apropriado. O agente também pode ter opções de configuração adicionais. Se você usar um agente sem um arquivo de configuração, use o formato no seguinte comando:

```
VSDiagnostics.exe start <id> /attach:<pid> /loadAgent:<agentCLSID>;<agentName>[;<config>]
```
