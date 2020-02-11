---
title: Analisar a Atividade de Usuário Virtual em testes de carga
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- virtual user activity chart, viewing
ms.assetid: 8bda19b3-91c1-4daf-b6c7-09108bddadff
author: jillre
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: dda1f35a63d3f7788faf9a94f16888c8323529c4
ms.sourcegitcommit: 00ba14d9c20224319a5e93dfc1e0d48d643a5fcd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "77091711"
---
# <a name="how-to-analyze-what-virtual-users-are-doing-during-a-load-test-using-the-virtual-user-activity-chart"></a>Como analisar o que usuários virtuais estão fazendo durante um teste de carga usando o gráfico de atividade de usuário virtual

Veja a atividade do usuário virtual associado ao seu teste de carga usando o **Gráfico de atividade de usuário virtual**. Cada linha do gráfico representa um usuário virtual individual. O **Gráfico de Atividade de Usuário Virtual** mostra exatamente o que cada usuário virtual executou durante o teste. É possível ver padrões de atividade de usuário, padrões de carga, correlacionar testes reprovados ou lentos e ver solicitações com outra atividade de usuário virtual. O **Gráfico de Atividade de Usuário Virtual** está disponível apenas depois da conclusão da execução do teste de carga.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

Os procedimentos a seguir demonstram como exibir o **Gráfico de atividade do usuário virtual**, como investigar as atividades de um usuário específico e como usar a filtragem.

## <a name="to-view-the-virtual-user-activity-chart-in-your-load-test-results"></a>Para ver o Gráfico de Atividade de Usuário Virtual nos resultados do teste de carga

1. Para exibir os dados do usuário virtual, primeiro você precisa definir a configuração **Todos os detalhes individuais** para a propriedade **Armazenamento de detalhes de medição de tempo** associada ao teste de carga. Em seguida, execute o teste de carga.

2. Após a execução do teste de carga, a página de resumo dos resultados do teste é exibida. Escolha o botão **Detalhes do Usuário** na barra de ferramentas.

     - ou -

     Abra a exibição Gráficos escolhendo o botão **Gráficos** na barra de ferramentas. Clique com o botão direito do mouse em um gráfico e selecione **Ir para detalhe do usuário**.

     Se você usar essa opção, o **Gráfico de Atividade de Usuário Virtual** ampliará automaticamente na parte do teste em que você clicou com o botão direito do mouse. Por exemplo, se o ponteiro estiver localizado aproximadamente na marca de 30 segundos, a exibição de detalhes será mostrada aproximadamente na marca 30second na ferramenta **Zoom para o período de tempo** na parte inferior do **Gráfico de atividade do usuário virtual**.

     Em seguida, você pode usar investigar detalhes de uma atividade de usuários específicos no **Gráfico de Atividade de Usuário Virtual**.

## <a name="to-investigate-a-specific-users-activity-in-the-virtual-user-activity-chart"></a>Para investigar detalhes de uma atividade de usuários específicos no Gráfico de Atividade de Usuário Virtual

1. Use a ferramenta Zoom para o período de tempo na parte inferior do **Gráfico de Atividade de Usuário Virtual** para selecionar uma área do gráfico onde você deseja investigar detalhes sobre um usuário específico.

2. Mova o ponteiro sobre um detalhe no gráfico. Observe que as informações a seguir são exibidas na dica de ferramenta:

   - **ID de usuário**

   - **Cenário**

   - **Test**

   - **URL** (Não é exibido em um teste ou transação)

   - **Resultado**

   - **Navegador** (Não é exibido em um teste ou transação)

   - **Rede**

   - **Start Time**

   - **Duration**

   - **Agente**

   - **Log de teste** (Link para o log de teste)

     > [!NOTE]
     > Para ajudar a depurar seu aplicativo, se você escolher o link **Log de teste**, o resultado do teste na Web ou do teste de unidade associado ao log será aberto.

     Em seguida, você pode usar as operações de filtragem e realce disponíveis no **Gráfico de Atividade de Usuário Virtual**.

## <a name="to-use-filtering-options-in-the-virtual-user-activity-chart"></a>Para usar as opções de filtragem no Gráfico de Atividade de Usuário Virtual

1. Na **legenda Detalhes**, use a lista suspensa para selecionar **Teste**, **Página** ou **Transação**.

    **Painel de Legenda de detalhes**

    ![Painel de legenda de detalhes](../test/media/ltest_detailslegend.png)

2. Marque ou desmarque as caixas de seleção dos erros, logs, testes, pesquisas e páginas aspx associados ao teste de carga.

    O **Gráfico de Atividade de Usuário Virtual** é atualizado de acordo.

    O **Gráfico de Atividade de Usuário Virtual** fornece a capacidade de filtrar testes, páginas e transações com base em diferentes critérios. Você pode remover alguns testes da exibição, remover todos os testes com êxito ou remover os testes reprovados com certas falhas. Também é possível remover todos os testes que não possuem logs.

    Por exemplo, é possível selecionar a opção **(Realçar erros)** , que exibe todos os erros no carrinho colorido em vermelho. Também é possível selecionar a opção **(Realçar resultados com registros)** , que exibe todos os resultados do teste que têm os logs coloridos em verde no gráfico.

    **Painel Filtrar resultados**

    ![Painel Filtrar resultados](../test/media/ltest_filterresults.png)

3. Em **Filtrar resultados**, marque ou desmarque as caixas de seleção das seguintes opções de filtro:

   - **Mostrar apenas os resultados com logs** Exibe apenas resultados de teste com logs de teste associados.

   - **Mostrar resultados bem-sucedidos** Exibe resultados bem-sucedidos.

   - **Mostrar resultados com erros** Exibe resultados com erros que podem ajudar na depuração.

     > [!NOTE]
     > A lista de tipos de erros listados no nó **Mostrar resultados com erros** pode ser mais investigada escolhendo o botão **Tabelas** na barra de ferramentas do **Visualizador de Resultados de Testes de Desempenho Web**. Para saber mais, confira [Analisar resultados de teste de carga e erros na exibição Tabelas](../test/analyze-load-test-results-and-errors-in-the-tables-view.md).

     O **Gráfico de Atividade de Usuário Virtual** é atualizado de acordo.

## <a name="see-also"></a>Consulte também

- [Analisando a atividade do usuário virtual na exibição Detalhes](../test/analyze-load-test-virtual-user-activity-in-the-details-view.md)
- [Passo a passo: Usando o gráfico de atividade do usuário virtual para isolar problemas](../test/walkthrough-use-the-virtual-user-activity-chart-to-isolate-issues.md)