---
title: Analisar os resultados do teste de carga
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- results, load test
- load test results, accessing
- Load Test Viewer
- load tests, accessing
- load tests, analyzing
- load tests, results
- Load Test Viewer, viewing
ms.assetid: b0a3e694-2894-479b-b270-7e61e9fafacd
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b72db87014304dc2b9baf57e05015e53a630c431
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85288527"
---
# <a name="how-to-access-load-test-results-for-analysis"></a>Como acessar os resultados do teste de carga para análise

Quando você executar um teste de carga do Editor de Teste de Carga, os resultados de testes de carga serão abertos automaticamente e o teste de carga em execução será exibido no **Analisador de Teste de Carga**. Ao executar um teste de carga da linha de comando, você deverá acessar os resultados de testes de carga manualmente.

O resultado de teste de carga para o teste de carga concluído contém exemplos de contador de desempenho e informações de erros que foram coletados periodicamente dos computadores em teste. Um grande número de exemplos de contador de desempenho podem ser coletados durante a execução de um teste de carga. A quantidade de dados de desempenho coletados depende do tamanho da execução do teste, do intervalo de amostragem, do número de computadores em teste, do número de contadores que estão sendo coletados, dos coletores de dados que são configurados e dos níveis de registro em log. Em um teste de carga grande, a quantidade de dados de desempenho coletados pode atingir facilmente vários gigabytes. Para obter mais informações, consulte [Test Controllers and Test Agents](configure-test-agents-and-controllers-for-load-tests.md).

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-access-a-load-test-result"></a>Para acessar um resultado de teste local

1. De um projeto de teste de carga e de desempenho na Web, abra um teste de carga.

2. Na barra de ferramentas do Editor de Teste de Carga, clique no botão **Abrir e gerenciar resultados**.

     A caixa de diálogo **Abrir e gerenciar resultados** é exibida.

3. Em **Digite um nome de controlador para encontrar resultados de testes de carga**, selecione um controlador. Selecione ** \<local> -nenhum controlador** para acessar os resultados armazenados localmente.

4. Em **Exibir resultados para o seguinte teste de carga**, selecione o teste de carga cujos resultados deseja exibir. Selecione **\<Show results for all tests>** para ver todos os resultados de todos os testes.

     Se houver resultados de testes de carga disponíveis, eles aparecerão na lista **Resultados de testes de carga**. As colunas são **Hora**, **Duração**, **Usuário**, **Resultado**, **Teste** e **Descrição**. **Teste** contém o nome do teste e **Descrição** contém a descrição opcional adicionada antes da execução do teste.

    > [!NOTE]
    > Os resultados aparecem com os resultados mais recentes na parte superior da lista.

5. Na lista **Resultados de testes de carga**, selecione os resultados do teste de carga para analisar e escolha **Abrir**.

6. O **Analisador de Testes de Carga** é exibido. O resultado do teste de carga selecionado é exibido na exibição Resumo. Para saber mais, confira [Visão geral do resumo de resultados de teste de carga](../test/load-test-results-summary-overview.md).

     Você pode gerenciar os outros aspectos de resultados do teste da carga na caixa de diálogo **Abrir e gerenciar resultados**, que inclui importar, exportar e remover resultados do teste de carga. Para saber mais, confira [Gerenciar resultados do teste de carga no repositório de resultados do teste de carga](../test/manage-load-test-results-in-the-load-test-results-repository.md).

## <a name="see-also"></a>Veja também

- [Analisar resultados do teste de carga](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
