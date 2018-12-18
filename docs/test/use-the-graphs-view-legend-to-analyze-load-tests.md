---
title: Usando a legenda de exibição de gráficos para analisar testes de carga no Visual Studio
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- Load Test Analyzer, graphs view legend
- load tests, graphs view legend
ms.assetid: 0f6ba8e4-1343-419c-8a9f-240cf50efed7
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 082b3da934e602aef2f0c4eefcfffc45da2c40f0
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52896075"
---
# <a name="use-the-graphs-view-legend-to-analyze-load-tests"></a>Usar a legenda da exibição Grafos para analisar testes de carga

A exibição Gráficos do Analisador de Testes de Carga inclui um painel de legenda que exibe informações para cada contador de desempenho associado ao gráfico selecionado atualmente.

![Legenda de exibição dos gráficos](../test/media/load_viewlegend.png)

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

As seguintes informações estão contidas na legenda:

-   **Mostrar no gráfico:** use as caixas de seleção para especificar se a linha de um determinado contador, como **Carga do usuário** ou **Erros/s**, é plotada no gráfico. Marque uma caixa de seleção se você quiser que a linha seja plotada no grafo. Desmarque uma caixa de seleção para remover a linha de plotagem do gráfico. Quando uma linha de plotagem é removida, as estatísticas do contador continuam sendo exibidas na legenda.

-   **Intervalo:** esta coluna exibe o intervalo do eixo y do contador de desempenho. Por padrão, esse valor se ajustará automaticamente à medida que o intervalo de dados de exemplo mudar. Um intervalo definido automaticamente sempre será a próxima potência de 10 maior que o valor máximo; isso inclui potências negativas de dez. Um gráfico pode conter vários contadores, cada um com um intervalo diferente. Por isso, o eixo y não é identificado com nenhum intervalo específico, e sim identificado com valores de 0-100 que representam uma porcentagem do intervalo total para cada contador. Por exemplo, para um contador com um intervalo de 1.000, um ponto de dados de 60 no eixo y corresponderia a um valor de 600 para o contador.

    > [!NOTE]
    > Você pode desativar o ajuste de valor do intervalo automático bloqueando o intervalo em um valor específico. Quando o intervalo é bloqueado, todos os valores excedendo o intervalo são exibidos como o valor máximo que você especificou na parte superior do gráfico. Use a caixa de diálogo **Opções de plotagem** para bloquear o intervalo em um valor específico.

-   **Contador:** as quatro colunas chamadas **Contador**, **Instância**, **Categoria** e **Computador** identificam com exclusividade o contador de desempenho.

-   **Cor:** a coluna **Cor** mostra a cor e o estilo da linha plotada do contador de desempenho. Use a caixa de diálogo **Opções de plotagem** para alterar a cor ou o estilo da linha de um contador de desempenho no gráfico. A caixa de diálogo **Opções de plotagem** está disponível no menu de atalho da legenda.

-   **Estatísticas:** as colunas **Mín.**, **Máx.**, **Média** e **Último** mostram as respectivas estatísticas do contador de desempenho. Esses valores correspondem aos dados exibidos na região visível do gráfico. Por exemplo, se você ampliar uma região de uma execução, as estatísticas da legenda refletirão valores somente da área ampliada. A coluna "Último" é o valor do contador de desempenho do intervalo de amostragem concluído mais recentemente.

    > [!NOTE]
    > A coluna Último só é exibida na legenda do Analisador de Testes de Carga quando o teste de carga está em execução.

     Para saber mais, confira [Como ampliar uma região do grafo](../test/how-to-zoom-in-on-a-region-of-the-graph-in-load-test-results.md).

A seleção de um item na legenda faz o seguinte:

-   Permite que o item seja removido da legenda e do gráfico. Clique com o botão direito do mouse no item e selecione **Excluir** ou pressione a tecla **Delete**.

-   Realça a linha plotada no gráfico.

-   Faz a grade de dados exibir dados do item selecionado.

-   Permite acessar a caixa de diálogo **Opções de plotagem** do contador.

> [!TIP]
> Use o botão suspenso **Opções de Grafo** na barra de ferramentas do **Analisador de Teste de Carga** e selecione **Mostrar Legenda** para mostrar ou ocultar o painel **Legenda** associado à exibição de grafo.

## <a name="see-also"></a>Consulte também

- [Como ampliar uma região do grafo](../test/how-to-zoom-in-on-a-region-of-the-graph-in-load-test-results.md)
- [Analisar resultados do teste de carga na exibição Grafos](../test/analyze-load-test-results-in-the-graphs-view.md)
