---
title: Analisar resultados de teste de carga no Visual Studio
ms.date: 10/20/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, test results
- load tests, analyzing test results
- load tests, managing test results
ms.assetid: 8a4ba300-425d-447c-91d9-c53f4345feee
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 92685b4ed7f3ea9bfbaaad70d3bb61786bcc82a0
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52896660"
---
# <a name="analyze-load-test-results-using-the-load-test-analyzer"></a>Analisar resultados do teste de carga usando o Analisador de Teste de Carga

Localize gargalos, identifique erros e meça as melhorias em seu aplicativo ao usar o **Analisador de Teste de Carga**.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

Analise resultados de teste de carga das seguintes maneiras:

-   Monitore um teste de carga quando ele estiver em execução.

-   Analise um teste de carga depois de concluído.

-   Exiba resultados de um teste de carga anterior.

Você também pode criar relatórios que comparam dois ou mais relatórios para análise de tendência para compartilhar com os participantes. Confira [Relatando resultados do teste de carga para comparações de testes ou análise de tendências](../test/compare-load-test-results.md).

Essas tarefas podem ser concluídas se você executar o teste de carga no Visual Studio Enterprise ou da linha de comando, quer você execute o teste de carga em um único computador ou em um computador remoto.

## <a name="differences-between-analyzing-a-running-and-a-completed-load-test"></a>Diferenças entre a análise de um teste de carga em execução e um teste de carga concluído

 Quando você executa um teste de carga, o **Analisador de Teste de Carga** aparece em uma guia separada, com o nome do teste de carga e a hora em que o teste foi iniciado (por exemplo, **LoadTest1 [12:40 PM]**). Quando um teste de carga é executado, um conjunto menor de dados do contador de desempenho é mantido na memória. Você pode monitorar esse conjunto de dados quando seu teste de carga é executado. Depois que um teste de carga é concluído, você pode analisar o conjunto de dados completo do banco de dados. Há diferenças em relação a quais dados são exibidos quando um teste de carga é executado e quais dados você pode ver depois que um teste de carga é concluído. Por exemplo, 90% e 95% dos dados de tempo de resposta não são calculados até que o teste de carga seja concluído. Algumas diferenças também ocorrem na funcionalidade das ferramentas que estão disponíveis para analisar os dados.

 Quando você executa o teste de carga, duas exibições ficam disponíveis: a exibição **Grafos** e a exibição **Tabelas**. A exibição **Grafos** permite representar graficamente os contadores de desempenho coletados. A exibição **Tabelas** fornece informações sobre os testes, as páginas, as transações e as solicitações coletadas. Você também obtém uma tabela que lista os erros.

 Por padrão, quando a execução de teste de carga é concluída, a exibição **Resumo** é exibida. Você pode alternar entre as exibições **Resumo**, **Grafos**, **Tabelas** e **Detalhes** usando a barra de ferramentas. O **Analisador de Teste de Carga** pode ser encaixado ou configurado para flutuar usando as técnicas normais de manipulação de janela do Visual Studio. Quando você analisa as execuções de testes de carga concluídas, é possível que haja vários **Analisadores de Teste de Carga** abertos ao mesmo tempo para comparar as diferentes execuções de testes de carga.

## <a name="tasks"></a>Tarefas

|Tarefas|Tópicos associados|
|-|-|
|**Acessando os resultados do teste de carga:** quando você executar um teste de carga usando o Editor de Teste de Carga, os resultados do teste de carga serão abertos automaticamente e o teste de carga em execução será exibido no **Analisador de Teste de Carga**.|-   [Como acessar os resultados do teste de carga para análise](../test/how-to-access-load-test-results-for-analysis.md)|
|**Adicionar observações de análise ao teste de carga:** você pode adicionar comentários ao seu teste de carga quando você conduz sua análise. Os comentários são armazenados permanentemente, junto com o resultado do teste de carga. A descrição inserida também aparece na coluna **Descrição** associada ao teste de carga na caixa de diálogo **Abrir e Gerenciar Resultados dos Testes** no Editor de Teste de Carga.<br /><br /> Para saber mais, confira [Como acessar resultados do teste de carga para análise](../test/how-to-access-load-test-results-for-analysis.md).<br /><br /> Além disso, os comentários são exibidos quando você cria um relatório do Excel para os resultados de testes de carga.<br /><br /> Para saber mais, confira [Relatando resultados do teste de carga para comparações de testes ou análise de tendências](../test/compare-load-test-results.md).||
|**Analisando os resultados do teste de carga:** depois de acessar os dados de execução de teste de carga, você pode analisar os dados resultantes. Você pode exibir o Resumo do Teste de Carga para entender os resultados rapidamente. O resumo do teste de carga mostra os resultados-chave em um formato compacto e fácil de ler.<br /><br /> Você pode imprimir o resumo do teste de carga. Isso deixa prático usá-lo quando você comunica resultados aos participantes.<br /><br /> Você pode analisar os detalhes dos resultados do teste de carga usando os gráficos e tabelas dos resultados. Eles incluem **Erros**, **Páginas**, **Solicitações**, **Rastreamento do SQL**, **Testes**, **Limites** e **Transações**.|-   [Visão geral resumida dos resultados do teste de carga](../test/load-test-results-summary-overview.md)<br />-   [Como exibir resposta da página da Web](../test/how-to-view-web-page-response-time-in-a-load-test.md)<br />-   [Analisando violações de regra de limite](../test/analyze-threshold-rule-violations-in-load-tests.md)<br />-   [Analisar resultados do teste de carga na exibição Grafos](../test/analyze-load-test-results-in-the-graphs-view.md)<br />-   [Analisar resultados do teste de carga e erros na exibição Tabelas](../test/analyze-load-test-results-and-errors-in-the-tables-view.md)|
|**Analisando a atividade de usuário virtual nos resultados do teste de carga para isolar problemas de desempenho:** você pode usar o Gráfico de atividade do usuário virtual para visualizar o que os usuários virtuais estão fazendo durante um teste de carga. Isso pode ajudar a isolar picos em uma CPU ou quedas em solicitações/s, e determina quais testes ou páginas estão em execução durante esses picos e quedas.|-   [Analisando a atividade do usuário virtual na exibição Detalhes](../test/analyze-load-test-virtual-user-activity-in-the-details-view.md)|