---
title: Visão geral do resumo de resultados do teste de carga no Visual Studio
ms.date: 10/19/2016
ms.topic: conceptual
f1_keywords:
- vs.test.load.monitor.summary.view
helpviewer_keywords:
- load test results, summary
- load tests, summary in analyzer
- load tests, results summary
- Load Test Viewer, summary
- load tests, summary in Load Test Viewer
ms.assetid: 326b6c3c-5378-452b-8ca3-ba5a06ab3d41
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: ae70422ce3c88a3de6842f3f0946666b86ae559e
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895009"
---
# <a name="load-test-results-summary-overview"></a>Visão geral do resumo dos resultados do teste de carga

Depois de executar um teste de carga, você poderá exibir o resumo do teste de carga para entender os resultados rapidamente. O resumo do teste de carga fornece os resultados-chave em um formato compacto e fácil de ler. Você também pode imprimir o resumo do teste de carga. Isso deixa prático usá-lo quando você comunica resultados aos participantes. O resumo do teste de carga também é a exibição padrão quando você abre um resultado do teste de carga de um teste de carga executado anteriormente. Para saber mais, confira [Como acessar resultados do teste de carga para análise](../test/how-to-access-load-test-results-for-analysis.md).

![Exibição resumida](../test/media/ltest_summaryview.png)

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="the-load-test-summary"></a>O resumo do teste de carga

O resumo do teste de carga é dividido em seções. As seções iniciais aparecem na parte superior do resumo e estão sempre visíveis. Quando você exibe o resumo do teste de carga, os seguintes itens são os primeiros:

- Informações da execução de teste

- Resultados gerais

- Estatística-chave: 5 páginas mais lentas

- Estatística-chave: 5 testes mais lentos

- Estatística-chave: 5 operações SQL mais lentas

    > [!NOTE]
    > A seção Operações SQL só será exibida se o rastreamento SQL estiver habilitado no teste de carga.

As seções de fechamento aparecem ao final do resumo e podem ser recolhidas para economizar espaço. Os seguintes itens aparecem ao final do resumo do teste de carga:

- Resultados do teste

- Resultados da página

- Resultados da transação

- Recursos do sistema em teste

- Recursos de controlador e agente

- Erros

## <a name="test-run-information"></a>Informações sobre a execução de teste

A seção de informações sobre a execução do teste contém informações gerais sobre a execução, inclusive o nome do teste, as horas de início e de término e o controlador que executou o teste. Esta seção também contém a descrição opcional da execução que você adiciona ao executar o teste de carga.

## <a name="overall-results"></a>Resultados gerais

A seção de resultados geral contém resultados resumidos do teste, inclusive o número de solicitações por segundo, o número total de solicitações com falha, o tempo médio de resposta e o tempo médio da página.

## <a name="key-statistic-top-5-slowest-pages"></a>Estatística-chave: as 5 páginas mais lentas

A seção de páginas mais lentas contém as 5 páginas mais lentas no teste de carga. A URL e o tempo médio de carregamento de página são exibidos para cada página. As páginas são listadas em ordem decrescente. Você pode escolher a URL de uma página para abrir a tabela **Páginas** e inspecionar mais detalhes dessa página. Para obter mais informações, confira [Como exibir a resposta da página da Web](../test/how-to-view-web-page-response-time-in-a-load-test.md).

O valor de percentil de **Tempo de página 95% (seg.)** informa que 95% das páginas foram concluídas em menos do que esse tempo em segundos.

## <a name="key-statistic-top-5-slowest-tests"></a>Estatística-chave: os 5 testes mais lentos

A seção de testes mais lentos contém os 5 testes mais lentos no teste de carga. O nome do teste e o tempo médio do teste são exibidos para cada teste. Os testes são listados em ordem decrescente. Você pode escolher o nome de um teste para abrir a tabela **Testes** e inspecionar mais detalhes desse teste. Para obter mais informações, consulte [Analisar resultados de teste de carga e erros na exibição Tabelas](../test/analyze-load-test-results-and-errors-in-the-tables-view.md).

O valor de percentil de **Tempo de teste 95% (seg.)** informa que 95% dos testes foram concluídos em menos do que esse tempo em segundos.

## <a name="key-statistic-top-5-slowest-sql-operations"></a>Estatística-chave: as 5 operações SQL mais lentas

Se o rastreamento SQL for habilitado no teste de carga, a seção de consultas mais lenta conterá as 5 consultas mais lentas no teste de carga. O nome da operação e a duração do teste são exibidos para cada teste. A duração é exibida em microssegundos (SQL Server 2005) ou em milissegundos (SQL Server 2000 e anterior). Os testes são listados em ordem decrescente por duração. Você pode escolher o nome de uma operação para abrir a tabela **Rastreamento do SQL** e inspecionar mais detalhes dessa operação. Para obter mais informações, confira [A tabela de dados do Rastreamento do SQL](../test/analyze-load-test-results-and-errors-in-the-tables-view.md#the-sql-trace-data-table).

## <a name="test-results"></a>Resultados do teste

A seção de resultados do teste contém uma lista de todos os testes e cenários no teste de carga. O nome do teste, o cenário, o número de vezes em que ele foi executado, o número de vezes em que ele falhou e o tempo médio do teste são exibidos. Você pode escolher o nome de um teste para abrir a tabela **Testes** e inspecionar mais detalhes desse teste. Para obter mais informações, consulte [Analisar resultados de teste de carga e erros na exibição Tabelas](../test/analyze-load-test-results-and-errors-in-the-tables-view.md).

> [!NOTE]
> Você pode recolher e expandir essa seção escolhendo a seta à esquerda do título da seção.

## <a name="page-results"></a>Resultados da página

A seção de resultados da página contém uma lista de todas as páginas da Web no teste de carga. A URL, o cenário, o nome do teste, o tempo médio da página e a contagem são exibidos. Você pode escolher a URL de uma página para abrir a tabela **Páginas** e inspecionar mais detalhes dessa página. Para obter mais informações, confira [Como exibir a resposta da página da Web](../test/how-to-view-web-page-response-time-in-a-load-test.md).

> [!NOTE]
> Você pode recolher e expandir essa seção escolhendo a seta à esquerda do título da seção.

## <a name="transaction-results"></a>Resultados da transação

A seção de resultados da transação contém uma lista de todas as transações no teste de carga. O nome da transação, o cenário, o teste, o tempo de resposta, o tempo decorrido e a contagem são exibidos. Você pode escolher o nome de uma transação para abrir a tabela **Transações** e inspecionar mais detalhes dessa transação. Para obter mais informações, consulte [Analisar resultados de teste de carga e erros na exibição Tabelas](../test/analyze-load-test-results-and-errors-in-the-tables-view.md).

> [!NOTE]
> Você pode recolher e expandir essa seção escolhendo a seta à esquerda do título da seção.

Os valores de percentil reportam as seguintes informações de transação:

-   90% das transações totais foram concluídas em menos de \<tempo> segundos.

-   95% das transações totais foram concluídas em menos de \<tempo> segundos.

## <a name="system-under-test-resources"></a>Recursos do sistema em teste

A seção Recursos do sistema em teste contém uma lista de computadores que formam o conjunto de computadores de destino para o qual a carga está sendo gerada. Isso inclui qualquer computador do qual você coleta conjuntos de contadores diferentes de Agente ou Controlador. O nome do computador, % de tempo de processador e a memória disponível são exibidos. Você pode escolher um nome do computador para abrir o gráfico **Sistema em teste** e consultar o uso de recursos com o passar do tempo. Para obter mais informações, confira [Analisar os resultados do teste de carga na exibição Grafo](../test/analyze-load-test-results-in-the-graphs-view.md).

> [!NOTE]
> Você pode recolher e expandir essa seção escolhendo a seta à esquerda do título da seção.

## <a name="controller-and-agent-resources"></a>Recursos do controlador e do agente

A seção Controlador e recursos do agente contém uma lista dos computadores usados para executar o teste. O nome do computador, % de tempo de processador e a memória disponível são exibidos. Você pode escolher um nome do computador para abrir o gráfico **Controlador e agentes** e consultar o uso de recursos ao longo do tempo. Para obter mais informações, confira [Analisar os resultados do teste de carga na exibição Grafo](../test/analyze-load-test-results-in-the-graphs-view.md).

> [!NOTE]
> Você pode recolher e expandir essa seção escolhendo a seta à esquerda do título da seção.

## <a name="errors"></a>Erros

A seção erros contém uma lista de todos os erros ocorridos durante o teste de carga. O tipo e o subtipo do erro, a contagem e a última mensagem são exibidos. Você pode escolher um erro para abrir a tabela **Erros** e inspecionar mais detalhes desse erro. Para obter mais informações, consulte [Analisar resultados de teste de carga e erros na exibição Tabelas](../test/analyze-load-test-results-and-errors-in-the-tables-view.md).

> [!NOTE]
> Você pode recolher e expandir essa seção escolhendo a seta à esquerda do título da seção.

## <a name="print-a-summary"></a>Imprimir um resumo

É possível imprimir o resumo do teste de carga escolhendo **Imprimir** no menu de atalho no resumo. É possível visualizar a impressão escolhendo primeiro **Visualizar impressão** no menu de atalho no resumo. Você também pode imprimir diretamente na tela de visualização.

## <a name="see-also"></a>Consulte também

- [Analisar violações de regra de limite](../test/analyze-threshold-rule-violations-in-load-tests.md)
- [Analisar resultados do teste de carga](../test/analyze-load-test-results-using-the-load-test-analyzer.md)