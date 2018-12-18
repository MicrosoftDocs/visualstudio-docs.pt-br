---
title: Analisando a atividade do usuário virtual do teste de carga no Visual Studio
ms.date: 10/03/2016
ms.topic: conceptual
f1_keywords:
- vs.test.load.monitor.activitychart
helpviewer_keywords:
- virtual user activity chart
- load test, virtual user activity chart
ms.assetid: 63f4bd42-3cfb-4eee-af68-e8334976539e
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 58ab8859bffa89ae19eed6d37c442b71f98ef224
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52896088"
---
# <a name="analyzing-load-test-virtual-user-activity-in-the-details-view-of-the-load-test-analyzer"></a>Analisando a atividade do usuário virtual do teste de carga na exibição Detalhes do Analisador de Teste de Carga

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

**Gráfico de atividade do usuário virtual**

![Gráfico de Atividade de Usuário Virtual](../test/media/virtual_actchart.png)

A exibição **Detalhes** mostra o **Gráfico de Atividade do Usuário Virtual**, que é usado para analisar visualmente o que os usuários virtuais individuais fizeram durante o teste de carga. O **Gráfico de Atividade do Usuário Virtual** permite visualizar padrões de atividade do usuário e padrões de carga, correlacionar testes com falha ou lentos e ver as solicitações com outra atividade de usuário virtual. O **Gráfico de Atividade do Usuário Virtual** também pode ajudar a determinar picos de uso da CPU, quedas nas solicitações por segundo e quais testes ou páginas estavam em execução durante os picos e as quedas.

> [!NOTE]
> Antes de executar o teste de carga no qual você deseja usar o **Gráfico de Detalhes da Atividade do Usuário Virtual**, é necessário verificar se a propriedade **Armazenamento de Detalhes de Tempo** está definida como a opção **AllIndividualDetails** usando o Editor de Teste de Desempenho de Carga.

 **Painel de legenda de detalhes**

 ![Painel de legenda de detalhes](../test/media/ltest_detailslegend.png)

 O painel de legenda de detalhes está visível no **Gráfico de Atividade do Usuário Virtual**. O painel permite filtrar testes, páginas e transações com base em vários critérios diferentes. Por exemplo, você pode remover alguns testes da exibição, ou remover todos os testes com êxito, ou remover testes reprovados com determinadas falhas. Também é possível remover todos os testes que não possuem logs.

 Você pode realçar testes que falharam, o que exibe todos os testes com falha em vermelho. Também é possível realçar testes que possuem logs de teste. Os testes com logs serão coloridos de verde.

 **Painel Filtrar resultados**

 ![Painel Filtrar resultados](../test/media/ltest_filterresults.png)

 O painel Resultados do filtro está visível no **Gráfico de Atividade do Usuário Virtual**. Esse painel pode filtrar o seguinte:

-   **Mostrar apenas os resultados com logs** Exibe apenas resultados de teste com logs de teste associados.

-   **Mostrar resultados bem-sucedidos** Exibe resultados bem-sucedidos.

-   **Mostrar resultados com erros** Exibe resultados com erros que podem ajudar na depuração.

## <a name="tasks"></a>Tarefas

|Tarefas|Tópicos associados|
|-|-|
|**Executar o teste de carga:** depois de criar um teste de carga e configurá-lo para permitir a coleta dos dados de atividade do usuário virtual, será necessário executar o teste até sua conclusão para exibir o **Gráfico de Atividade do Usuário Virtual**.||
|**Exibir os resultados dos testes de carga que contêm os dados de atividade do usuário virtual:** depois que o teste de carga tiver sido criado e configurado e sua execução estiver concluída, você poderá exibir os dados de atividade do usuário virtual usando o **Gráfico de Atividade do Usuário Virtual**.|-   [Analisar resultados do teste de carga](../test/analyze-load-test-results-using-the-load-test-analyzer.md)<br />-   [Como analisar o que os usuários virtuais fazem durante um teste de carga](../test/how-to-analyze-virtual-user-activity-during-a-load-test.md)|
|**Isolar problemas de desempenho em testes de carga:** você pode usar o **Gráfico de Atividade do Usuário Virtual** para ajudar a isolar problemas de desempenho em seu teste de carga.|-   [Passo a passo: usando o gráfico de atividade do usuário virtual para isolar problemas](../test/walkthrough-use-the-virtual-user-activity-chart-to-isolate-issues.md)|

## <a name="see-also"></a>Consulte também

- [Analisar resultados do teste de carga](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
- [Analisar resultados do teste de carga e erros na exibição Tabelas](../test/analyze-load-test-results-and-errors-in-the-tables-view.md)