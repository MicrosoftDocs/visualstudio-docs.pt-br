---
title: Adicionar e excluir contadores em grafos nos resultados do teste de carga
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- load test results graphs, adding counters
- load test results graph
- load test, results graph
- load test results, graphs
ms.assetid: 81536233-1962-40d9-9511-0b4633814d90
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2b2cefc56d299c9ec917aea555aec1cd9ca53887
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85288462"
---
# <a name="how-to-add-and-delete-counters-on-graphs-in-load-test-results"></a>Como adicionar e excluir contadores em gráficos em resultados de teste de carga

Você pode usar o painel **Contadores** para adicionar contadores de desempenho a um grafo.

![Contador adicionado ao grafo](../test/media/ltest_selectcounter.png)

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

**Considerações de intervalo de amostragem do contador de desempenho**

Escolha um valor para a propriedade **Taxa de Amostragem** nas configurações de execução de teste de carga com base na duração do seu teste de carga. Uma taxa de amostragem menor, como o valor padrão de cinco segundos, requer mais espaço no banco de dados dos resultados de testes de carga. Para testes de carga mais longos, aumentar a taxa de amostragem reduzirá a quantidade de dados coletados. Para saber mais, confira [Como especificar a taxa de amostragem](../test/how-to-specify-the-sample-rate-for-a-load-test.md).

Veja algumas diretrizes para taxas de amostragem:

|Duração do teste de carga|Taxa de amostragem recomendada|
|-|-----------------------------|
|\< 1 hora|5 segundos|
|1 a 8 horas|15 s|
|8 a 24 horas|30 segundos|
|> 24 horas|60 segundos|

**Considerações para incluir detalhes de tempo para coletar dados de percentil**

Há uma propriedade nas configurações de execução no Editor de Teste de Carga denominada **Armazenamento de detalhes de medição de tempo**. Se a propriedade **Armazenamento de detalhes de medição de tempo** estiver habilitada, o tempo para execução de cada teste, transação e página individual durante o teste de carga será armazenado no repositório de resultados de testes de carga. Isso permite que os 90º e 95º dados de percentil sejam mostrados no **Analisador de Teste de Carga** nas tabelas Testes, Transações e Páginas.

Há duas opções para habilitar a propriedade **Armazenamento de detalhes de medição de tempo** nas propriedades de configurações de execução, denominadas **StatisticsOnly** e **AllIndividualDetails**. Seja qual opção for escolhidas, todos os testes, páginas e transações individuais são cronometrados, e os dados de percentil são calculados dos dados de medição de tempo individuais. A diferença é que, com a opção **StatisticsOnly**, assim que os dados de percentil são calculados, os dados de medição de tempo individuais são excluídos do repositório. Isso reduz a quantidade de espaço necessário no repositório quando você usa detalhes de medição de tempo. No entanto, os usuários avançados podem querer processar os dados detalhados de medição de tempo de outras formas, usando ferramentas SQL. Nesse caso, a opção **AllIndividualDetails** deve ser usada para que os dados detalhados de medição de tempo estejam disponíveis para esse processamento. Além disso, se você definir a propriedade para **AllIndividualDetails**, será possível analisar a atividade do usuário virtual usando o gráfico de **Atividade de Usuário Virtual** no **Analisador de Teste de Carga** após a conclusão da execução do teste de carga. Para saber mais, confira [Análise da atividade de usuário virtual na exibição Detalhes](../test/analyze-load-test-virtual-user-activity-in-the-details-view.md).

A quantidade de espaço necessária no repositório de resultados de testes de carga para armazenar os dados detalhados de medição de tempo pode ser muito grande, especialmente para testes de carga mais longos. Além disso, o tempo para armazenar esses dados no repositório de resultados de testes de carga no final do teste de carga é mais longo, pois esses dados são armazenados nos agentes de teste de carga até que o teste de carga seja concluído. Quando o teste de carga é concluído, os dados são armazenados no repositório. Por padrão, a propriedade **Armazenamento de detalhes de medição de tempo** fica habilitada. Se isso for um problema para o seu ambiente de teste, talvez seja conveniente definir o **Armazenamento de detalhes de medição de tempo** como **Nenhum**.

Para saber mais, confira [Como especificar a propriedade de armazenamento dos detalhes de medição de tempo](../test/how-to-specify-the-timing-details-storage-property-for-a-load-test.md).

## <a name="to-display-a-particular-performance-counter-on-a-load-test-graph"></a>Para exibir um contador de desempenho específico em um gráfico de teste de carga

1. Depois que um teste de carga é concluído ou depois que você carregar um resultado do teste, na barra de ferramentas do Analisador de Teste de Carga, escolha **Gráficos**.

     O painel **Contadores** é mostrado na exibição Gráficos.

    > [!NOTE]
    > Se o painel **Contadores** não estiver visível, escolha **Mostrar painel de contadores** na barra de ferramentas.

2. No painel **Contadores**, expanda os nós na hierarquia até encontrar o contador de desempenho que você deseja ver graficamente.

     Por exemplo, para exibir a memória disponível em um computador em que os testes estão em execução, expanda **Computadores**, expanda o nó do computador e, em seguida, expanda **Memória**. Você verá o contador **MBytes disponíveis**.

3. Escolha o gráfico no qual você deseja exibir o contador de desempenho.

4. Clique com o botão direito do mouse no contador de desempenho no painel **Contadores** e selecione **Mostrar Contador no Gráfico**.

    > [!TIP]
    > Para interromper temporariamente a exibição dos dados do contador de desempenho no gráfico, desmarque a caixa de seleção para o contador de desempenho na legenda. Isso permite que as estatísticas de mínimo, máximo e média ainda sejam analisadas sem exibir a linha de tendência no gráfico. Isso pode ser útil se o gráfico contiver vários traçados do contador de desempenho que se sobrepõem quando você analisar os problemas. Para saber mais, confira [Usar a legenda de exibição Grafos para analisar testes de carga](../test/use-the-graphs-view-legend-to-analyze-load-tests.md).

5. Para remover os dados do contador de desempenho do gráfico, clique com o botão direito do mouse no contador de desempenho na coluna de **Contador** da legenda e selecione **Excluir**.

     \- ou –

     Clique com o botão direito do mouse na linha de dados do gráfico e selecione **Excluir**.

     \- ou –

     Escolha o contador de desempenho na coluna **Contador** de legenda ou na linha de dados do gráfico e pressione a tecla **Delete**.

    > [!NOTE]
    > Você também pode optar por colocar um contador de desempenho na legenda, mas não no gráfico, usando o comando **Adicionar contador na legenda**.

## <a name="see-also"></a>Veja também

- [Analisar resultados do teste de carga na exibição Grafos](../test/analyze-load-test-results-in-the-graphs-view.md)
- [Como criar gráficos personalizados](../test/how-to-create-custom-graphs-in-load-test-results.md)
