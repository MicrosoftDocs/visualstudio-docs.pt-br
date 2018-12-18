---
title: Como criar gráficos personalizados em resultados do teste de carga no Visual Studio
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load test results graphs, creating
- load test results graphs
ms.assetid: 17fcafce-76f9-4411-9389-6e5376eab236
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 7973fbf5ac81da2ba603aacb201b7592e602969e
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895815"
---
# <a name="how-to-create-custom-graphs-in-load-test-results"></a>Como criar grafos personalizados em resultados do teste de carga

Você pode projetar gráficos que exibam informações específicas sobre resultados de teste de carga. Você cria um gráfico personalizado especificando os contadores de teste de carga que o gráfico exibirá.

Você pode executar o procedimento a seguir enquanto um teste de carga está em execução ou depois de concluir a execução.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-create-a-custom-load-test-results-graph"></a>Para criar um grafo de resultados de teste de carga personalizado

1.  Na barra de ferramentas **Teste de Carga**, escolha **Adicionar um Novo Grafo**.

     \- ou -

     No **Analisador de Teste de Carga**, clique com o botão direito do mouse no painel **Contadores** ou em um grafo e, em seguida, selecione **Adicionar Grafo**.

     A caixa de diálogo **Digite o nome do gráfico** é exibida.

2.  Em **Nome do gráfico**, digite um nome para o gráfico e escolha **OK**.

     O novo grafo é exibido no **Analisador de Teste de Carga**. Ele é exibido no painel de gráfico selecionado no momento; ele substitui o gráfico que foi exibido nesse painel.

3.  Personalize o novo gráfico adicionando contadores. Para saber mais, confira [Como adicionar e excluir contadores em gráficos](../test/how-to-add-and-delete-counters-on-graphs-in-load-test-results.md).

## <a name="see-also"></a>Consulte também

- [Analisar resultados do teste de carga na exibição Grafos](../test/analyze-load-test-results-in-the-graphs-view.md)
- [Como adicionar e excluir contadores em grafos](../test/how-to-add-and-delete-counters-on-graphs-in-load-test-results.md)