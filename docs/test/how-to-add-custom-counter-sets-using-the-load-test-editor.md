---
title: Adicionar conjuntos de contadores personalizados para teste de carga
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- counters, counter sets
- counter sets
- load tests, counter sets
ms.assetid: 499aca80-1069-408d-ac68-326da6a50645
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e2b78cb68f1e7a7e1f47c6cc3e771353d7e46ca9
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85288423"
---
# <a name="how-to-add-custom-counter-sets-using-the-load-test-editor"></a>Como adicionar conjuntos de contadores personalizados usando o Editor de Teste de Carga

Quando cria um teste de carga com o **Novo Assistente de Teste de Carga**, você adiciona um conjunto de contadores inicial. Isso oferece um conjunto de contadores predefinidos para seu teste de carga.

> [!NOTE]
> Se os testes de carga forem distribuídos por computadores remotos, os contadores de agente e controlador serão mapeados para os conjuntos de contadores de agente e controlador. Para obter mais informações sobre como usar computadores remotos no teste de carga, consulte [Controladores e agentes de teste](configure-test-agents-and-controllers-for-load-tests.md).

Você gerencia os contadores no **Editor de Teste de Carga**. Os conjuntos de contadores que já foram adicionados ao teste ficam visíveis no nó **Conjuntos de contadores** do teste de carga. Depois de criar um teste de carga, é possível adicionar a ele novos conjuntos de contadores personalizados.

![Conjunto de contadores personalizados](../test/media/loadtestcustomcounter.png)

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-add-a-custom-counter-set-to-a-load-test"></a>Para adicionar um conjunto de contadores personalizados a um teste de carga

1. Abra um teste de carga.

2. Expanda o nó **Conjuntos de contadores**. Todos os conjuntos de contadores que foram adicionados ao teste de carga estarão visíveis.

3. Clique com o botão direito do mouse no nó **Conjuntos de contadores** e selecione **Adicionar conjunto de contadores personalizados**.

    > [!NOTE]
    > O conjunto de contadores recebe um nome padrão, como **Custom1**. É possível alterar o nome usando a janela **Propriedades**. Pressione **F4** para exibir a janela **Propriedades**.

4. Para adicionar contadores ao conjunto de contadores personalizado, clique com o botão direito do mouse no novo conjunto de contadores e escolha **Adicionar contadores**. Para saber mais sobre como adicionar contadores, confira [Como adicionar contadores a conjuntos de contadores](../test/how-to-add-counters-to-counter-sets-using-the-load-test-editor.md).

    > [!NOTE]
    > Também é possível adicionar um conjunto de contadores personalizados clicando com o botão direito do mouse em um conjunto de contadores existente, escolhendo copiar e colando-o no nó de conjuntos de contadores. Os contadores adicionais que são copiados, mas não são necessários, podem ser excluídos. Você pode alterar o nome do novo conjunto de contadores usando a janela **Propriedades**.

## <a name="see-also"></a>Veja também

- [Especificar os conjuntos de contadores e as regras de limite para computadores em um teste de carga](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)
- [Definir configurações de execução de teste de carga](../test/configure-load-test-run-settings.md)
