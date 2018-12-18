---
title: Analisando violações de regra de limite em testes de carga no Visual Studio
ms.date: 10/19/2016
ms.topic: conceptual
f1_keywords:
- vs.test.load.monitor.threshholdresult
helpviewer_keywords:
- load tests, thresholds
- threshold violations
- threshold counts
- load tests, threshold violations
- load test results, analyzing threshold violations
- thresholds in load tests
ms.assetid: 969ed346-cf2e-4d48-82b3-edb3e075e1c0
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 17a79e4c684ee60d18288bc30ce1e3fce83dc8a5
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895425"
---
# <a name="analyzing-threshold-rule-violations-in-load-tests-using-the-load-test-analyzer"></a>Analisando violações de regra de limite em testes de carga usando o Analisador de Teste de Carga

As regras de limite são associadas a contadores de desempenho específicos, e as violações indicam que um contador de desempenho excedeu ou ficou abaixo de um valor definido. Ao executar um teste de carga, você pode analisar as violações que ocorrem de acordo com as regras de limite definidas anteriormente.

Se ocorrer qualquer violação, um hiperlink de **violações de limite** aparecerá na barra de status do **Analisador de Teste de Carga** e especificará o número de violações que ocorreram. Você escolhe o hiperlink para exibir a tabela de violações de limite. Você também pode exibir violações de limite na janela **Contadores** e no gráfico.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="view-threshold-violations-in-the-table"></a>Exibir violações de limite na tabela

 A tabela de violações de limite exibe as primeiras 1.000 violações. A tabela a seguir contém estas colunas:

|Column|Descrição|Visível por padrão|
|-|-|-|
|Hora|O tempo durante o teste de carga em que a violação ocorreu.|Sim|
|Computador|O nome do computador em teste em que a violação ocorreu. **Observação:** isso é importante quando você executa testes de carga em equipamentos.|Sim|
|Categoria|A categoria do contador de desempenho em que a violação ocorreu.|Sim|
|Contador|O nome do contador de desempenho em que a violação ocorreu.|Sim|
|Instância|A instância do contador de desempenho em que a violação ocorreu.|Sim|
|Mensagem|Uma mensagem que descreve a violação de limite. Por exemplo, **O valor 5 excede o limite crítico de 0**.|Sim|

> [!NOTE]
> É possível classificar a tabela escolhendo-se os cabeçalhos de coluna.

 Para obter mais informações, consulte [Analisar resultados de teste de carga e erros na exibição Tabelas](../test/analyze-load-test-results-and-errors-in-the-tables-view.md).

## <a name="view-threshold-violations-in-the-counters-panel"></a>Exibir violações de limite no painel Contadores

 É possível exibir violações de limite no painel **Contadores**, na árvore que lista os contadores de desempenho para o teste de carga. Os ícones no painel **Contadores** informam violações de limite. O ícone será um dos seguintes:

 O ícone será um dos seguintes:

 ![Sem violação de limite](../test/media/icon_ltest_1.gif) Sem violação de limite.

 ![Uma violação de limite crítica no último intervalo](../test/media/icon_ltest_2.gif) Uma violação de limite crítica ocorreu no último intervalo.

 ![Uma violação de limite crítica em um intervalo anterior](../test/media/icon_ltest_3.gif) Uma violação de limite crítica ocorreu em um intervalo anterior.

 ![Uma violação de limite de aviso no último intervalo](../test/media/icon_ltest_4.gif) Uma violação de limite de aviso ocorreu no último intervalo.

 ![Uma violação de limite de aviso em um intervalo anterior](../test/media/icon_ltest_5.gif) Uma violação de limite de aviso ocorreu em um intervalo anterior.

 Se desejar, as violações de limite também podem ser mostradas no gráfico. O ícone de limite é exibido no gráfico ao lado do ponto de dados onde a violação de limite ocorreu.

 Na árvore de contadores, o ícone de uma violação de limite é propagado do nó de contador específico até o nó raiz. Isso alerta você para uma violação em um contador que pode não estar visível na árvore porque a árvore não foi expandida.

## <a name="view-threshold-violations-on-the-graph"></a>Exibir violações de limite no grafo

 Você pode ver violações de limite no gráfico De forma semelhante ao painel **Contadores**, os ícones informam as violações de limite no gráfico. Os ícones aparecem no gráfico ao lado do ponto de dados onde a violação de limite ocorreu. Se uma violação de limite ocorrer em um contador que não aparece no gráfico, você poderá adicioná-la ao gráfico arrastando-a do painel **Contadores** para o gráfico.

 Para obter mais informações, confira [Analisar os resultados do teste de carga na exibição Grafo](../test/analyze-load-test-results-in-the-graphs-view.md).

## <a name="see-also"></a>Consulte também

- [Especificando os conjuntos de contadores e as regras de limite para computadores em um teste de carga](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)
- [Analisar resultados do teste de carga](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
- [Analisar resultados do teste de carga e erros na exibição Tabelas](../test/analyze-load-test-results-and-errors-in-the-tables-view.md)