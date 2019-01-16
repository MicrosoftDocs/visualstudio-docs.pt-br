---
title: Usando dados salvos do IntelliTrace | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.historicaldebug.norepro
helpviewer_keywords:
- iTrace files
- IntelliTrace, log files
- IntelliTrace log files
- .iTrace files
ms.assetid: 9f2cce86-345a-4e22-84ba-91542d81e67a
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: c348bc105d997e07dcbc6ee373c2952e16c572cf
ms.sourcegitcommit: 01185dadd2fa1f9a040d2a366869f1a5e1d18e0f
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2019
ms.locfileid: "54227779"
---
# <a name="using-saved-intellitrace-data-c-visual-basic-c"></a>Usando dados salvos do IntelliTrace (C#, Visual Basic, C++)

Vá para os pontos específicos da execução do aplicativo quando você iniciar a depuração de um arquivo de log do IntelliTrace (.iTrace). Esse arquivo pode conter eventos de desempenho, exceções, threads, etapas de teste, módulos e outras informações do sistema que o IntelliTrace registra durante a execução do seu aplicativo.

 Certifique-se de que você tenha:

-   Arquivos de origem e arquivos de símbolo (.pdb) compatíveis com seu código de aplicativo. Caso contrário, o Visual Studio não pode resolver os locais de origem e mostra a mensagem "Símbolos não encontrados". Ver [especificar arquivos de símbolo (. PDB) e código-fonte](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md) e [diagnosticar problemas após a implantação](../debugger/diagnose-problems-after-deployment.md).

-   Visual Studio Enterprise (mas não no Professional ou Community edições) no seu computador de desenvolvimento ou em outro computador para abrir arquivos. itrace

-   Um arquivo .iTrace de uma destas origens:

    |**Source**|**Confira**|
    |----------------|-------------|
    |Uma sessão do IntelliTrace no Visual Studio Enterprise (mas não Professional ou Community edições)|[Recursos do IntelliTrace](../debugger/intellitrace-features.md)|
    |Uma sessão de teste no Microsoft Test Manager. Isso anexa um arquivo .iTrace a um item de trabalho do Team Foundation Server.|[Coletar mais dados de diagnóstico em testes manuais](/azure/devops/test/mtm/collect-more-diagnostic-data-in-manual-tests?view=vsts)|
    |Microsoft Monitoring Agent, sozinho ou com o System Center 2012 R2 Operations Manager, para aplicativos Web do ASP.NET e aplicativos do SharePoint em execução na implantação|-   [Diagnosticar problemas após a implantação](../debugger/diagnose-problems-after-deployment.md)<br />-   [Novidades do System Center 2012 R2 Operations Manager](http://technet.microsoft.com/library/dn249700.aspx)|

##  <a name="GetStarted"></a> O que você deseja fazer?

-   [Abrir um log do IntelliTrace](#Open)

-   [Noções básicas sobre o log do IntelliTrace](#Understand)

-   [Iniciar depuração a partir de um log do IntelliTrace](#StartDebugging)

##  <a name="Open"></a> Abrir um log do IntelliTrace
 Em um computador com o Visual Studio Enterprise, abra o arquivo. itrace.

-   Clique duas vezes no arquivo .iTrace fora do Visual Studio ou abra o arquivo de dentro do Visual Studio.

     \- ou -

-   Se o arquivo .iTrace estiver anexado a um item de trabalho do Team Foundation Server, siga estas etapas no item de trabalho:

    -   Em **Todos os Links**, localize o arquivo .iTrace. Abra-o.

         \- ou -

    -   Em **Etapas de Reprodução**, escolha o link **IntelliTrace**.

> [!TIP]
>  Se você fechou o arquivo IntelliTrace durante a depuração, poderá reabri-lo facilmente. Vá para o menu **Depurar**, escolha **IntelliTrace**, **Mostrar Resumo do Log**. Você também pode escolher **Mostrar Resumo do Log** na janela **IntelliTrace**. Isso só estará disponível durante a depuração com o IntelliTrace.

##  <a name="Understand"></a> Noções básicas sobre o log do IntelliTrace
 Algumas das seções a seguir no arquivo .iTrace só aparecerão se você tiver coletado dados de uma origem em particular, por exemplo, do Test Manager ou aplicativos do SharePoint.

|**Section**|**Contém**|**Origem de coleta**|
|-----------------|------------------|---------------------------|
|[Violações de desempenho](#Performance)|Eventos de desempenho com chamadas de função que excedam o limite configurado|Microsoft Monitoring Agent, o coletor autônomo ou com o System Center 2012 R2 Operations Manager para aplicativos web do ASP.NET hospedados no IIS|
|[Dados de exceção](#ExceptionData)|Exceções, incluindo toda a pilha de chamadas para cada exceção|Todas as fontes|
|[Análise](#Analysis)|Somente para aplicativos do SharePoint 2010 e do SharePoint 2013. Diagnostique eventos do IntelliTrace e do SharePoint, como eventos do depurador, eventos de ULS, exceções não identificadas e outros dados que o Microsoft Monitoring Agent registrou.|Microsoft Monitoring Agent, o coletor autônomo ou com o System Center 2012 R2 Operations Manager|
|[Informações do sistema](#SystemInfo)|Configurações e especificações do sistema host|Todas as fontes|
|[Lista de threads](#ThreadsList)|Threads executados durante a coleta|Todas as fontes|
|[Dados de teste](#TestData)|Etapas de teste e seus resultados de uma sessão de teste|Test Manager|
|[Módulos](#Modules)|Módulos que o processo de destino carregou na ordem em que foram carregados.|Todas as fontes|
|[Solicitação da Web](#Modules)|Dados de solicitação da Web para produção IIS aplicativos web e SharePoint 2010 e SharePoint 2013|Microsoft Monitoring Agent e o coletor autônomo|

 Aqui estão algumas dicas para ajudar a localizar informações sobre cada seção:

-   Escolha um cabeçalho de coluna para classificar dados.

-   Use a caixa de pesquisa para filtrar dados. A pesquisa de texto sem formatação funciona em todas as colunas, exceto nas colunas de tempo. Você também pode filtrar pesquisas para uma coluna específica com um filtro por coluna. Digite o nome da coluna sem espaços, dois-pontos (**:**) e o valor de pesquisa. Depois disso, use um ponto-e-vírgula (**;**) para adicionar outro valor de coluna e de pesquisa.

     Por exemplo, para localizar os eventos de desempenho que tenham a palavra "lento" na coluna **Descrição**, digite:

     `Description:slow`

##  <a name="StartDebugging"></a> Iniciar depuração a partir de um log do IntelliTrace

###  <a name="Performance"></a> Violações de desempenho
 Revise os eventos de desempenho que foram registrados para seu aplicativo. Você pode ocultar esses eventos que não ocorrem com frequência.

##### <a name="to-start-debugging-from-a-performance-event"></a>Para iniciar a depuração de um evento de desempenho

1.  Em **Violações de Desempenho**, revise os eventos de desempenho gravados, o tempo de execução total e outras informações dos eventos. Em seguida, verifique um pouco mais os métodos que foram chamados durante um evento de desempenho específico.

     ![Exibir detalhes de eventos de desempenho](../debugger/media/ffr_itsummarypageperformance.png "FFR_ITSummaryPagePerformance")

     Você também pode clicar duas vezes no evento.

2.  Na página de eventos, revise o tempo de execução dessas chamadas. Localize uma chamada lenta na árvore de execução.

     As chamadas mais lentas aparecem em sua própria seção quando você tem várias chamadas, aninhadas ou de outra maneira.

3.  Expanda essa chamada para revisar qualquer chamada e aninhada e os valores de parâmetro gravados nesse momento.

     (Teclado: Para mostrar ou ocultar uma chamada aninhada, pressione a **seta para a direita** ou **seta para a esquerda** , respectivamente. Para mostrar e ocultar valores de parâmetro para uma chamada aninhada, pressione a tecla **Espaço**.)

     Comece a depuração pela chamada.

     ![Iniciar a depuração de chamada de método](../debugger/media/ffr_itsummarypageperformancemethodscalled.png "FFR_ITSummaryPagePerformanceMethodsCalled")

     Você também pode simplesmente clicar duas vezes na chamada ou pressionar a tecla **Enter**.

     Se o método estiver no código do aplicativo, o Visual Studio irá para esse método.

     ![Vá para o código do aplicativo do evento de desempenho](../debugger/media/ffr_itsummarypageperformancegotocode.png "FFR_ITSummaryPagePerformanceGoToCode")

     Agora você pode revisar outros valores gravados, a pilha de chamadas, navegar por código, ou usar a janela do **IntelliTrace** para [avançar ou retornar "no tempo" entre outros métodos](../debugger/intellitrace.md) que foram chamados durante esse evento de desempenho.

###  <a name="ExceptionData"></a> Dados de exceção
 Revise as exceções acionadas e que foram registradas para seu aplicativo. Você pode agrupar as exceções que tenham o mesmo tipo e a mesma pilha de chamadas de forma que você veja apenas a exceção mais recente.

##### <a name="to-start-debugging-from-an-exception"></a>Para iniciar a depuração a partir de uma exceção

1.  Em **Dados da Exceção**, revise os eventos de exceção gravados, seus tipos, mensagens e quando as exceções aconteceram. Para se aprofundar no código, comece com a depuração do evento mais recente em um grupo de exceções.

     ![Iniciar a depuração de eventos de exceção](../debugger/media/ffr_itsummarypageexception.png "FFR_ITSummaryPageException")

     Você também pode clicar duas vezes no evento. Se os eventos não estiverem agrupados, escolha **Depurar Este Evento**.

     Se a exceção ocorreu no código do aplicativo, o Visual Studio irá para o local onde a exceção ocorreu.

     ![Vá para o código do aplicativo de um evento de exceção](../debugger/media/ffr_itsummarypageexceptiongotocode.png "FFR_ITSummaryPageExceptionGoToCode")

     Agora você pode revisar outros valores gravados, a pilha de chamadas, ou usar a janela do **IntelliTrace** para [avançar ou retornar "no tempo" entre outros eventos gravados](../debugger/intellitrace.md), o código relativo e os valores gravados nesses momentos.

    |**Coluna**|**Exibe**|
    |----------------|-------------------|
    |**Tipo**|Tipo .NET da exceção|
    |**Mensagem Mais Recente** para exceções agrupadas ou **Mensagem** para exceções não agrupadas|A mensagem fornecida pela exceção|
    |**Contagem** para exceções agrupadas|O número de vezes em que a exceção foi acionada|
    |**ID do Thread** para exceções não agrupadas|ID do thread que acionou a exceção|
    |**Horário do Evento Mais Recente** ou **Hora do Evento**|Carimbo de data/hora registrado quando a exceção foi acionada|
    |**Pilha de chamadas**|Pilha de chamadas para uma exceção.<br /><br /> Para ver a pilha de chamadas, escolha uma exceção na lista. A pilha de chamadas aparece abaixo da lista de exceções.|

###  <a name="Analysis"></a> Análise
 Diagnostique problemas com os aplicativos do SharePoint 2010 e do SharePoint 2013 usando uma ID de correlação do SharePoint ou examine qualquer exceção sem tratamento encontrada pelo Microsoft Monitoring Agent.

-   Use uma ID de correlação do SharePoint para localizar sua solicitação da Web e eventos correspondentes. Escolha um evento e inicie a depuração no ponto onde e quando o evento ocorreu.

-   Se o Microsoft Monitoring Agent encontrou exceções sem tratamento, escolha uma exceção e inicie a depuração no ponto onde e quando a exceção ocorreu.

##### <a name="start-debugging-with-a-sharepoint-correlation-id"></a>Iniciar depuração com uma ID de correlação do SharePoint

1. Copie a ID de correlação do SharePoint de sua origem.

    Por exemplo:

    ![IntelliTrace &#45; erro do SharePoint &#45; ID de correlação](../debugger/media/sharepointerror_intellitrace.png "SharePointError_IntelliTrace")

2. Abra o arquivo .iTrace, vá para **Análise** e digite a ID de correlação do SharePoint para revisar a solicitação da Web e os eventos registrados correspondentes.

    ![Log do IntelliTrace &#45; ID de correlação do SharePoint inserir](../debugger/media/entersharepointcorrelationid.png "EnterSharePointCorrelationID")

3. Sob **Eventos de Solicitação**, examine os eventos. A partir da parte superior, os eventos aparecem na ordem em que aconteceram.

   1. Escolha um evento para ver seus detalhes.

   2. Escolha **Iniciar Depuração** para iniciar depuração no ponto onde o evento aconteceu.

      ![Arquivo de log do IntelliTrace &#45; solicitação do modo de exibição da web &#43; eventos](../debugger/media/entersharepointcorrelationid2.png "EnterSharePointCorrelationID2")

   Você pode ver esses tipos de eventos do SharePoint com eventos do IntelliTrace:

-   **Eventos de perfil de usuário**

     Esses eventos ocorrem quando o SharePoint carrega um perfil de usuário e quando as propriedades de perfil de usuário são lidas ou alteradas.

-   **Eventos do ULS (Unified Logging System)**

     O Microsoft Monitoring Agent registra um subconjunto de eventos ULS do SharePoint ULS e destes campos:

    |**Campo do IntelliTrace**|**Campo do ULS do SharePoint**|
    |----------------------------|------------------------------|
    |**ID**|**EventID**|
    |**Nível**|**Nível**|
    |**ID da Categoria**|**ID da Categoria**|
    |**Categoria**|**Categoria**|
    |**Área**|**Produto**|
    |**Saída**|**Message**|
    |**ID de Correlação**|**ID de Correlação**|

##### <a name="start-debugging-from-an-unhandled-exception"></a>Iniciar depuração a partir de uma exceção sem tratamento

1. Escolha uma ID de correlação do SharePoint para uma exceção. As exceções são agrupadas por tipo e pilha de chamadas.

2. (Opcional) Expanda **Pilha de Chamadas** para ver a pilha de chamadas para um grupo de exceções.

3. Escolha **Exceção da Depuração** para iniciar a depuração no ponto onde e quando a exceção aconteceu.

    ![Log do IntelliTrace &#45; exceções sem tratamento do SharePoint](../debugger/media/sharepointunhandledexceptions_intellitrace.png "SharePointUnhandledExceptions_IntelliTrace")

   Para obter instruções, consulte [passo a passo: Depurando um aplicativo do SharePoint usando o IntelliTrace](../sharepoint/walkthrough-debugging-a-sharepoint-application-by-using-intellitrace.md). Para os tipos de dados que registra o agente, consulte [recursos do IntelliTrace](../debugger/intellitrace-features.md).

###  <a name="ThreadsList"></a> Lista de threads
 Examine os threads registrados executados no processo de destino. Você pode iniciar a depuração do primeiro evento válido do IntelliTrace em um thread selecionado.

##### <a name="to-start-debugging-from-a-specific-thread"></a>Para iniciar a depuração de um thread específico

1. Em **Lista de Threads**, escolha um thread.

2. Na parte inferior da **Lista de Threads**, escolha **Iniciar Depuração**. Você também pode clicar duas vezes em um thread.

    Para iniciar a depuração de onde o aplicativo começa, clique duas vezes em **Thread Principal**. Ver [recursos do IntelliTrace](../debugger/intellitrace-features.md).

   Os dados do thread que o usuário cria podem ser mais úteis do que os threads que um servidor cria e gerencia para aplicativos Web hospedados pelo IIS.

|**Coluna**|**Exibe**|
|----------------|-------------------|
|**ID**|Número de ID do thread|
|**Nome**|Nome do thread. Threads sem nome aparecem como "\<Sem nome>".|
|**Hora de início**|A hora em que o thread foi criado|
|**Hora de término**|A hora em que o thread foi concluído|

###  <a name="TestData"></a> Dados de teste
 Examine os dados do IntelliTrace que o Test Manager registrou ao testar seu aplicativo.

##### <a name="to-start-debugging-from-a-specific-test-step"></a>Para iniciar a depuração de uma etapa específica do teste

1.  Expanda **Grade de Etapas do Teste**. Escolha uma etapa do teste.

2.  Na parte inferior da **Grade de Etapas do Teste**, escolha **Iniciar Depuração**. Você também pode clicar duas vezes em uma etapa de teste.

     Isso inicia a depuração do primeiro evento válido do IntelliTrace após a etapa selecionada do teste.

     Quando houver dados de teste, o IntelliTrace tentará resolver a compilação do Team Foundation Server associada usada para executar o teste. Se a compilação for encontrada, os símbolos associados ao aplicativo serão resolvidos automaticamente.

|**Campo**|**Exibe**|
|---------------|-------------------|
|**Sessão de teste**|Sessões de teste que foram registradas. Normalmente, há apenas uma. Esta lista estará vazia se os dados de teste tiverem sido criados usando um teste exploratório manual.|
|**Caso de teste**|Casos de teste da sessão de teste selecionada. Esta lista estará vazia se os dados de teste tiverem sido criados usando um teste exploratório manual.|
|**Grade de etapas do teste**|Etapas de teste que foram registradas com o resultado de teste de aprovação ou de falha|

###  <a name="SystemInfo"></a> Informações do sistema
 Esta seção mostra detalhes sobre o sistema que hospedou o aplicativo, por exemplo, informações de hardware, do sistema operacional e específicas do ambiente e do processo.

###  <a name="Modules"></a> Módulos
 Esta seção mostra os módulos que o processo de destino carregou. Os módulos aparecem na ordem em que foram carregados.

|**Coluna**|**Exibe**|
|----------------|-------------------|
|**Nome do Módulo**|Nome do arquivo do módulo|
|**Caminho do Módulo**|Local do disco onde o módulo foi carregado|
|**ID do módulo**|O identificador exclusivo do módulo que é específico da versão e que contribui para os arquivos de símbolo (PDB) correspondentes. Ver [Localizando arquivos de símbolo (. PDB) e arquivos de origem](specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).|

### <a name="where-can-i-get-more-information"></a>Onde posso obter mais informações?
 [Usando o coletor IntelliTrace autônomo](../debugger/using-the-intellitrace-stand-alone-collector.md)

 [Recursos do IntelliTrace](../debugger/intellitrace-features.md)

 [Coletar mais dados de diagnóstico em testes manuais](/azure/devops/test/mtm/collect-more-diagnostic-data-in-manual-tests?view=vsts)

 [IntelliTrace](../debugger/intellitrace.md)

#### <a name="forums"></a>Fóruns
 [Depurador do Visual Studio](http://go.microsoft.com/fwlink/?LinkId=262263)

#### <a name="guidance"></a>Diretrizes
 [Testando para entrega contínua com Visual Studio 2012 – capítulo 6: Uma caixa de ferramentas de teste](http://go.microsoft.com/fwlink/?LinkID=255203)