---
title: Conjuntos de contadores de teste de carga
ms.date: 10/19/2016
ms.topic: how-to
f1_keywords:
- vs.test.load.dialog.countersetmapping
helpviewer_keywords:
- counters, counter sets
- performance counters
- counter sets
- load tests, counter sets
ms.assetid: 64315c2f-a0b2-4378-be16-0774b99beef5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1eeb99d58a9fc0547d118c529878d8b02cc83dda
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85287682"
---
# <a name="how-to-manage-counter-sets-using-the-load-test-editor"></a>Como gerenciar conjuntos de contadores usando o Editor de Teste de Carga

Quando cria um teste de carga com o **Novo Assistente de Teste de Carga**, você adiciona um conjunto de contadores inicial. Isso oferece um conjunto de contadores predefinidos para seu teste de carga.

> [!NOTE]
> Se os testes de carga forem distribuídos por computadores remotos, os contadores de agente e controlador serão mapeados para os conjuntos de contadores de agente e controlador. Para obter mais informações sobre como usar computadores remotos no teste de carga, consulte [Controladores e agentes de teste](configure-test-agents-and-controllers-for-load-tests.md).

Gerenciar conjuntos de contadores envolve escolher o conjunto de computadores do qual você deseja coletar dados de desempenho e atribuir um conjunto de contadores para coletar de cada computador individualmente. Você gerencia os contadores no **Editor de Teste de Carga**.

![Gerenciando conjuntos de contadores](../test/media/loadtestmanagecountersets.png)

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-manage-counter-sets"></a>Para gerenciar conjuntos de contadores

1. Abra um teste de carga.

2. Escolha o botão **Gerenciar conjuntos de contadores**.

     – ou –

     Clique com o botão direito do mouse na pasta **Conjuntos de contadores** na árvore do teste de carga e escolha **Gerenciar conjuntos de contadores**.

     A caixa de diálogo **Gerenciar conjuntos de contadores** é exibida.

3. (Opcional) Na caixa de listagem **Computadores e conjuntos de contadores selecionados serão adicionados nas seguintes configurações de execução**, selecione outra configuração de execução.

    > [!NOTE]
    > Isso se aplicará apenas se você tiver mais de uma configuração de execução no teste de carga.

4. (Opcional) Escolha **Adicionar Computador** para adicionar um novo computador ao monitor. Será solicitado que você forneça um nome. Digite o nome de um computador e você verá os nós abaixo da nova entrada. Por exemplo **ASP.NET**, **IIS**, **SQL**, entre outros. Marque as caixas de seleção na frente dos nós que deseja selecionar. Os contadores são exibidos no painel **Versão prévia das seleções**.

5. (Opcional) Na caixa de texto **Marcações de Computador**, digite uma marcação a ser associada ao computador. Por exemplo, "TestMachine12 em lab3".

     Os marcadores de computador permitem identificar um computador com um nome fácil de reconhecer.

     As marcações são exibidas no nó **Mapeamentos de conjuntos de contadores** da árvore no Editor de Teste de Carga. O mais importante é que os marcadores são exibidos em relatórios do Excel, o que ajuda os participantes a identificar qual função o computador tem no teste de carga. Por exemplo, "Web Server1 em lab2" ou "SQL Server2 em Phoenix office". Para saber mais, confira [Relatar resultados do teste de carga para comparações de testes ou análise de tendências](../test/compare-load-test-results.md).

6. Escolha **OK**.

## <a name="see-also"></a>Veja também

- [Controladores de teste e agentes de teste](configure-test-agents-and-controllers-for-load-tests.md)
- [Especificar os conjuntos de contadores e as regras de limite para computadores em um teste de carga](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)
- [Definir configurações de execução de teste de carga](../test/configure-load-test-run-settings.md)
