---
title: Adicionar uma regra de limite para teste de carga
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, monitoring
- load tests, thresholds
- load tests, analyzing
- thresholds in load tests
ms.assetid: 3d8fac8f-426f-4155-9ced-f7cd4c79792c
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4ecec4826966205d849c07169da954198d687696
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2019
ms.locfileid: "72644436"
---
# <a name="how-to-add-a-threshold-rule-using-the-load-test-editor"></a>Como adicionar uma regra de limite usando o Editor de Teste de Carga

As regras de limite nos testes de carga comparam um valor de contador de desempenho ou com um valor constante, ou outro valor de contador de desempenho.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-add-a-threshold-rule"></a>Para adicionar uma regra de limite

1. Abra um teste de carga.

2. No Editor de Teste de Carga, expanda o nó **Conjuntos de contadores**.

3. Expanda uma das **Categorias de contadores** em um dos Conjuntos de contadores. Por exemplo, você pode selecionar **LoadTest:Scenario**. Expanda o nó.

4. Clique com o botão direito do mouse em um dos contadores, por exemplo, **Carga de usuários**, em **LoadTest:Scenario**. Selecione **Adicionar regra de limite**.

     A caixa de diálogo **Adicionar regra de limite** é exibida.

5. Você pode escolher entre dois tipos de regra: **Comparar Constante** e **Comparar Contador**. Selecione o tipo apropriado e defina os valores.

    > [!NOTE]
    > Defina a propriedade **Alertar caso seja superado** como **Verdadeiro** para indicar que ultrapassar um limite é um problema ou como **Falso** para indicar que ficar abaixo do limite é um problema.

## <a name="see-also"></a>Consulte também

- [Analisar violações de regra de limite](../test/analyze-threshold-rule-violations-in-load-tests.md)
- [Especificar os conjuntos de contadores e as regras de limite para computadores em um teste de carga](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)
- [Analisar resultados de teste de carga](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
