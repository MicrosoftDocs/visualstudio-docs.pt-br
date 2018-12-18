---
title: Analisar resultados de teste de carga e erros no Visual Studio
ms.date: 10/19/2016
ms.topic: conceptual
f1_keywords:
- vs.test.load.monitor.pageresult
- vs.test.load.dialog.column
- vs.test.load.monitor.requestresult
- vs.test.load.monitor.testresult
- vs.test.load.monitor.table.view
- vs.test.load.monitor.agentresult
- vs.test.load.monitor.transactionresult
helpviewer_keywords:
- tables, Load Test Viewer options
- load test results, tables
- load tests, Load Test Viewer
- data [Visual Studio ALM], load test tables
- Load Test Viewer, tables
- load tests, results tables
ms.assetid: 0a84bda3-6051-45eb-9c7f-d57419e1f97d
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: cab92c4daac6da81541771b534f4f1a6f9be159e
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52896621"
---
# <a name="analyze-load-test-results-and-errors-in-the-tables-view-of-the-load-test-analyzer"></a>Analisar resultados do teste de carga e erros na exibição Tabelas do Analisador de Teste de Carga

Ao exibir os resultados de uma execução do teste de carga, você pode mostrar painéis diferentes que ofereçam maneiras diferentes de analisar os dados. É possível exibir os dados como um gráfico, para ver como eles mudam com o passar do tempo, ou exibir os dados como tabelas detalhadas.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

Para alternar para a exibição de tabela, escolha **Tabelas** na barra de ferramentas do **teste de carga**. Para alternar entre tabelas diferentes, use a lista suspensa **Tabela** na barra de ferramentas acima da grade de tabela. Na exibição de tabela, é possível exibir até quatro tabelas por vez. Para obter mais informações, consulte [Organizar lado a lado tabelas de teste de carga](../test/analyze-load-test-results-and-errors-in-the-tables-view.md#tile-load-test-tables) neste tópico.

A maioria dos valores numéricos exibidos em uma tabela para contadores de desempenho é cumulativa em relação à execução de todo o teste de carga. As colunas chamadas **Último** são uma exceção e representam o valor do intervalo de amostragem mais recente.

> [!NOTE]
> As colunas chamadas **Último** só permanecem disponíveis durante a execução de um teste de carga. Depois que um teste de carga é concluído, essas colunas não permanecem disponíveis.

É possível classificar a maioria das tabelas escolhendo-se o título da coluna que você deseja classificar. Por padrão, algumas tabelas não exibem todas as colunas disponíveis. Será possível adicionar colunas a tabelas, se houver colunas disponíveis. Para adicionar colunas, clique com o botão direito do mouse na tabela e escolha **Adicionar/Remover Colunas**.

> [!NOTE]
> É possível copiar os dados de uma tabela para outros aplicativos como o Excel para análise adicional.

## <a name="the-load-test-tables"></a>As tabelas do teste de carga

A tabela a seguir lista as tabelas que estão disponíveis para analisar execuções de teste de carga.

|Nome da tabela|Descrição|
|-|-|
|Erros|Exibe uma lista de erros ocorridos durante a execução do teste de carga. Para obter mais informações, confira [A tabela de erros](../test/analyze-load-test-results-and-errors-in-the-tables-view.md#the-errors-table) neste tópico e [Analisar resultados do teste de carga](../test/analyze-load-test-results-using-the-load-test-analyzer.md).|
|Pages (Páginas)|Exibe uma lista de páginas acessadas durante a execução do teste de carga. Alguns dados nessa tabela só estarão disponíveis depois que um teste de carga for concluído. Para obter mais informações, confira [Como exibir a resposta da página da Web](../test/how-to-view-web-page-response-time-in-a-load-test.md).|
|Solicitações|Exibe detalhes de solicitações individuais emitidas durante um teste de carga. Isso inclui todas as solicitações HTTP e as solicitações dependentes como imagens. Para obter mais informações, confira [A tabela Solicitações](../test/analyze-load-test-results-and-errors-in-the-tables-view.md#the-requests-table) neste tópico.|
|Rastreamento SQL|Exibe os resultados do rastreamento do SQL. Essa tabela só estará disponível depois que um teste de carga for concluído, e apenas se o rastreamento do SQL tiver sido usado durante o teste. Para obter mais informações, confira [A tabela de dados Rastreamento do SQL](../test/analyze-load-test-results-and-errors-in-the-tables-view.md#the-sql-trace-data-table) neste tópico.|
|Testes|Exibe detalhes de testes individuais durante um teste de carga. Para obter mais informações, confira [A tabela Testes](../test/analyze-load-test-results-and-errors-in-the-tables-view.md#the-tests-table) neste tópico.|
|Limites|Exibe uma lista de violações da regra de limite ocorridos durante a execução do teste de carga. Para obter mais informações, confira [Analisando violações de regra de limite](../test/analyze-threshold-rule-violations-in-load-tests.md).|
|Transações|Exibe uma lista de transações ocorridas durante uma execução do teste de carga. Para obter mais informações, confira [A tabela Transações](../test/analyze-load-test-results-and-errors-in-the-tables-view.md#the-transactions-table) neste tópico.|
|Agentes|Só será exibida se o teste de carga estiver usando um controlador de teste e agentes de teste. Exibe uma lista dos agentes que foram usados durante a execução do teste de carga. A tabela Agentes inclui quantas solicitações o agente testou e, dessas solicitações, quantas falharam. Além disso, a tabela Agentes inclui o número de testes na combinação de testes de carga que o agente testou e, desses, quantos falharam.|
|Detalhes do teste|Exibe detalhes dos testes incluídos na combinação de testes do teste de carga. Os detalhes incluem o nome do teste, o cenário em que o teste estava, a hora em que o teste começou, o tempo necessário para testar a execução e o resultado do teste que indica se o teste passou ou falhou. Se o teste tiver falhado, haverá um link na coluna **Detalhes**. É possível escolher o link que levará você até o Editor de Testes de Desempenho na Web com a solicitação com falha realçada.|

## <a name="collect-percentile-data"></a>Coletar dados de percentil

 Algumas tabelas de teste de carga podem conter colunas adicionais, que incluem dados de percentil e tempos de resposta divididos em grupos baseados na emulação de rede. Por padrão, esses dados não são coletados. Dados percentuais só estão disponíveis ao salvar resultados em um banco de dados, não ao salvar localmente. Para obter mais informações, confira [Gerenciando resultados do teste no Repositório de Resultados do Teste de Carga](../test/manage-load-test-results-in-the-load-test-results-repository.md). Além disso, para coletar esses dados, no **Editor de Teste de Carga**, sob o nó **Configurações de Execução**, selecione o nó da configuração de execução específico a ser alterado. Na janela **Propriedades**, para a propriedade **Armazenamento de Detalhes de Medição de Tempo**, selecione **StatisticsOnly** ou **AllIndividualDetails**. Para obter mais informações, confira [Como exibir a resposta da página da Web](../test/how-to-view-web-page-response-time-in-a-load-test.md).

## <a name="the-requests-table"></a>A tabela Solicitações

 A tabela **Solicitações** exibe detalhes de solicitações individuais emitidas durante um teste de carga. Isso inclui todas as solicitações HTTP e as solicitações dependentes como imagens. A tabela lista solicitações por teste e cenário, porque uma solicitação pode ser incluída em muitos testes e cenários.

 A seguinte tabela lista as colunas na tabela **Solicitações**:

|Column|Descrição|Visível por padrão|
|-|-|-|
|**Solicitação**|A URL da solicitação. Por exemplo, *home.html* ou *orange-arrow.gif*.|Sim|
|**Cenário**|O nome do cenário.|Sim|
|**Teste**|O nome do teste.|Sim|
|**Total**|O número total dessa solicitação de teste de desempenho na Web emitida durante a execução do teste de carga. O total inclui solicitações aprovadas e com falha, mas não inclui solicitações armazenadas em cache, porque não são emitidas para o servidor Web.|Sim|
|**Aprovado**|O número de vezes em que a solicitação foi emitida e aprovada.|Não|
|**Falha**|O número de vezes em que a solicitação foi emitida e falhou. As entradas nessa coluna são exibidas como hiperlinks. É possível escolher qualquer hiperlink para exibir uma lista dos erros individuais na caixa de diálogo **Erros de Teste de Carga**. Para obter mais informações, confira [Analisar resultados do teste de carga](../test/analyze-load-test-results-using-the-load-test-analyzer.md).|Sim|
|**Em Cache**|O número total de vezes em que a solicitação já foi armazenada em cache.|Não|
|**Solicitações/s**|A taxa por segundo da solicitação durante a execução do teste de carga.|Não|
|**Aprovado/s**|A taxa por segundo dessa solicitação durante a execução do teste de carga, para as instâncias dessa solicitação que passaram.|Não|
|**Com falha/s**|A taxa por segundo dessa solicitação durante a execução do teste de carga, para as instâncias dessa solicitação que falharam.|Não|
|**Primeiro Tempo de Byte**|O tempo médio para receber o primeiro byte da resposta, medido desde a hora em que a solicitação foi enviada para o servidor Web. As unidades estão em segundos.|Não|
|**Tempo de resposta**|O tempo médio para receber toda a resposta para uma solicitação, medido desde a hora em que a solicitação foi enviada para o servidor Web. As unidades estão em segundos.|Sim|
|**Comprimento do conteúdo**|O tamanho médio do conteúdo da resposta para a solicitação. As unidades estão em bytes.|Sim|

## <a name="the-tests-table"></a>A tabela Testes

 A tabela **Testes** exibe detalhes de testes individuais executados durante um teste de carga. A tabela lista testes por teste e cenário, porque um teste pode ser incluído em muitos cenários.

 A seguinte tabela lista as colunas na tabela **Testes**.

|Column|Descrição|Visível por padrão|
|-|-|-|
|**Teste**|O nome do teste.|Sim|
|**Cenário**|O nome do cenário.|Sim|
|**Total**|O número total de vezes em que o teste foi executado no cenário. Isso inclui o número de vezes em que o teste passou e falhou.|Sim|
|**Aprovado**|O número de vezes em que o teste foi executado no cenário e passou.|Sim|
|**Falha**|O número de vezes em que o teste foi executado no cenário e falhou. As entradas nessa coluna são exibidas como hiperlinks. É possível escolher qualquer hiperlink para exibir uma lista dos erros individuais na caixa de diálogo **Erros de Teste de Carga**. Para obter mais informações, confira [Analisar resultados do teste de carga](../test/analyze-load-test-results-using-the-load-test-analyzer.md).|Sim|
|**Testes/s**|A taxa por segundo do teste durante a execução do teste de carga.|Sim|
|**Aprovado/s**|A taxa por segundo desse teste durante a execução do teste de carga, para as instâncias desse teste que passaram.|Não|
|**Com falha/s**|A taxa por segundo desse teste durante a execução do teste de carga, para as instâncias desse teste que falharam.|Não|
|**Tempo de teste**|O tempo médio de execução do teste durante a execução do teste de carga. As unidades estão em segundos.|Sim|
|**Tempo de teste 90%**|O 90º valor de percentil para Tempo de Teste.|Não|
|**Tempo de teste 95%**|O 95º valor de percentil para Tempo de Teste.|Sim|
|**Solicitações/teste**|O número médio de solicitações no teste se ele for um teste de desempenho na Web.|Não|

## <a name="the-transactions-table"></a>A tabela Transações

 A tabela **Transações** exibe uma lista de transações ocorridas durante uma execução de teste de carga. As transações se referem às transações definidas em um teste de desempenho na Web ou a temporizadores definidos em um teste da unidade. A transação não se refere a transações de banco de dados.

 A seguinte tabela lista as colunas na tabela **Transações**.

> [!NOTE]
> Para exibir todas as colunas, você deve habilitar a propriedade Armazenamento de Detalhes de Medição de Tempo associada à configuração de execução ativa. Para saber mais, confira [Como especificar a propriedade de armazenamento de detalhes de tempo](../test/how-to-specify-the-timing-details-storage-property-for-a-load-test.md).

|Column|Descrição|Visível sem detalhes de tempo|
|-|-|-|
|**Transação**|O nome da transação.|Sim|
|**Cenário**|O nome do cenário.|Sim|
|**Teste**|O nome do teste.|Sim|
|**Total**|O número total de transações emitidas durante a execução do teste de carga.|Sim|
|**Tempo de transação**|O tempo de execução da transação durante uma execução do teste de carga. Para testes de desempenho na Web, o tempo de raciocínio é incluído no cálculo. As unidades estão em segundos.|Não|
|**Tempo de resposta**|O tempo de resposta da transação do teste de desempenho na Web em uma execução do teste de carga. Tempo de Resposta é diferente do Tempo da Transação porque Tempo de Resposta não inclui tempo de raciocínio ocorrido durante a transação. As unidades estão em segundos.|Não|
|**Tempo méd. de transação**|O tempo médio da transação. Esse tempo inclui tempos de raciocínio. Por exemplo, se você tiver três solicitações e cada uma tiver um tempo de raciocínio, esse tempo incluirá esses tempos de raciocínio e a hora real para executar solicitações.|Não|
|**Tempo méd. de resposta**|O tempo médio de resposta de uma transação do teste de desempenho na Web em uma execução do teste de carga. Tempo de Resposta é diferente do Tempo da Transação porque Tempo de Resposta não inclui tempo de raciocínio ocorrido durante a transação. As unidades estão em segundos.|Não|
|**Tempo de resposta mínimo**|Isso não inclui tempos de raciocínio.|Não|
|**Tempo máximo de resposta**|Isso não inclui tempos de raciocínio.|Não|
|**Mediana do tempo de resposta**|Isso não inclui tempos de raciocínio.|Não|
|**Tempo de resposta 90%**|O 90º valor de percentil para Tempo de Transação. Isso não inclui tempos de raciocínio. **Observação:** isso é diferente do Visual Studio Team System 2008 Test Load Agent, que usou o valor **Tempo de transação de 90%**.|Não|
|**Tempo de resposta 95%**|O 95º valor de percentil para Tempo de Transação. Isso não inclui tempos de raciocínio. **Observação:** isso é diferente do Visual Studio Team System 2008 Test Load Agent, que usou o valor **Tempo de transação de 95%**.|Não|
|**Tempo de resposta 99%**|O 99º valor de percentil para Tempo de Transação. Isso não inclui tempos de raciocínio.|Não|
|**Desvio padrão do tempo de resposta**|Isso não inclui tempos de raciocínio.|Não|

## <a name="the-errors-table"></a>A tabela Erros

 Ao executar um teste de carga, você pode analisar erros ocorridos. A análise de erros e o ajuste dos testes são partes importantes do processo de teste da carga. Se tiver ocorrido qualquer erro, um hiperlink **erros** será exibido na barra de status do teste de carga e especificará o número de erros ocorridos. Para exibir a tabela de erros, escolha o hiperlink.

 A tabela de erros agrupa os erros ocorridos durante um teste de carga pelo tipo e pelo subtipo do erro. Também há uma linha **total** na tabela que especifica a contagem total de todos os erros ocorridos.

 A tabela de erros contém as seguintes colunas:

|Column|Descrição|Visível por padrão|
|-|-|-|
|Tipo|O tipo do erro. Por exemplo, HttpError.|Sim|
|SubType|O subtipo do erro. Por exemplo, LoadTestException.|Sim|
|Count|O número de erros desse tipo ocorridos durante o teste de carga. As entradas nessa coluna são exibidas como hiperlinks. É possível escolher qualquer hiperlink para exibir uma lista dos erros individuais.|Sim|
|Última mensagem|Uma mensagem que descreve o erro. Por exemplo, 404 - NotFound.|Sim|

 Para saber mais, confira [Trabalhando com tabelas de teste de carga](../test/analyze-load-test-results-and-errors-in-the-tables-view.md).

### <a name="drill-down-to-the-error-list"></a>Fazer drill down até a lista de erros

A tabela de erros agrupa os erros pelo tipo e pelo subtipo do erro. Para exibir uma tabela dos erros individuais, você exibe a caixa de diálogo **Erros de teste de carga**. Para exibir a caixa de diálogo, escolha um hiperlink na coluna **Contagem** da tabela de erros. Também é possível exibir a caixa de diálogo clicando com o botão direito do mouse em uma linha na tabela de erros populada e escolhendo-se **Erros**.

> [!NOTE]
> Apenas as primeiras 1.000 instâncias de qualquer combinação de tipo e subtipo de erro são coletadas. Ao exibir a caixa de diálogo **Erros de Teste de Carga**, você verá no máximo as primeiras 1.000 instâncias com erro.

A tabela **Erros de Teste de Carga** contém as seguintes colunas:

|Column|Descrição|
|-|-|
|**Time**|O tempo durante o teste de carga em que o erro ocorreu.|
|**Agente**|O nome do computador do agente em que o erro ocorreu. Isso é importante quando você executa testes de carga usando controladores de teste e agentes de teste. Para obter mais informações, consulte [Instalar e configurar agentes de teste](../test/lab-management/install-configure-test-agents.md).|
|**Teste**|O nome do teste de desempenho na Web no qual o erro ocorreu.|
|**Cenário**|O nome do cenário no qual o erro ocorreu.|
|**Solicitação**|A URL da solicitação na qual o erro ocorreu.|
|**Tipo**|O tipo do erro. Por exemplo, HttpError.|
|**SubType**|O subtipo do erro. Por exemplo, LoadTestException.|
|**Texto**|O texto da mensagem de erro. Por exemplo, 404 - NotFound.|
|**Pilha**|As entradas nessa coluna estão vazias ou a palavra **Pilha** está formatada como um hiperlink. É possível escolher o hiperlink para exibir um rastreamento de pilha do erro.|
|**Detalhes**|As entradas nessa coluna estão vazias ou a palavra **TestLog** está formatada como um hiperlink. Esse link pode ajudar a isolar erros no teste de carga. Por exemplo, a escolha do link **TestLog** em um erro na solicitação de teste de desempenho Web abrirá os resultados do teste de desempenho Web no Visualizador de Resultados de Teste de Desempenho Web e realçará o erro da solicitação.|

> [!NOTE]
> É possível classificar a tabela escolhendo-se os cabeçalhos de coluna.

## <a name="the-sql-trace-data-table"></a>A tabela de dados de Rastreamento do SQL

É possível coletar dados de rastreamento do SQL durante uma execução do teste de carga para analisar posteriormente. A coleta dos dados de rastreamento permite identificar as consultas e os procedimentos armazenados mais lentos no banco de dados do SQL Server que está sendo testado.

Se o rastreamento do SQL estiver habilitado, um arquivo será criado durante a execução do teste de carga que contém os dados de rastreamento. Esses dados são salvos automaticamente em Carregar Repositório de Resultados de Teste ao final da execução do teste, e o arquivo de rastreamento é excluído. Analise os dados de rastreamento na tabela **Rastreamento SQL** depois que o teste de carga for concluído.

### <a name="to-view-sql-trace-data"></a>Para exibir dados de Rastreamento do SQL

1. No Analisador de Testes de Carga, escolha **Tabelas** na barra de ferramentas para garantir que a grade da tabela seja exibida.

2. Na caixa de listagem suspensa **Tabela**, selecione **Rastreamento SQL**.

3. Os dados de rastreamento que foram coletados durante a execução são exibidos na grade. A tabela lista as operações SQL mais lentas classificadas por duração, com a mais lenta na parte superior. Normalmente, a coluna **Duração** é a primeira coluna a ser examinada. Os dados são exibidos em milissegundos.

   As colunas são exibidas da seguinte forma:

    - **Classe de evento**

    - **Duração**

    - **CPU**

    - **Leituras**

    - **Gravações**

    - **TextData**

    - **StartTime**

    - **EndTime**

   Se quiser rastrear eventos SQL diferentes dos dados identificados nessas colunas, você poderá configurar seu próprio rastreamento SQL personalizado usando o SQL Profiler, uma ferramenta separada do Visual Studio.

## <a name="tile-load-test-tables"></a>Tabelas de teste de carga de bloco

Ao exibir os resultados de uma execução do teste de carga, você pode exibir os dados como tabelas detalhadas. Para alternar para a exibição de tabela, escolha **Tabelas** na barra de ferramentas do **teste de carga**. As tabelas que estão disponíveis são **Erros**, **Páginas**, **Solicitações**, **Rastreamento do SQL**, **Testes**, **Limites** e **Transações**. Para saber mais, confira [Trabalhando com tabelas de teste de carga](../test/analyze-load-test-results-and-errors-in-the-tables-view.md).

Na exibição de tabela, é possível exibir até quatro tabelas por vez sem sobreposição das tabelas.

### <a name="to-tile-tables"></a>Para organizar lado a lado as tabelas

1. Na barra de ferramentas **Analisador de Teste de Carga**, escolha **Tabelas**.

     A exibição da tabela é aberta. O layout padrão tem dois painéis horizontais.

2. Na barra de ferramentas **Analisador de Teste de Carga**, escolha o botão de **layout** e uma das seguintes opções:

    - **Um painel**

    - **Dois painéis horizontais**

    - **Três painéis horizontais**

    - **Quatro painéis horizontais**

3. Para alternar as tabelas diferentes, use a lista suspensa acima da grade de tabela em cada painel.

    > [!NOTE]
    > Não é possível exibir a mesma tabela em mais de um painel. Se você alterar a tabela exibida em um painel para uma tabela já exibida em outro, as tabelas alternarão os painéis.

## <a name="see-also"></a>Consulte também

- [Analisar resultados do teste de carga](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
- [Como acessar os resultados do teste de carga para análise](../test/how-to-access-load-test-results-for-analysis.md)
- [Analisar resultados do teste de carga na exibição Grafos](../test/analyze-load-test-results-in-the-graphs-view.md)
- [Analisar violações de regra de limite](../test/analyze-threshold-rule-violations-in-load-tests.md)
- [Gerenciar resultados do teste de carga no repositório de Resultados do Teste de Carga](../test/manage-load-test-results-in-the-load-test-results-repository.md)
- [Visão geral resumida dos resultados do teste de carga](../test/load-test-results-summary-overview.md)