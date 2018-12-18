---
title: Tempo de resposta da página em um teste de carga no Visual Studio
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, response times
- response times in load tests
- load test results, response times
ms.assetid: e61c49f3-3161-45b1-9220-08b5459065a2
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 9740d26ef99c10bb9ec84afa23b998f6e1467f40
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895256"
---
# <a name="how-to-view-web-page-response-time-in-a-load-test-using-the-load-test-analyzer"></a>Como exibir o tempo de resposta da página da Web em um teste de carga usando o Analisador de Teste de Carga

O tempo necessário para cada página da Web carregar é conhecido como *tempo de resposta*. Quando você cria um teste de desempenho na Web, pode definir uma meta de tempo de resposta para cada solicitação de página da Web no teste de desempenho na Web.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

Se você executar o teste de desempenho na Web sob estresse em um teste de carga, poderá analisar as seguintes informações para cada página:

-   O tempo médio de resposta da página.

-   A porcentagem de iterações de teste que correspondem à meta de tempo de resposta para a página.

-   Você pode analisar os tempos de resposta da página da Web usando a exibição Tabelas ou a exibição Grafos no **Analisador de Teste de Carga**:

-   Analisando o tempo de resposta da página da Web na exibição de tabelas

-   Analisando o tempo de resposta da página da Web na exibição de grafos

## <a name="view-response-time-data-in-a-table"></a>Exibir dados de tempo de resposta em uma tabela

1. No **Analisador de Teste de Carga**, escolha **Tabelas** na barra de ferramentas para garantir que a grade da tabela seja exibida.

2. Na caixa de listagem suspensa **Tabela**, selecione **Páginas**.

3. Os dados de cada página são exibidos na grade. As seguintes colunas são exibidas normalmente.

   |Título de coluna|Descrição|
   |-|-|
   |**Página**|O nome da página da Web.|
   |**Cenário**|O nome do cenário. Importante se você tiver mais de um cenário no teste de desempenho na Web.|
   |**Teste**|O nome do teste de desempenho na Web. Importante se você tiver mais de um teste de desempenho na Web em seu teste de carga.|
   |**Network**|O tipo de rede.<br /><br /> Por padrão, esses dados não são coletados. Para coletar esses dados, no **Editor de Teste de Carga**, no nó **Configurações de Execução**, selecione o nó da configuração de execução a ser alterado. Na janela **Propriedades**, para a propriedade de **Armazenamento de Detalhes de Medição de Tempo**, selecione **AllIndividualDetails**.|
   |**Total**|O número total de solicitações feitas para a página da Web. Esse é o total para todas as iterações no teste de carga.|
   |**Méd.**|Tempo médio de resposta da página.<br /><br /> Por padrão, esses dados não são coletados. Para coletar esses dados, no **Editor de Teste de Carga**, no nó **Configurações de Execução**, selecione o nó da configuração de execução a ser alterado. Na janela **Propriedades**, para a propriedade de **Armazenamento de Detalhes de Medição de Tempo**, selecione **AllIndividualDetails**.|
   |**Min**|O tempo de resposta mínimo da página.<br /><br /> Por padrão, esses dados não são coletados. Para coletar esses dados, no **Editor de Teste de Carga**, no nó **Configurações de Execução**, selecione o nó da configuração de execução a ser alterado. Na janela **Propriedades**, para a propriedade de **Armazenamento de Detalhes de Medição de Tempo**, selecione **AllIndividualDetails**.|
   |**Mediana**|O tempo de resposta mediana da página.<br /><br /> Por padrão, esses dados não são coletados. Para coletar esses dados, no **Editor de Teste de Carga**, no nó **Configurações de Execução**, selecione o nó da configuração de execução a ser alterado. Na janela **Propriedades**, para a propriedade de **Armazenamento de Detalhes de Medição de Tempo**, selecione **AllIndividualDetails**.|
   |**90%**|O 90º percentil para o tempo de resposta. Isso indica que 90% das páginas respondeu mais rápido do que esse número, e 10% das páginas respondeu mais lentamente.<br /><br /> Por padrão, esses dados não são coletados. Para coletar esses dados, no **Editor de Teste de Carga**, no nó **Configurações de Execução**, selecione o nó da configuração de execução a ser alterado. Na janela **Propriedades**, para a propriedade de **Armazenamento de Detalhes de Medição de Tempo**, selecione **AllIndividualDetails**.|
   |**95%**|O 95º percentil para o tempo de resposta. Isso indica que 95% das páginas respondeu mais rápido do que esse número e 5% das páginas respondeu mais lentamente.|
   |**99%**|O 99º percentil para o tempo de resposta. Isso indica que 99% das páginas respondeu mais rápido do que esse número e 1% das páginas respondeu mais lentamente.<br /><br /> Por padrão, esses dados não são coletados. Para coletar esses dados, no **Editor de Teste de Carga**, no nó **Configurações de Execução**, selecione o nó da configuração de execução a ser alterado. Na janela **Propriedades**, para a propriedade de **Armazenamento de Detalhes de Medição de Tempo**, selecione **AllIndividualDetails**.|
   |**Max**|O tempo de resposta máximo da página.<br /><br /> Por padrão, esses dados não são coletados. Para coletar esses dados, no **Editor de Teste de Carga**, no nó **Configurações de Execução**, selecione o nó da configuração de execução a ser alterado. Na janela **Propriedades**, para a propriedade de **Armazenamento de Detalhes de Medição de Tempo**, selecione **AllIndividualDetails**.|
   |**Desvio padrão**|Por padrão, os dados de desvio padrão não são coletados. Para coletar esses dados, no **Editor de Teste de Carga**, no nó **Configurações de Execução**, selecione o nó da configuração de execução a ser alterado. Na janela **Propriedades**, para a propriedade de **Armazenamento de Detalhes de Medição de Tempo**, selecione **AllIndividualDetails**.|
   |**Tempo da Página**|O tempo médio de resposta para todas as solicitações feitas para a página da Web.|
   |**Meta**|A meta de tempo da página. Esse é um valor constante para a página. **Observação:** a meta de tempo da página é exibida somente quando a meta é definida para a solicitação no teste de desempenho Web.|
   |**Meta da reunião %**|A porcentagem de solicitações feitas para a página da Web que atingiu a meta de tempo de resposta.|

   Para obter mais informações, consulte [Analisar resultados de teste de carga e erros na exibição Tabelas](../test/analyze-load-test-results-and-errors-in-the-tables-view.md).

## <a name="view-response-time-data-in-a-graph"></a>Exibir dados de tempo de resposta em um grafo

Você também pode exibir dados de tempo de resposta em um gráfico para ver como eles mudam com o passar do tempo durante o teste de carga. Isso é especialmente útil se seu padrão de carga aumenta conforme a execução do teste (por exemplo, se você usar o padrão de carga por etapa). Para obter mais informações, confira [Editar padrões de carga para modelar atividades de usuário virtual](../test/edit-load-patterns-to-model-virtual-user-activities.md).

Para exibir dados de tempo de resposta em um gráfico:

1. No **Analisador de Teste de Carga**, escolha **Grafos** na barra de ferramentas para garantir que o grafo seja exibido.

2. Na janela **Contadores**, expanda o nó do cenário no qual você está interessado (por exemplo, `Scenario1`).

3. Expanda o nó de teste de desempenho na Web no qual você está interessado.

4. Expanda o nó **Páginas**.

5. Expanda o nó da página no qual você está interessado.

6. Clique com o botão direito do mouse em **% de Páginas que Atendem à Meta** e escolha **Mostrar Contador no Gráfico**.

    Os dados são adicionado ao gráfico.

7. (Opcional) Repita a etapa anterior para **Tempo Méd. Página**, **Meta de Tempo de Resposta da Página** e **Total de Páginas**.

   > [!NOTE]
   > A **Meta de Tempo de Resposta da Página** é constante.

   Para obter mais informações, confira [Analisar os resultados do teste de carga na exibição Grafo](../test/analyze-load-test-results-in-the-graphs-view.md).

## <a name="see-also"></a>Consulte também

- [Analisar resultados do teste de carga e erros na exibição Tabelas](../test/analyze-load-test-results-and-errors-in-the-tables-view.md)
- [Como acessar os resultados do teste de carga para análise](../test/how-to-access-load-test-results-for-analysis.md)
- [Analisar resultados do teste de carga](../test/analyze-load-test-results-using-the-load-test-analyzer.md)