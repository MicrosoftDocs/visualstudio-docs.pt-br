---
title: Diagnosticar problemas após a implantação | Microsoft Docs
ms.date: 04/10/2018
ms.topic: how-to
ms.assetid: a3463eab-a352-4d17-8551-adbaad526db0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8a4ae5e4f6f21208f02cbfd6513b3c5eb28124a8
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350583"
---
# <a name="diagnose-problems-after-deployment-using-intellitrace-c-visual-basic"></a>Diagnosticar problemas após a implantação usando o IntelliTrace (C#, Visual Basic)

Para diagnosticar problemas no seu aplicativo da web ASP.NET após a implantação usando o IntelliTrace, inclua informações de compilação com a versão para permitir que o Visual Studio localize automaticamente os arquivos de origem e símbolos corretos que são necessárias para depurar o log do IntelliTrace.

 Se você estiver usando o Microsoft Monitoring Agent para controlar o IntelliTrace, também precisará configurar o monitoramento de desempenho do aplicativo no servidor da web. Ele registra eventos de diagnóstico enquanto seu aplicativo é executado e salva os eventos em um arquivo de log do IntelliTrace. Em seguida, você poderá observar os eventos no Visual Studio Enterprise (não nas edições Professional ou Community); vá para o código em que ocorreu o evento, observe os valores gravados naquele momento e avance ou retorne por meio do código executado. Depois de encontrar e resolver o problema, repita o ciclo apenas para compilar, liberar e monitorar seu aplicativo para que você possa corrigir problemas potenciais futuros o quanto antes e com mais rapidez.

 ![Código, compilação, versão, monitorar, diagnosticar, corrigir](../debugger/media/ffr_cycle.png "FFR_Cycle")

 **Você precisará de:**

- Visual Studio, Azure DevOps ou Team Foundation Server 2017, 2015, 2013, 2012 ou 2010 para configurar seu build

- Para monitorar seu aplicativo e registrar dados de diagnóstico use o Microsoft Monitoring Agent

- Visual Studio Enterprise (mas não as edições Professional ou Community) para examinar dados de diagnóstico e depurar seu código com o IntelliTrace

## <a name="step-1-include-build-information-with-your-release"></a><a name="SetUpBuild"></a> Etapa 1: Incluir informações de build com sua versão
 Configure seu processo de build para criar um manifesto de compilação (arquivo *BuildInfo.config*) de seu projeto Web e inclua esse manifesto em sua versão. Esse manifesto contém informações sobre o projeto, sobre o controle do código-fonte e o sistema de compilação utilizados para criar uma compilação específica. Essas informações ajudam o Visual Studio a encontrar o código-fonte e os símbolos correspondentes após abrir o log do IntelliTrace para revisar os eventos registrados.

### <a name="create-the-build-manifest-for-an-automated-build-using-team-foundation-server"></a><a name="AutomatedBuild"></a> Criar o manifesto de build de um build automatizado usando Team Foundation Server

 Siga essas etapas caso use Team Foundation Version Control ou Git.

#### <a name="azure-devops-and-team-foundation-server-2017"></a><a name="TFS2017"></a> Azure DevOps e Team Foundation Server 2017

O Visual Studio 2017 e versões posteriores não incluem o arquivo *Buildinfo*, que foi preterido e removido. Para depurar aplicativos Web ASP.NET após a implantação, use um dos seguintes métodos:

* Para implantação no Azure, use o [Application Insights](/azure/application-insights/).

* Se você precisar usar o IntelliTrace, abra o projeto no Visual Studio e carregue os arquivos de símbolos a partir do build correspondente. É possível carregar arquivos de símbolos pela janela **Módulos** ou por meio da configuração de símbolos em **Ferramentas** > **Opções** > **Depuração** > **Símbolos**.

#### <a name="team-foundation-server-2013"></a><a name="TFS2013"></a> Team Foundation Server 2013
 Configure seu pipeline de build para adicionar os locais de seu código-fonte, compilação e símbolos ao manifesto de compilação (arquivo BuildInfo.config). O Team Foundation Build automaticamente cria esse arquivo e coloca-o em sua pasta de saída do projeto.

1. [Edite seu pipeline de build ou crie um novo pipeline de build.](/azure/devops/pipelines/get-started-designer?view=vsts)

     ![Exibir pipeline de compilação no TFS 2013](../debugger/media/ffr_tfs2013viewbuilddefinition.png "FFR_TFS2013ViewBuildDefinition")

2. Escolha o modelo padrão (TfvcTemplate.12.xaml) ou seu próprio modelo personalizado.

     ![Escolha o modelo de processo de compilação &#45; TFS 2013](../debugger/media/ffr_tfs2013buildprocesstemplate.png "FFR_TFS2013BuildProcessTemplate")

3. Especifique onde salvar o arquivo de símbolos (PDB) de forma que o código-fonte seja indexado automaticamente.

     Se você usar um modelo personalizado, verifique se o modelo tem uma atividade para indexar o código-fonte. Posteriormente, adicione um argumento de MSBuild para especificar onde salvar o arquivo de símbolos.

     ![Configurar o caminho de símbolos no pipeline de compilação TFS 2013](../debugger/media/ffr_tfs2013builddefsymbolspath.png "FFR_TFS2013BuildDefSymbolsPath")

     Para obter mais informações sobre símbolos, confira [Publicar dados de símbolos](/azure/devops/pipelines/tasks/build/index-sources-publish-symbols?view=vsts).

4. Adicione este argumento de MSBuild para incluir os locais do TFS e de símbolos ao arquivo de manifesto da compilação:

     **/p:IncludeServerNameInBuildInfo=True**

     Qualquer um que possa acessar seu servidor Web pode ver esses locais no manifesto de compilação. Certifique-se de que o servidor de código-fonte é seguro.

5. Se você usa um modelo personalizado, adicione este argumento de MSBuild para especificar onde salvar o arquivo de símbolos:

     **/p: BuildSymbolStorePath =**\<*path to symbols*>

     ![Incluir informações do servidor de compilação em Build def TFS 2013](../debugger/media/ffr_tfs2013builddefincludeserverinfo.png "FFR_TFS2013BuildDefIncludeServerInfo")

     E adicione estas linhas ao arquivo de seu projeto da Web (.csproj, .vbproj):

    ```xml
    <!-- Import the targets file. Change the folder location as necessary. -->
       <Import Project=""$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v$(VisualStudioVersion)\BuildInfo\Microsoft.VisualStudio.ReleaseManagement.BuildInfo.targets" />

    ```

     Qualquer um que possa acessar seu servidor Web pode ver esses locais no manifesto de compilação. Certifique-se de que o servidor de código-fonte é seguro.

6. Execute uma nova compilação.

    Vá para [etapa 2: liberar seu aplicativo](#DeployRelease)

#### <a name="team-foundation-server-2012-or-2010"></a><a name="TFS2012_2010"></a> Team Foundation Server 2012 ou 2010
 Siga estas etapas para criar automaticamente o arquivo de manifesto de compilação (BuildInfo.config) para seu projeto e colocá-lo na pasta de saída do projeto. O arquivo aparece como "*ProjectName*.BuildInfo.config" na pasta de saída, mas é renomeado "BuildInfo.config" na pasta de implantação, após publicar seu aplicativo.

1. Instale o Visual Studio 2013 (qualquer edição) no servidor do Team Foundation Build.

2. No pipeline de build, especifique onde salvar os símbolos de forma que o código-fonte seja indexado automaticamente.

     Se você usar um modelo personalizado, verifique se o modelo tem uma atividade para indexar o código-fonte.

3. Adicionar estes argumentos de MSBuild ao pipeline de build:

    - **/p:VisualStudioVersion=12.0**

    - **/p:MSBuildAssemblyVersion=12.0**

    - **/tv:12.0**

    - **/p:IncludeServerNameInBuildInfo=True**

    - **/p: BuildSymbolStorePath =**\<*path to symbols*>

4. Execute uma nova compilação.

    Vá para [etapa 2: liberar seu aplicativo](#DeployRelease)

### <a name="create-the-build-manifest-for-a-manual-build-using-visual-studio"></a><a name="ManualBuild"></a> Criar o manifesto de build para um build manual usando o Visual Studio
 Siga estas etapas para criar automaticamente o arquivo de manifesto de compilação (BuildInfo.config) para seu projeto e colocá-lo na pasta de saída do projeto. O arquivo aparece como "*ProjectName*.BuildInfo.config" na pasta de saída, mas é renomeado "BuildInfo.config" na pasta de implantação, após publicar seu aplicativo.

1. No **Gerenciador de Soluções**, descarregue seu projeto Web.

2. Abra o arquivo de projeto (.csproj, .vbproj). Adicione as seguintes linhas:

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

3. Faça check-in do arquivo de projeto atualizado.

4. Execute uma nova compilação.

    Vá para [etapa 2: liberar seu aplicativo](#DeployRelease)

### <a name="create-the-build-manifest-for-a-manual-build-using-msbuildexe"></a><a name="MSBuild"></a> Criar o manifesto de build para um build manual usando o MSBuild.exe
 Adicione estes argumentos de compilação ao executar uma compilação:

 **/p:GenerateBuildInfoConfigFile=True**

 **/p:IncludeServerNameInBuildInfo=True**

 **/p: BuildSymbolStorePath =**\<*path to symbols*>

## <a name="step-2-release-your-app"></a><a name="DeployRelease"></a> Etapa 2: Liberar seu aplicativo
 Se você usa o [pacote Web.Deploy](https://msdn.microsoft.com/library/dd394698.aspx) que foi criado por seu processo de compilação para implantar seu aplicativo, o manifesto de compilação é renomeado automaticamente de "*ProjectName*.BuildInfo.config" para "BuildInfo.config" e é colocado na mesma pasta com seu arquivo Web.config do aplicativo no seu servidor Web.

 Se você usa outros métodos para implantar seu aplicativo, verifique se o manifesto de build foi renomeado de "*ProjectName*.BuildInfo.config" para "BuildInfo.config" e colocado na mesma pasta que seu arquivo Web.config do aplicativo no seu servidor Web.

## <a name="step-3-monitor-your-app"></a>Etapa 3: monitorar seu aplicativo
 Configure o monitoramento do desempenho de aplicativos no seu servidor Web para que você possa monitorar a ocorrência de problemas em seu aplicativo, registrar eventos de diagnóstico e salvar esses eventos em um arquivo de log do IntelliTrace. Confira [Monitoramento de problemas de implantação versão](../debugger/using-the-intellitrace-stand-alone-collector.md).

## <a name="step-4-find-the-problem"></a><a name="InvestigateEvents"></a> Etapa 4: Encontrar o problema
 Você precisará do Visual Studio Enterprise no seu computador de desenvolvimento ou em outro computador para revisar os eventos registrados e depurar seu código usando o IntelliTrace. Você também pode usar ferramentas como CodeLens, mapas do depurador e mapas de código para ajudar no diagnóstico do problema.

### <a name="open-the-intellitrace-log-and-matching-solution"></a>Abrir o log do IntelliTrace e a solução correspondente

1. Abra o log do IntelliTrace (.iTrace file) no Visual Studio Enterprise. Ou apenas clique duas vezes no arquivo se você tiver o Visual Studio Enterprise no mesmo computador.

2. Escolha **Abrir solução** para fazer com que o Visual Studio abra automaticamente a solução ou o projeto correspondente, caso o projeto não tenha sido compilado como parte de uma solução. [P: o log do IntelliTrace tem informações ausentes sobre o meu aplicativo implantado. Por que isso aconteceu? O que devo fazer?](#InvalidConfigFile)

     O Visual Studio faz automaticamente um check-in particular de todas as alterações pendentes quando abre a solução ou o projeto correspondente. Para obter mais detalhes sobre esse check-in particular, procure na janela de **Saída** ou no **Team Explorer**.

     Assim, antes de fazer qualquer alteração, confirme se você tem o código-fonte correto. Se você usa ramificação, pode estar trabalhando em uma ramificação diferente daquela em que o Visual Studio encontra o código-fonte, como sua ramificação de versão.

     ![Abrir solução do log do IntelliTrace](../debugger/media/ffr_itsummarypageopensolution.png "FFR_ITSummaryPageOpenSolution")

     Se você já tem um workspace mapeado para essa solução ou projeto, o Visual Studio seleciona esse workspace para colocar o código-fonte encontrado.

     ![Abrir do controle do código-fonte para o espaço de trabalho mapeado](../debugger/media/ffr_openprojectfromsourcecontrol_mapped.png "FFR_OpenProjectFromSourceControl_Mapped")

     Caso contrário, escolha outro workspace ou crie um novo workspace. O Visual Studio mapeará a ramificação inteira para esse workspace.

     ![Abrir do controle do código-fonte &#45; criar novo espaço de trabalho](../debugger/media/ffr_openprojectfromsourcecontrol_createnewworkspace.png "FFR_OpenProjectFromSourceControl_CreateNewWorkspace")

     Para criar um workspace com mapeamentos específicos ou com um nome que não seja o nome do computador, escolha **Gerenciar**.

     [P: Por que o Visual Studio indica que meu workspace selecionado não é qualificado?](#IneligibleWorkspace)

     [P: por que não posso continuar até escolher uma coleção de equipe ou uma coleção diferente?](#ChooseTeamProject)

### <a name="diagnose-a-performance-problem"></a>Diagnosticar um problema de desempenho

1. Em **Violações de Desempenho**, revise os eventos de desempenho gravados, o tempo de execução total e outras informações dos eventos. Em seguida, verifique um pouco mais os métodos que foram chamados durante um evento de desempenho específico.

     ![Exibir detalhes do evento de desempenho](../debugger/media/ffr_itsummarypageperformance.png "FFR_ITSummaryPagePerformance")

     Você também pode clicar duas vezes no evento.

2. Na página de eventos, revise o tempo de execução dessas chamadas. Localize uma chamada lenta na árvore de execução.

     As chamadas mais lentas aparecem em sua própria seção quando você tem várias chamadas, aninhadas ou de outra maneira.

     Expanda essa chamada para revisar qualquer chamada aninhada e os valores gravados nesse momento. Em seguida, inicie a depuração dessa chamada.

     ![Iniciar a depuração da chamada de método](../debugger/media/ffr_itsummarypageperformancemethodscalled.png "FFR_ITSummaryPagePerformanceMethodsCalled")

     Você também pode clicar duas vezes na chamada.

     Se o método estiver no código do aplicativo, o Visual Studio irá para esse método.

     ![Ir para o código do aplicativo do evento de desempenho](../debugger/media/ffr_itsummarypageperformancegotocode.png "FFR_ITSummaryPagePerformanceGoToCode")

     Agora você pode revisar outros valores gravados, a pilha de chamadas, navegar por código, ou usar a janela do **IntelliTrace** para [avançar ou retornar "no tempo" entre outros métodos](../debugger/intellitrace.md) que foram chamados durante esse evento de desempenho.

    - [O que são todos esses outros eventos e informações no log do IntelliTrace?](../debugger/using-saved-intellitrace-data.md)
    - [O que mais posso fazer aqui?](#WhatElse)
    - [Deseja obter mais informações sobre eventos de desempenho?](https://devblogs.microsoft.com/devops/performance-details-in-intellitrace/)

### <a name="diagnose-an-exception"></a>Diagnosticar uma exceção

1. Em **Dados da Exceção**, revise os eventos de exceção gravados, seus tipos, mensagens e quando as exceções aconteceram. Para se aprofundar no código, comece com a depuração do evento mais recente em um grupo de exceções.

     ![Iniciar Depuração do evento de exceção](../debugger/media/ffr_itsummarypageexception.png "FFR_ITSummaryPageException")

     Você também pode clicar duas vezes no evento.

     Se a exceção ocorreu no código do aplicativo, o Visual Studio irá para o local onde a exceção ocorreu.

     ![Ir para o código do aplicativo a partir de um evento de exceção](../debugger/media/ffr_itsummarypageexceptiongotocode.png "FFR_ITSummaryPageExceptionGoToCode")

     Agora você pode revisar outros valores gravados, a pilha de chamadas, ou usar a janela do **IntelliTrace** para [avançar ou retornar "no tempo" entre outros eventos gravados](../debugger/intellitrace.md), o código relativo e os valores gravados nesses momentos.

     [O que são todos esses outros eventos e informações no log do IntelliTrace?](../debugger/using-saved-intellitrace-data.md)

### <a name="what-else-can-i-do-from-here"></a><a name="WhatElse"></a>O que mais posso fazer aqui?

- [Obtenha mais informações sobre esse código](../ide/find-code-changes-and-other-history-with-codelens.md). Para encontrar referências para esse código, seu histórico de alterações, bugs relacionados, itens de trabalho, análises do código ou testes de unidade – tudo isso sem sair do editor – use os indicadores do CodeLens no editor.

     ![CodeLens &#45; exibir referências a este código](../debugger/media/ffr_itsummarypageperformancecodelensreferences.png "FFR_ITSummaryPagePerformanceCodeLensReferences")

     ![CodeLens &#45; exibir o histórico de alterações para este código](../debugger/media/ffr_itsummarypageperformancecodelensauthors.png "FFR_ITSummaryPagePerformanceCodeLensAuthors")

- [Mapeie seu local no código enquanto estiver depurando.](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md) Para acompanhar visualmente os métodos que foram chamados durante a sessão de depuração, mapeie a pilha de chamadas.

     ![Mapear a pilha de chamadas durante a depuração](../debugger/media/ffr_itsummarypageperformancedebuggermap.png "FFR_ITSummaryPagePerformanceDebuggerMap")

### <a name="q--a"></a><a name="FAQ"></a>P & A

#### <a name="q-why-include-information-about-my-project-source-control-build-and-symbols-with-my-release"></a><a name="WhyInclude"></a> P: Por que incluir informações sobre meu projeto, controle do código-fonte, build e símbolos com minha liberação?
 O Visual Studio usa essas informações para encontrar a solução e o código-fonte correspondentes para a versão que está tentando depurar. Após abrir o log do IntelliTrace e selecionar um evento para iniciar a depuração, o Visual Studio usa símbolos para encontrar e mostrar o código onde ocorreu o evento. Você pode então visualizar os valores que estão registrados e avançar ou retornar através da execução do seu código.

 Se estiver usando o TFS e essas informações não estiverem no manifesto de build (BuildInfo.config file), o Visual Studio procurará o código-fonte e os símbolos correspondentes em seu TFS conectado no momento. Você recebe uma solicitação para escolher um TFS diferente caso o Visual Studio não encontre o TFS correto ou o código-fonte correspondente.

#### <a name="q-the-intellitrace-log-is-missing-information-about-my-deployed-app-why-did-this-happen-what-do-i-do"></a><a name="InvalidConfigFile"></a> P: O log do IntelliTrace não contém todas as informações sobre meu aplicativo implantado. Por que isso ocorreu? O que devo fazer?
 Isso pode ter acontecer quando ao implantar do seu computador de desenvolvimento ou quando não está conectado ao TFS durante a implantação.

1. Vá para sua pasta de implantação do projeto.

2. Encontre e abra o manifesto de compilação (BuildInfo.config file).

3. Certifique-se de que o arquivo tem as informações necessárias:

- **ProjectName**

   O nome de seu projeto no Visual Studio. Por exemplo:

  ```xml
  <ProjectName>FabrikamFiber.Extranet.Web</ProjectName>
  ```

- **SourceControl**

- Informações sobre seu sistema de controle do código-fonte e as seguintes propriedades necessárias:

  - **TFS**

    - **ProjectCollectionUri**: o URI para seu Team Foundation Server e coleção de projetos

    - **ProjectItemSpec**: o caminho para seu arquivo de projeto do aplicativo (.csproj ou .vbproj)

    - **ProjectVersionSpec**: a versão para seu projeto

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

    - **GitSourceControl**: o local de esquema de **GitSourceControl**

    - **RepositoryUrl**: o URI para seu Team Foundation Server, a coleção de projetos e o repositório Git

    - **ProjectPath**: o caminho para seu arquivo de projeto do aplicativo (.csproj ou .vbproj)

    - **ConfirmID**: a ID da confirmação

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

- **Compilar**

   Informações sobre seu sistema de compilação, `"TeamBuild"` ou `"MSBuild"` e as seguintes propriedades necessárias:

  - **BuildLabel** (para TeamBuild): o nome e o número do build. Esse rótulo também é usado como o nome do evento de implantação. Para saber mais sobre números de build, veja [Usar números de build para dar nomes significativos a buils concluídos](/azure/devops/pipelines/build/options?view=vsts).

  - **SymbolPath** (Recomendado): a lista dos URIs dos locais de seus símbolos (arquivo PDB) separados por ponto-e-vírgula. Esses URIs podem ser URLs ou UNCs (caminhos de rede). Isso facilita para o Visual Studio encontrar os símbolos correspondentes para ajudar com sua depuração.

  - **BuildReportUrl** (para TeamBuild): o local do relatório de build no TFS

  - **BuildId** (para TeamBuild): o URI para os detalhes do built no TFS. Esse URI também é usado como a ID do evento de implantação. Essa ID deve ser exclusiva se você não estiver usando TeamBuild.

  - **BuiltSolution**: o caminho para seu arquivo de solução que o Visual Studio usa para localizar e abrir a solução correspondente. Esse é o conteúdo da propriedade **SolutionPath** do MsBuild.

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

#### <a name="q-why-does-visual-studio-say-my-selected-workspace-is-ineligible"></a><a name="IneligibleWorkspace"></a>P: por que o Visual Studio diz que meu espaço de trabalho selecionado não é elegível?
 **R:** O workspace selecionado não tem nenhum mapeamento entre a pasta do controle do código-fonte e uma pasta local. Para criar um mapeamento para esse workspace, escolha **Gerenciar**. Caso contrário, escolha um workspace já mapeado ou crie um novo workspace.

 ![Abrir do controle do código-fonte sem nenhum espaço de trabalho mapeado](../debugger/media/ffr_openprojectfromsourcecontrol_notmapped.png "FFR_OpenProjectFromSourceControl_NotMapped")

#### <a name="q-why-cant-i-continue-until-i-choose-a-team-collection-or-a-different-collection"></a><a name="ChooseTeamProject"></a> P: Por que não consigo continuar até escolher uma coleção de equipe ou uma coleção diferente?
 **R:** Isso pode acontecer por um destes motivos:

- O Visual Studio não está conectado ao TFS.

     ![Abrir do controle do código-fonte &#45; não conectado](../debugger/media/ffr_openprojectfromsourcecontrol_notconnected.png "FFR_OpenProjectFromSourceControl_NotConnected")

- O Visual Studio não encontrou a solução ou o projeto em sua coleção de equipe atual.

     Quando o arquivo de manifesto de compilação ( \<*ProjectName*>.BuildInfo.config) não especifica onde o Visual Studio pode encontrar a fonte correspondente, o Visual Studio usa o TFS atualmente conectado para localizar a solução ou o projeto de correspondência. Se sua coleção de equipe atual não tiver o código-fonte correspondente, o Visual Studio solicitará que você se conecte a uma coleção de equipe diferente.

- O Visual Studio não encontrou a solução ou o projeto na coleção especificada pelo arquivo de manifesto de compilação ( \<*ProjectName*>.BuildInfo.config).

     O TFS especificado pode não ter mais o código-fonte compatível ou nem mesmo existir, talvez porque você migrou para um novo TFS. Se o TFS especificado não existir, o Visual Studio poderá atingir o tempo limite depois de cerca de um minuto e depois será solicitado que você se conecte a uma coleção diferente. Para prosseguir, conecte-se ao servidor TFS correto.

     ![Abrir do controle do código-fonte &#45; migrado](../debugger/media/ffr_openprojectfromsourcecontrol_migrated.png "FFR_OpenProjectFromSourceControl_Migrated")

#### <a name="q-whats-a-workspace"></a><a name="WhatWorkspace"></a> P: O que é um workspace?
 **R:** Seu [workspace armazena uma cópia do código-fonte](/azure/devops/repos/tfvc/create-work-workspaces?view=vsts), de modo que você possa desenvolvê-lo e testá-lo separadamente antes de fazer check-in do trabalho. Se você ainda não tem um workspace mapeado especificamente para a solução ou o projeto encontrado, o Visual Studio solicitará a escolha de um workspace disponível ou a criação de um novo workspace com o nome do computador como o nome padrão do workspace.

#### <a name="q-why-do-i-get-this-message-about-untrusted-symbols"></a><a name="UntrustedSymbols"></a> P: Por que recebo esta mensagem sobre símbolos não confiáveis?
 ![Depurar com caminho de símbolos não confiáveis?](../debugger/media/ffr_ituntrustedsymbolpaths.png "FFR_ITUntrustedSymbolPaths")

 **R:** Essa mensagem é exibida quando o caminho dos símbolos no arquivo de manifesto de compilação ( \<*ProjectName*>.BuildInfo.config) não está incluído na lista de caminhos de símbolo confiáveis. Você pode adicionar o caminho à lista de caminhos de símbolos nas opções do depurador.
