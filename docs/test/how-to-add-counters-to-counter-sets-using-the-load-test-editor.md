---
title: Adicionar contadores a conjuntos de contadores para teste de carga
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- counters, counter sets
- counter sets
- load tests, counter sets
ms.assetid: e17d0e71-f982-4fc1-a2df-a1065d37473d
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: b2a6ba058ba7c09eb66c15cb578fcaaf36d2ced2
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52894697"
---
# <a name="how-to-add-counters-to-counter-sets-using-the-load-test-editor"></a>Como adicionar contadores a conjuntos de contadores usando o Editor de Teste de Carga

Quando cria um teste de carga com o **Assistente de Teste de Carga**, você adiciona um conjunto inicial de contadores. Isso oferece um conjunto de contadores predefinidos para seu teste de carga. Para saber mais, confira [Especificar os conjuntos de contadores e as regras de limite para computadores em um teste de carga](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md).

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

> [!NOTE]
> Se os testes de carga forem distribuídos por computadores remotos, os contadores de agente e controlador serão mapeados para os conjuntos de contadores de agente e controlador. Para obter mais informações sobre como usar computadores remotos no teste de carga, consulte [Controladores e agentes de teste](configure-test-agents-and-controllers-for-load-tests.md).

Você gerencia os contadores no **Editor de Teste de Carga**. Os conjuntos de contadores que já foram adicionados ao teste ficam visíveis no nó **Conjuntos de contadores** do teste de carga. Depois que você cria um teste de carga, você pode adicionar novos contadores aos conjuntos de contadores existentes.

## <a name="to-add-counters-to-a-counter-set"></a>Para adicionar contadores a um conjunto de contadores

1.  Abra um teste de carga.

2.  Expanda o nó **Conjuntos de contadores**. Todos os conjuntos de contadores que foram adicionados ao teste de carga estarão visíveis.

    > [!NOTE]
    > A árvore hierárquica de testes de carga também contém o nó **Configurações de execução**. Esse nó contém o nó **Mapeamentos de conjuntos de contadores**, que mostra todos os computadores e conjuntos de contadores mapeados para esses computadores.

3.  Clique com o botão direito do mouse em um conjunto de contadores existente e escolha **Adicionar contadores**.

     A caixa de diálogo **Selecionar contadores de desempenho** é exibida.

4.  Na caixa de combinação suspensa **Computador**, digite o nome do computador para o qual deseja mapear. Opcionalmente, selecione um dos computadores na lista suspensa.

    > [!NOTE]
    > Como os conjuntos de contadores devem ser mapeados para um computador antes que os dados de desempenho sejam coletados, você deve especificar um computador no qual coletar dados de desempenho.

5.  Selecione **Categoria de desempenho** para filtrar as categorias de contadores de dados de desempenho. Você verá duas colunas de dados para selecionar contadores de desempenho.

    > [!NOTE]
    > Algumas categorias de contadores exigirão que você selecione uma instância também. Por exemplo, se você selecionar o contador SQL, deverá selecionar uma instância SQL porque pode haver mais de uma instância do SQL instalada no computador de destino.

6.  Selecione um contador e uma instância para adicionar ao seu conjunto de contadores personalizado.

     \- ou -

     Selecione o botão de opção **Todos os contadores** para selecionar todos os contadores disponíveis.

7.  Escolha **OK**.

    > [!NOTE]
    > Também é possível adicionar contadores como um conjunto de contadores escolhendo um contador ou uma categoria de contador existente, selecionando Copiar e depois colando-o(a) em um nó diferente do conjunto de contadores. Os contadores extras que são copiados, mas não são necessários, podem ser excluídos.

## <a name="see-also"></a>Consulte também

- [Especificar os conjuntos de contadores e as regras de limite para computadores em um teste de carga](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)
- [Definir configurações de execução de teste de carga](../test/configure-load-test-run-settings.md)