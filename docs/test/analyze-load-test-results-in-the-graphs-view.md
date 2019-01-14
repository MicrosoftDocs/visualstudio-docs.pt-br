---
title: Analisando resultados de teste de carga na exibição de gráficos do Analisador de Teste de Carga
ms.date: 10/19/2016
ms.topic: conceptual
f1_keywords:
- vs.test.load.monitor.graph.view
helpviewer_keywords:
- graphs, analyzing load tests
- load tests, graphs in Load Test Viewer
- Load Test Viewer, graphs
- load tests, results graphs
- load tests, using graphs
- load test results, graphs
ms.assetid: 4a919cd8-541c-40ee-be3b-352fabc56140
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.openlocfilehash: f27689d5e3c322a539a0db5ee1f93c569cb181a5
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53914550"
---
# <a name="analyze-load-test-results-in-the-graphs-view-of-the-load-test-analyzer"></a>Analisar resultados do teste de carga na exibição Grafos do Analisador de Teste de Carga

Os resultados de um teste de carga são exibidos como dados em vários painéis diferentes.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

Para exibir os resultados do teste como grafos, escolha **Grafos** na barra de ferramentas **teste de carga**. Cada gráfico individual é exibido em um painel, com o nome do gráfico exibido na parte superior em uma lista suspensa. Para exibir um gráfico diferente no painel, escolha um nome de gráfico diferente na lista.

Até quatro painéis de gráfico podem ser exibidos por vez. Você pode alternar entre diferentes layouts de painel usando o botão de barra de ferramentas **layout do painel**.

Vários gráficos internos são fornecidos. Você pode usar os gráficos internos como estão ou pode personalizá-los. Além disso, também é possível criar seus próprios gráficos. Para obter mais informações, confira [Como: Adicionar e excluir contadores em grafos](../test/how-to-add-and-delete-counters-on-graphs-in-load-test-results.md) e [Como: Criar grafos personalizados](../test/how-to-create-custom-graphs-in-load-test-results.md).

## <a name="built-in-graphs"></a>Grafos internos

A tabela a seguir lista os gráficos internos que estão disponíveis para analisar resultados de testes de carga.

|Nome do gráfico|Descrição|
|-|-|
|Indicadores-Chave|Contadores que descrevem aspectos básicos do desempenho de teste, como carga do usuário, taxa de transferência e tempo de resposta.|
|Tempo de Resposta de Teste|Dados sobre quanto tempo leva a execução de testes.|
|Tempo de Resposta de Página|O tempo médio de resposta para páginas da Web que são acessadas durante o teste de carga.|
|Sistema em Teste|Informações sobre os computadores nos quais o aplicativo que está sendo testado é executado. Isso inclui dados sobre uso da memória, do processador, do disco físico, dos processos.<br /><br /> Por padrão, os contadores Apenas os Mbytes Disponíveis e Tempo de Processador são coletados.|
|Controlador e Agentes|Informações sobre os computadores nos quais os testes de carga são executados. Isso inclui dados sobre uso da memória, do processador, do disco físico, dos processos.<br /><br /> Por padrão, os contadores Apenas os Mbytes Disponíveis e Tempo de Processador são coletados.|
|Tempo de Resposta de Transação|O tempo médio de resposta para transações que ocorrem durante o teste de carga.|

 Você pode exibir diferentes contadores no gráfico, no tempo de execução e depois que um teste for executado.

> [!NOTE]
> Apenas os contadores de desempenho de tempo de resposta podem ser adicionados a um gráfico de tempo de resposta gerado automaticamente.

 As informações do contador são exibidas no gráfico e na legenda abaixo dos gráficos. Também é possível ampliar uma seção do gráfico. Para obter mais informações, confira [Como: Ampliar uma região do grafo](../test/how-to-zoom-in-on-a-region-of-the-graph-in-load-test-results.md).

## <a name="counters-displayed-in-graphs"></a>Contadores exibidos em grafos

 Os gráficos exibem *contadores*. Os contadores referem-se aos dados coletados durante um teste de carga, como testes por segundo ou tempo médio de teste. Para obter mais informações sobre contadores, confira [Especificando os conjuntos de contadores e as regras de limite para computadores em um teste de carga](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md).

 A legenda dos contadores que são exibidos nos gráficos mostra várias colunas de dados úteis sobre a execução do teste de carga. Para desativar a exibição de qualquer dado no gráfico, desmarque a caixa de seleção na linha da legenda.

 A legenda contém as seguintes colunas:

|Contador|O nome do contador|
|-|-|
|Instância|O nome da instância do contador.|
|Categoria|O nome da categoria do contador.|
|Computador|O nome do computador para o qual o contador é coletado.|
|Cor|A cor da linha no gráfico.|
|Intervalo|Indica o número que é representado por 100 no gráfico desse contador. Por exemplo, para um intervalo cujo valor superior é 10.000, o rótulo 100 na parte superior do gráfico representa 10.000.|
|Mín.|Indica o valor mínimo do contador em milissegundos.|
|Máx.|Indica o valor máximo do contador em milissegundos.|
|Média|Indica o valor médio do contador em milissegundos.|
|Último|Mostra o valor do contador durante o intervalo de amostragem mais recente em milissegundos.|

## <a name="tasks"></a>Tarefas

|Tarefas|Tópicos associados|
|-|-|
|**Personalizar os grafos usando a legenda:** A legenda da exibição de Grafos exibe informações de cada contador de desempenho associado a um grafo. Você pode usar a legenda para remover os contadores de desempenho, realçar contadores de desempenho no gráfico e personalizar as opções de plotagem.|-   [Usando a legenda da exibição Grafos para analisar testes de carga](../test/use-the-graphs-view-legend-to-analyze-load-tests.md)|
|**Exibir contadores em grafos:** Você pode adicionar diferentes tipos de dados a um grafo de resultados do teste de carga colocando contadores no grafo.|-   [Como: Adicionar e excluir contadores em grafos](../test/how-to-add-and-delete-counters-on-graphs-in-load-test-results.md)|
|**Ampliar grafos:** Após a conclusão de um teste de carga, você poderá usar as barras de zoom para ampliar e rolar para uma região do gráfico. Ao ampliar, você pode examinar detalhadamente os dados que foram gerados durante uma execução de teste de carga.|-   [Como: Ampliar uma região do grafo](../test/how-to-zoom-in-on-a-region-of-the-graph-in-load-test-results.md)|
|**Organizar grafos lado a lado:** Você pode organizar grafos de resultados de testes de carga em qualquer um dos diversos padrões. Você pode organizar até quatro grafos lado a lado.||
|**Criar grafos personalizados:** Você pode projetar gráficos que exibam informações específicas sobre resultados de teste de carga. Você cria um gráfico personalizado especificando os contadores de teste de carga que o gráfico exibirá.|-   [Como: Criar grafos personalizados](../test/how-to-create-custom-graphs-in-load-test-results.md)|
|**Exportar os dados de contadores de desempenho no grafo:** Você pode exportar os dados do grafo para o Microsoft Excel usando o botão **Exportar Dados do Grafo para o Excel** na barra de ferramentas do **Analisador de Teste de Carga** enquanto estiver na exibição **Grafos**.||

## <a name="related-tasks"></a>Tarefas relacionadas

 [Analisar resultados do teste de carga e erros na exibição Tabelas](../test/analyze-load-test-results-and-errors-in-the-tables-view.md)

 [Como: Acessar os resultados do teste de carga para análise](../test/how-to-access-load-test-results-for-analysis.md)

 [Analisar resultados do teste de carga](../test/analyze-load-test-results-using-the-load-test-analyzer.md)

## <a name="see-also"></a>Consulte também

- [Como: Adicionar e excluir contadores em grafos](../test/how-to-add-and-delete-counters-on-graphs-in-load-test-results.md)
- [Como: Criar grafos personalizados](../test/how-to-create-custom-graphs-in-load-test-results.md)
- [Como: Ampliar uma região do grafo](../test/how-to-zoom-in-on-a-region-of-the-graph-in-load-test-results.md)