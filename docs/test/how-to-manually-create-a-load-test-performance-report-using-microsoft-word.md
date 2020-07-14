---
title: Criar um relatório de desempenho de teste de carga usando o Microsoft Word
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- load tests, reporting
- load tests, creating Word reports
ms.assetid: 3b864c75-2699-48c1-a2b4-9651f108c267
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f630c0e5c054185dcc0dcb87f553dff8dd2ad8f7
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85287591"
---
# <a name="how-to-manually-create-a-load-test-performance-report-using-microsoft-word"></a>Como criar manualmente um relatório de desempenho de teste de carga usando o Microsoft Word

Você pode criar manualmente relatórios de teste de carga do Microsoft Word copiando e colando dados da exibição de gráficos e da exibição resumida Resultados de Teste de Carga. Os dados que são apresentados na exibição resumida e na exibição de gráficos são aplicados no formato HTML quando são copiados.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

> [!TIP]
> Você pode copiar texto sem formatação da exibição de tabelas e de capturas de tela da exibição de detalhes no Microsoft Word, mas o texto não é aplicado no formato HTML e exigirá formatação e edição adicionais.

> [!TIP]
> Também é possível gerar relatórios organizados do Microsoft Excel automaticamente. Para obter mais informações, confira [Como criar relatórios de desempenho de teste de carga usando o Microsoft Excel](../test/how-to-create-load-test-performance-reports-using-microsoft-excel.md).

## <a name="copy-summary-view-data"></a>Copiar dados da exibição resumida

1. No **resultados de teste de carga**, se a exibição de resumo não for exibida no momento, clique em **Resumo** na barra de ferramentas.

2. Na exibição resumida, clique com o botão direito do mouse e selecione **Selecionar Tudo**.

3. Na exibição resumida, clique com o botão direito do mouse e selecione **Copiar**. Isso renderiza os dados da exibição resumida como formato HTML na área de transferência.

4. No Microsoft Word, cole os dados da exibição resumida no local desejado.

5. Agora é possível modificar, formatar e excluir aspectos do conteúdo copiado para que ele atenda às suas necessidades de relatório.

## <a name="copy-graph-view-data"></a>Copiar dados de exibição de gráfico

1. Se a exibição de grafos não estiver sendo mostrada nos **Resultados do Teste de Carga**, escolha **Grafos** na barra de ferramentas.

2. (Opcional) Amplie o gráfico específico que você deseja copiar no documento do Microsoft Word, conforme mostrado na ilustração a seguir. Para obter mais informações, consulte [como ampliar uma região do grafo](../test/how-to-zoom-in-on-a-region-of-the-graph-in-load-test-results.md).

     ![Controle de zoom da exibição de grafo](../test/media/ltest_zoomcontrol.png)

3. No gráfico que deseja copiar no documento do Microsoft Word, clique com o botão direito do mouse e selecione **Copiar**.

4. No Microsoft Word, cole o gráfico e os dados da tabela associada no local desejado.

    > [!WARNING]
    > Não é possível copiar o gráfico de uma área de trabalho remota e colá-lo em outro computador, pois somente as informações da tabela associada ao gráfico serão copiadas, e não a imagem do gráfico. A imagem do gráfico é armazenada no diretório temporário do computador do qual ela foi copiada e o segundo computador não pode desreferenciar esse diretório.

## <a name="see-also"></a>Veja também

- [Relatar resultados do teste de carga para comparações de testes ou análise de tendências](../test/compare-load-test-results.md)
- [Como criar relatórios de desempenho de teste de carga usando o Microsoft Excel](../test/how-to-create-load-test-performance-reports-using-microsoft-excel.md)
