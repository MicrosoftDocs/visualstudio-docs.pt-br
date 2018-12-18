---
title: Diagnosticar problemas após a implantação | Microsoft Docs
ms.custom: ''
ms.date: 04/10/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: a3463eab-a352-4d17-8551-adbaad526db0
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: b10635c1aefedf7af83a1c884717b80b442e8998
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50219907"
---
# <a name="diagnose-problems-after-deployment-using-intellitrace"></a>Diagnosticar problemas após a implantação usando o IntelliTrace

Para diagnosticar problemas no seu aplicativo da web ASP.NET após a implantação usando o IntelliTrace, inclua informações de compilação com a versão para permitir que o Visual Studio localize automaticamente os arquivos de origem e símbolos corretos que são necessárias para depurar o log do IntelliTrace.

 Se você estiver usando o Microsoft Monitoring Agent para controlar o IntelliTrace, também precisará configurar o monitoramento de desempenho do aplicativo no servidor da web. Ele registra eventos de diagnóstico enquanto seu aplicativo é executado e salva os eventos em um arquivo de log do IntelliTrace. Você pode, em seguida, examinar os eventos no Visual Studio Enterprise (mas não Professional ou Community edições), ir para o código onde ocorreu o evento, examinar os valores registrados no momento e avance ou retorne através do código que foi executado. Depois de encontrar e resolver o problema, repita o ciclo apenas para compilar, liberar e monitorar seu aplicativo para que você possa corrigir problemas potenciais futuros o quanto antes e com mais rapidez.

 ![Codificar, compilar, liberar, monitorar, diagnosticar, corrigir](../debugger/media/ffr_cycle.png "FFR_Cycle")

 **Você precisará:**

-   Visual Studio, DevOps do Azure ou o Team Foundation Server 2017, 2015, 2013, 2012 ou 2010 para configurar sua compilação

-   Para monitorar seu aplicativo e registrar dados de diagnóstico use o Microsoft Monitoring Agent

-   Visual Studio Enterprise (mas não as edições Professional ou Community) para examinar dados de diagnóstico e depurar seu código com o IntelliTrace

##  <a name="SetUpBuild"></a> Etapa 1: Inclua informações com sua versão de compilação
 Configurar o processo de compilação para criar um manifesto de compilação (*Buildinfo* arquivo) para a web de projeto e inclua esse manifesto em sua versão. Esse manifesto contém informações sobre o projeto, sobre o controle do código-fonte e o sistema de compilação utilizados para criar uma compilação específica. Essas informações ajudam o Visual Studio a encontrar o código-fonte e os símbolos correspondentes após abrir o log do IntelliTrace para revisar os eventos registrados.

###  <a name="AutomatedBuild"></a> Crie o manifesto de compilação para uma compilação automatizada usando o Team Foundation Server

 Siga essas etapas caso use Team Foundation Version Control ou Git.

####  <a name="TFS2017"></a> DevOps do Azure e o Team Foundation Server 2017

Visual Studio 2017 não inclui o *Buildinfo* arquivo, que foi substituído e, em seguida, removido. Para depurar aplicativos web ASP.NET após a implantação, use um dos seguintes métodos:

* Para implantação no Azure, use [Application Insights](https://docs.microsoft.com/azure/application-insights/).

* Se você precisar usar o IntelliTrace, abra o projeto no Visual Studio e carregar os arquivos de símbolo de compilação correspondente. Você pode carregar arquivos de símbolo a **módulos** janela ou por meio da configuração de símbolos no **ferramentas** > **opções** > **depuração**   >  **Símbolos**.


####  <a name="TFS2013"></a> Team Foundation Server 2013
 Configure seu pipeline de compilação para adicionar os locais de seu código-fonte, compilação e símbolos ao manifesto de compilação (Buildinfo config). O Team Foundation Build automaticamente cria esse arquivo e coloca-o em sua pasta de saída do projeto.

1.  [Edite seu pipeline de compilação ou crie um novo pipeline de compilação.](/azure/devops/pipelines/get-started-designer?view=vsts)

     ![Modo de exibição criar o pipeline no TFS 2013](../debugger/media/ffr_tfs2013viewbuilddefinition.png "FFR_TFS2013ViewBuildDefinition")

2.  Escolha o modelo padrão (TfvcTemplate.12.xaml) ou seu próprio modelo personalizado.

     ![Escolha o modelo de processo de compilação &#45; TFS 2013](../debugger/media/ffr_tfs2013buildprocesstemplate.png "FFR_TFS2013BuildProcessTemplate")

3.  Especifique onde salvar o arquivo de símbolos (PDB) de forma que o código-fonte seja indexado automaticamente.

     Se você usar um modelo personalizado, verifique se o modelo tem uma atividade para indexar o código-fonte. Posteriormente, adicione um argumento de MSBuild para especificar onde salvar o arquivo de símbolos.

     ![Configurar o caminho de símbolos no pipeline de build TFS 2013](../debugger/media/ffr_tfs2013builddefsymbolspath.png "FFR_TFS2013BuildDefSymbolsPath")

     Para obter mais informações sobre símbolos, consulte [publicar dados de símbolo](/azure/devops/pipelines/tasks/build/index-sources-publish-symbols?view=vsts).

4.  Adicione este argumento de MSBuild para incluir os locais do TFS e de símbolos ao arquivo de manifesto da compilação:

     **/p:IncludeServerNameInBuildInfo = true**

     Qualquer um que possa acessar seu servidor Web pode ver esses locais no manifesto de compilação. Certifique-se de que o servidor de código-fonte é seguro.

5.  Se você usa um modelo personalizado, adicione este argumento de MSBuild para especificar onde salvar o arquivo de símbolos:

     **1&gt;/p:buildsymbolstorepath=&lt;1}&lt;{2&gt;caminho =**\<*para símbolos*>

     ![Incluir informações do servidor de compilação na definição de compilação TFS 2013](../debugger/media/ffr_tfs2013builddefincludeserverinfo.png "FFR_TFS2013BuildDefIncludeServerInfo")

     E adicione estas linhas ao arquivo de seu projeto da Web (.csproj, .vbproj):

    ```xml
    <!-- Import the targets file. Change the folder location as necessary. -->
       <Import Project=""$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v$(VisualStudioVersion)\BuildInfo\Microsoft.VisualStudio.ReleaseManagement.BuildInfo.targets" />

    ```

     Qualquer um que possa acessar seu servidor Web pode ver esses locais no manifesto de compilação. Certifique-se de que o servidor de código-fonte é seguro.

6.  Execute uma nova compilação.

    Vá para [etapa 2: liberar seu aplicativo](#DeployRelease)

####  <a name="TFS2012_2010"></a> Team Foundation Server 2012 ou 2010
 Siga estas etapas para criar automaticamente o arquivo de manifesto de compilação (BuildInfo.config) para seu projeto e colocá-lo na pasta de saída do projeto. O arquivo aparece como "*ProjectName*. Buildinfo. config"na pasta de saída, mas é renomeado"Buildinfo. config"na pasta de implantação depois de publicar seu aplicativo.

1.  Instale o Visual Studio 2013 (qualquer edição) no servidor do Team Foundation Build.

2.  Em seu pipeline de compilação, especifique onde salvar os símbolos de forma que seu código-fonte seja indexado automaticamente.

     Se você usar um modelo personalizado, verifique se o modelo tem uma atividade para indexar o código-fonte.

3.  Adicione estes argumentos de MSBuild ao seu pipeline de compilação:

    -   **/p:VisualStudioVersion = 12.0**

    -   **/p:MSBuildAssemblyVersion = 12.0**

    -   **/TV:12.0**

    -   **/p:IncludeServerNameInBuildInfo = true**

    -   **1&gt;/p:buildsymbolstorepath=&lt;1}&lt;{2&gt;caminho =**\<*para símbolos*>

4.  Execute uma nova compilação.

    Vá para [etapa 2: liberar seu aplicativo](#DeployRelease)

###  <a name="ManualBuild"></a> Crie o manifesto de compilação para uma compilação manual usando o Visual Studio
 Siga estas etapas para criar automaticamente o arquivo de manifesto de compilação (BuildInfo.config) para seu projeto e colocá-lo na pasta de saída do projeto. O arquivo aparece como "*ProjectName*. Buildinfo. config"na pasta de saída, mas é renomeado"Buildinfo. config"na pasta de implantação depois de publicar seu aplicativo.

1.  Na **Gerenciador de soluções**, descarregue seu projeto web.

2.  Abra o arquivo de projeto (.csproj, .vbproj). Adicione as seguintes linhas:

    ```xml
    <!-- **************************************************** -->
    <!-- Build info -->
    <PropertyGroup>
       <!-- Generate the BuildInfo.config file -->
       <GenerateBuildInfoConfigFile>True</GenerateBuildInfoConfigFile>
       <!-- Include server name in build info -->
       <IncludeServerNameInBuildInfo>True</IncludeServerNameInBuildInfo>
       <!-- Include the symbols path so Visual Studio can find the matching deployed code when you start debugging. -->
       <BuildSymbolStorePath><path to symbols></BuildSymbolStorePath>
    </PropertyGroup>
    <!-- **************************************************** -->
    ```

3.  Faça check-in do arquivo de projeto atualizado.

4.  Execute uma nova compilação.

    Vá para [etapa 2: liberar seu aplicativo](#DeployRelease)

###  <a name="MSBuild"></a> Crie o manifesto de compilação para uma compilação manual usando MSBuild.exe
 Adicione estes argumentos de compilação ao executar uma compilação:

 **/p:GenerateBuildInfoConfigFile = true**

 **/p:IncludeServerNameInBuildInfo = true**

 **1&gt;/p:buildsymbolstorepath=&lt;1}&lt;{2&gt;caminho =**\<*para símbolos*>

##  <a name="DeployRelease"></a> Etapa 2: Liberar seu aplicativo
 Se você usar o [pacote Deploy](https://msdn.microsoft.com/library/dd394698.aspx) que foi criado pelo processo de compilação para implantar seu aplicativo, o manifesto de compilação é renomeado automaticamente de "*ProjectName*. Buildinfo. config"para"Buildinfo. config"e é colocado na mesma pasta com o arquivo de Web. config do seu aplicativo em seu servidor web.

 Se você usar outros métodos para implantar seu aplicativo, certifique-se de que o manifesto de compilação é renomeado de "*ProjectName*. Buildinfo. config"para"Buildinfo. config"e é colocado na mesma pasta com seu arquivo do aplicativo Web. config no servidor web.

## <a name="step-3-monitor-your-app"></a>Etapa 3: monitorar seu aplicativo
 Configure o monitoramento do desempenho de aplicativos no seu servidor Web para que você possa monitorar a ocorrência de problemas em seu aplicativo, registrar eventos de diagnóstico e salvar esses eventos em um arquivo de log do IntelliTrace. Ver [monitorar sua versão para problemas de implantação](../debugger/using-the-intellitrace-stand-alone-collector.md).

##  <a name="InvestigateEvents"></a> Etapa 4: Localizar o problema
 Será necessário o Visual Studio Enterprise no computador de desenvolvimento ou em outro computador para revisar os eventos registrados e depurar seu código usando o IntelliTrace. Você também pode usar ferramentas como CodeLens, mapas do depurador e mapas de código para ajudar no diagnóstico do problema.

### <a name="open-the-intellitrace-log-and-matching-solution"></a>Abrir o log do IntelliTrace e a solução correspondente

1.  Abra o log do IntelliTrace (arquivo. itrace) do Visual Studio Enterprise. Ou apenas duas vezes no arquivo, se você tiver o Visual Studio Enterprise no mesmo computador.

2.  Escolher **abrir solução** para fazer com que o Visual Studio abra automaticamente a solução ou projeto correspondente se o projeto não foi criado como parte de uma solução. [P: o log do IntelliTrace está faltando informações sobre meu aplicativo implantado. Por que isso ocorreu? O que devo fazer?](#InvalidConfigFile)

     O Visual Studio faz automaticamente um check-in particular de todas as alterações pendentes quando abre a solução ou o projeto correspondente. Para obter mais detalhes sobre esse check-in particular, examine os **saída** janela ou **Team Explorer**.

     Assim, antes de fazer qualquer alteração, confirme se você tem o código-fonte correto. Se você usa ramificação, pode estar trabalhando em uma ramificação diferente daquela em que o Visual Studio encontra o código-fonte, como sua ramificação de versão.

     ![Abra a solução de log do IntelliTrace](../debugger/media/ffr_itsummarypageopensolution.png "FFR_ITSummaryPageOpenSolution")

     Se você já tem um workspace mapeado para essa solução ou projeto, o Visual Studio seleciona esse workspace para colocar o código-fonte encontrado.

     ![Abrir do controle de origem para o espaço de trabalho mapeado](../debugger/media/ffr_openprojectfromsourcecontrol_mapped.png "FFR_OpenProjectFromSourceControl_Mapped")

     Caso contrário, escolha outro workspace ou crie um novo workspace. O Visual Studio mapeará a ramificação inteira para esse workspace.

     ![Abrir do controle de origem &#45; criar novo espaço de trabalho](../debugger/media/ffr_openprojectfromsourcecontrol_createnewworkspace.png "FFR_OpenProjectFromSourceControl_CreateNewWorkspace")

     Para criar um espaço de trabalho com mapeamentos específicos ou um nome que não é o nome do computador, escolha **gerenciar**.

     [P: por que o Visual Studio diz que meu espaço de trabalho selecionado é inelegível?](#IneligibleWorkspace)

     [P: por que não consigo continuar até escolher uma coleção de equipe ou uma coleção diferente?](#ChooseTeamProject)

### <a name="diagnose-a-performance-problem"></a>Diagnosticar um problema de desempenho

1.  Sob **violações de desempenho**, examine os eventos de desempenho gravados, tempo de execução total e outras informações de evento. Em seguida, verifique um pouco mais os métodos que foram chamados durante um evento de desempenho específico.

     ![Exibir detalhes de eventos de desempenho](../debugger/media/ffr_itsummarypageperformance.png "FFR_ITSummaryPagePerformance")

     Você também pode clicar duas vezes no evento.

2.  Na página de eventos, revise o tempo de execução dessas chamadas. Localize uma chamada lenta na árvore de execução.

     As chamadas mais lentas aparecem em sua própria seção quando você tem várias chamadas, aninhadas ou de outra maneira.

     Expanda essa chamada para revisar qualquer chamada aninhada e os valores gravados nesse momento. Em seguida, inicie a depuração dessa chamada.

     ![Iniciar a depuração de chamada de método](../debugger/media/ffr_itsummarypageperformancemethodscalled.png "FFR_ITSummaryPagePerformanceMethodsCalled")

     Você também pode clicar duas vezes na chamada.

     Se o método estiver no código do aplicativo, o Visual Studio irá para esse método.

     ![Vá para o código do aplicativo do evento de desempenho](../debugger/media/ffr_itsummarypageperformancegotocode.png "FFR_ITSummaryPagePerformanceGoToCode")

     Agora você pode revisar outros valores gravados, a pilha de chamadas, depurar seu código, ou usar o **IntelliTrace** janela [mover com versões anteriores ou encaminhará "no tempo" entre outros métodos](../debugger/intellitrace.md) que foram chamados durante Esse evento de desempenho.

    - [O que é todos esses outros eventos e informações no log do IntelliTrace?](../debugger/using-saved-intellitrace-data.md)
    - [O que mais posso fazer aqui?](#WhatElse)
    - [Deseja obter mais informações sobre eventos de desempenho?](https://blogs.msdn.microsoft.com/devops/2013/09/20/performance-details-in-intellitrace/)

### <a name="diagnose-an-exception"></a>Diagnosticar uma exceção

1.  Sob **dados de exceção**, examine os eventos de exceção gravados, seus tipos, mensagens, e quando as exceções aconteceram. Para se aprofundar no código, comece com a depuração do evento mais recente em um grupo de exceções.

     ![Iniciar a depuração de eventos de exceção](../debugger/media/ffr_itsummarypageexception.png "FFR_ITSummaryPageException")

     Você também pode clicar duas vezes no evento.

     Se a exceção ocorreu no código do aplicativo, o Visual Studio irá para o local onde a exceção ocorreu.

     ![Vá para o código do aplicativo de um evento de exceção](../debugger/media/ffr_itsummarypageexceptiongotocode.png "FFR_ITSummaryPageExceptionGoToCode")

     Agora você pode revisar outros valores gravados, a pilha de chamadas, ou usar o **IntelliTrace** janela [mover com versões anteriores ou encaminhará "no tempo" entre outros eventos gravados](../debugger/intellitrace.md), código relacionado e os valores registrados em Esses pontos no tempo.

     [O que é todos esses outros eventos e informações no log do IntelliTrace?](../debugger/using-saved-intellitrace-data.md)

###  <a name="WhatElse"></a> O que mais posso fazer aqui?

-   [Obter mais informações sobre esse código](../ide/find-code-changes-and-other-history-with-codelens.md). Para localizar referências a esse código, seu histórico de alterações, bugs relacionados, itens de trabalho, revisões de código ou testes de unidade – tudo sem sair do editor - usam os indicadores CodeLens no editor.

     ![CodeLens &#45; exibir as referências a esse código](../debugger/media/ffr_itsummarypageperformancecodelensreferences.png "FFR_ITSummaryPagePerformanceCodeLensReferences")

     ![CodeLens &#45; Exibir histórico de alterações para esse código](../debugger/media/ffr_itsummarypageperformancecodelensauthors.png "FFR_ITSummaryPagePerformanceCodeLensAuthors")

-   [Mapeie seu local no código enquanto você estiver depurando.](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md) Para acompanhar visualmente os métodos que foram chamados durante a sessão de depuração, mapeie a pilha de chamadas.

     ![Mapear a pilha de chamadas durante a depuração](../debugger/media/ffr_itsummarypageperformancedebuggermap.png "FFR_ITSummaryPagePerformanceDebuggerMap")

###  <a name="FAQ"></a> Perguntas e respostas

####  <a name="WhyInclude"></a> P: por que incluem informações sobre meu projeto, controle do código-fonte, compilação e símbolos com minha liberação?
 O Visual Studio usa essas informações para encontrar a solução e o código-fonte correspondentes para a versão que está tentando depurar. Após abrir o log do IntelliTrace e selecionar um evento para iniciar a depuração, o Visual Studio usa símbolos para encontrar e mostrar o código onde ocorreu o evento. Você pode então visualizar os valores que estão registrados e avançar ou retornar através da execução do seu código.

 Se você estiver usando o TFS e essas informações não estiverem no manifesto de compilação (Buildinfo config), Visual Studio procura o código-fonte correspondente e os símbolos o TFS atualmente conectado. Você recebe uma solicitação para escolher um TFS diferente caso o Visual Studio não encontre o TFS correto ou o código-fonte correspondente.

####  <a name="InvalidConfigFile"></a> P: o log do IntelliTrace está faltando informações sobre meu aplicativo implantado. Por que isso ocorreu? O que devo fazer?
 Isso pode ter acontecer quando ao implantar do seu computador de desenvolvimento ou quando não está conectado ao TFS durante a implantação.

1.  Vá para sua pasta de implantação do projeto.

2.  Encontre e abra o manifesto de compilação (BuildInfo.config file).

3.  Certifique-se de que o arquivo tem as informações necessárias:

- **ProjectName**

   O nome de seu projeto no Visual Studio. Por exemplo:

  ```xml
  <ProjectName>FabrikamFiber.Extranet.Web</ProjectName>
  ```

- **SourceControl**

- Informações sobre seu sistema de controle do código-fonte e as seguintes propriedades necessárias:

  - **TFS**

    - **{1&gt;projectcollectionuri&lt;1**: O URI para sua coleção de projeto e o Team Foundation Server

    - **{1&gt;projectitemspec&lt;1**: O caminho para o arquivo de projeto do seu aplicativo (. csproj ou. vbproj)

    - **{1&gt;projectversionspec&lt;1**: A versão do seu projeto

      Por exemplo:

    ```xml
    <SourceControl type="TFS">
       <TfsSourceControl>
          <ProjectCollectionUri>http://fabrikamfiber:8080/tfs/FabrikamFiber</ProjectCollectionUri>
          <ProjectItemSpec>$/WorkInProgress/FabrikamFiber/FabrikamFiber.CallCenter/FabrikamFiber.Web/FabrikamFiber.Web.csproj</ProjectItemSpec>
          <ProjectVersionSpec>LFabrikamFiber_BuildAndPublish_20130813@$/WorkInProgress</ProjectVersionSpec>
       </TfsSourceControl>
    </SourceControl>
    ```

  - **Git**

    - **{1&gt;gitsourcecontrol&lt;1**: O local do **GitSourceControl** esquema

    - **{1&gt;repositoryurl&lt;1**: O URI para seu Team Foundation Server, a coleção de projeto e o repositório Git

    - **ProjectPath**: O caminho para o arquivo de projeto do seu aplicativo (. csproj ou. vbproj)

    - **CommitId**: A id para a sua confirmação

      Por exemplo:

    ```xml
    <SourceControl type="Git">
       <GitSourceControl xmlns="http://schemas.microsoft.com/visualstudio/deploymentevent_git/2013/09">
          <RepositoryUrl>http://gittf:8080/tfs/defaultcollection/_git/FabrikamFiber</RepositoryUrl>
          <ProjectPath>/FabrikamFiber.CallCenter/FabrikamFiber.Web/FabrikamFiber.Web.csproj</ProjectPath>
          <CommitId>50662c96502dddaae5cd5ced962d9f14ec5bc64d</CommitId>
       </GitSourceControl>
    </SourceControl>
    ```

- **Build**

   Informações sobre seu sistema de compilação, `"TeamBuild"` ou `"MSBuild"` e as seguintes propriedades necessárias:

  - **{1&gt;buildlabel&lt;1** (para TeamBuild): O nome da compilação e o número. Esse rótulo também é usado como o nome do evento de implantação. Para obter mais informações sobre números de compilação, consulte [Use números para dar nomes significativos a compilações concluídas de compilação](/azure/devops/pipelines/build/options?view=vsts).

  - **SymbolPath** (recomendado): A lista de URIs para os locais de símbolos (arquivo PDB) separados por ponto e vírgula. Esses URIs podem ser URLs ou UNCs (caminhos de rede). Isso facilita para o Visual Studio encontrar os símbolos correspondentes para ajudar com sua depuração.

  - **{1&gt;buildreporturl&lt;1** (para TeamBuild): O local do relatório de compilação no TFS

  - **{1&gt;BuildID&lt;1** (para TeamBuild): O URI para a compilação detalhes no TFS. Esse URI também é usado como a ID do evento de implantação. Deve ser uma ID exclusiva caso não esteja usando o TeamBuild.

  - **{1&gt;builtsolution&lt;1**: O caminho para o arquivo de solução que o Visual Studio usa para localizar e abrir a solução correspondente. Este é o conteúdo do **SolutionPath** propriedade do MsBuild.

    Por exemplo:

  - **TFS**

    ```xml
    <Build type="TeamBuild">
       <MsBuild>
          <BuildLabel kind="label">FabrikamFiber_BuildAndPublish_20130813.1</BuildLabel>
          <SymbolPath>\\fabrikamfiber\FabrikamFiber.CallCenter\Symbols</SymbolPath>
          <BuildReportUrl kind="informative, url" url="http://fabrikamfiber:8080/tfs/FabrikamFiber/_releasePipeline/FindRelease?buildUri=fabrikamfiber%3a%2f%2f%2fBuild%2fBuild%2f448">Build Report Url</BuildReportUrl>
          <BuildId kind="id">1c4444d2-518d-4673-a590-dce2773c7744,fabrikamfiber:///Build/Build/448</BuildId>
          <BuiltSolution>$/WorkInProgress/FabrikamFiber/FabrikamFiber.CallCenter/FabrikamFiber.CallCenter.sln</BuiltSolution>
       </MsBuild>
    </Build>
    ```

  - **Git**

    ```xml
    <Build type="MSBuild">
       <MSBuild>
          <SymbolPath>\\gittf\FabrikamFiber.CallCenter\Symbols</SymbolPath>
          <BuiltSolution>/FabrikamFiber.CallCenter/FabrikamFiber.CallCenter.sln</BuiltSolution>
       </MSBuild>
    </Build>
    ```

####  <a name="IneligibleWorkspace"></a> P: por que o Visual Studio diz que meu espaço de trabalho selecionado é inelegível?
 **R:** espaço de trabalho selecionado não tem mapeamento entre a pasta de controle do código-fonte e uma pasta local. Para criar um mapeamento para esse espaço de trabalho, escolha **gerenciar**. Caso contrário, escolha um workspace já mapeado ou crie um novo workspace.

 ![Abrir do controle de origem com nenhum espaço de trabalho mapeado](../debugger/media/ffr_openprojectfromsourcecontrol_notmapped.png "FFR_OpenProjectFromSourceControl_NotMapped")

####  <a name="ChooseTeamProject"></a> P: por que não consigo continuar até escolher uma coleção de equipe ou uma coleção diferente?
 **R:** isso pode acontecer por qualquer um destes motivos:

-   O Visual Studio não está conectado ao TFS.

     ![Abrir do controle de origem &#45; não conectado](../debugger/media/ffr_openprojectfromsourcecontrol_notconnected.png "FFR_OpenProjectFromSourceControl_NotConnected")

-   O Visual Studio não encontrou a solução ou o projeto em sua coleção de equipe atual.

     Quando o arquivo de manifesto de compilação (\<*ProjectName*>. Buildinfo) não especifica onde o Visual Studio pode encontrar o código-fonte correspondente, o Visual Studio usa o TFS atualmente conectado para localizar a solução ou projeto correspondente. Se sua coleção de equipe atual não tiver o código-fonte correspondente, o Visual Studio solicitará que você se conecte a uma coleção de equipe diferente.

-   Visual Studio não encontrou a solução ou projeto na coleção especificada pelo arquivo de manifesto de compilação (\<*ProjectName*>. Buildinfo).

     O TFS especificado pode não ter mais o código-fonte compatível ou nem mesmo existir, talvez porque você migrou para um novo TFS. Se o TFS especificado não existir, o Visual Studio poderá atingir o tempo limite depois de cerca de um minuto e depois será solicitado que você se conecte a uma coleção diferente. Para prosseguir, conecte-se ao servidor TFS correto.

     ![Abrir do controle de origem &#45; migrado](../debugger/media/ffr_openprojectfromsourcecontrol_migrated.png "FFR_OpenProjectFromSourceControl_Migrated")

####  <a name="WhatWorkspace"></a> P: o que é um espaço de trabalho?
 **R:** sua [espaço de trabalho armazena uma cópia da fonte de](/azure/devops/repos/tfvc/create-work-workspaces?view=vsts) para que você possa desenvolver e testá-lo separadamente antes de verificação no seu trabalho. Se você ainda não tem um workspace mapeado especificamente para a solução ou o projeto encontrado, o Visual Studio solicitará a escolha de um workspace disponível ou a criação de um novo workspace com o nome do computador como o nome padrão do workspace.

####  <a name="UntrustedSymbols"></a> P: por que eu recebo essa mensagem sobre símbolos não confiáveis?
 ![Depurar com o caminho de símbolos não confiáveis? ](../debugger/media/ffr_ituntrustedsymbolpaths.png "FFR_ITUntrustedSymbolPaths")

 **R:** esta mensagem aparece quando o caminho de símbolos no arquivo de manifesto de compilação (\<*ProjectName*>. Buildinfo) não está incluído na lista de caminhos confiáveis de símbolos. Você pode adicionar o caminho à lista de caminhos de símbolos nas opções do depurador.
