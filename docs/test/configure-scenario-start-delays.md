---
title: Configurar atrasos de início de cenário para testes de carga
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- load tests, scenarios, start delays
ms.assetid: 2f634fba-8dfa-4c7a-a8b9-be867b78d16a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0d425b457056e256c5c9ed927c99adf002b78dd9
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85288787"
---
# <a name="configure-scenario-start-delays-in-load-tests"></a>Configurar atrasos de início do cenário em testes de carga

Usando o Editor de Teste de Carga e a janela **Propriedades**, especifique um atraso antes do início de um cenário em um teste de carga.

Por exemplo, talvez você queira usar a propriedade **Atrasar tempo de início** se precisar que um cenário comece a produzir itens consumidos por outro cenário. Você pode atrasar o cenário de consumo para habilitar o cenário de produção a fim de popular alguns dados.

Outro exemplo é que você talvez tenha um cenário executado apenas em uma determinada hora do dia. Assim, você deseja atrasar o início do cenário para simular isso.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="specify-the-delay-start-time-of-a-scenario"></a>Especificar o tempo de início de atraso de um cenário

Você pode especificar um atraso antes do início de um cenário em um teste de carga usando o Editor de Teste de Carga para alterar a propriedade **Tempo de Início do Atraso** na janela **Propriedades**.

> [!NOTE]
> Para obter uma lista completa das propriedades de cenário de teste de carga e suas descrições, confira [Propriedades do cenário de teste de carga](../test/load-test-scenario-properties.md).

Um exemplo de situação em que você talvez queira usar a propriedade **Atrasar tempo de início** é quando precisa que um cenário comece a produzir itens consumidos por outro cenário. Você pode atrasar o cenário de consumo para habilitar o cenário de produção a fim de popular alguns dados.

Outro exemplo é que você talvez tenha um cenário executado apenas em uma determinada hora do dia. Assim, você deseja atrasar o início do cenário para simular isso.

> [!NOTE]
> Para obter uma lista completa das propriedades das configurações de execução e suas descrições, confira [Propriedades do cenário de teste de carga](../test/load-test-scenario-properties.md).

### <a name="to-specify-the-delay-start-time-for-a-scenario"></a>Para especificar Atrasar Tempo de Início de um cenário

1. Abra um teste de carga.

     O Editor de Testes de Carga é exibido. A árvore do teste de carga é exibida.

2. Na pasta **Cenários** das árvores de teste de carga, escolha o nó do cenário para o qual você deseja especificar o atraso de tempo de início.

3. No menu **Exibir**, selecione **Janela de Propriedades**.

     As categorias e as propriedades do cenário são exibidas na janela **Propriedades**.

4. Na caixa de texto da propriedade **Atrasar tempo de início**, digite um valor temporal que indique o tempo de espera após o início do teste de carga, antes do início do cenário quando o teste de carga é executado.

    > [!NOTE]
    > Se o valor da propriedade **Desabilitar durante aquecimento** para o cenário for definido como **Verdadeiro**, o valor temporal das propriedades **Atrasar tempo de início** será aplicado após o período de aquecimento. Você pode controlar quais cenários estão incluídos no aquecimento usando a propriedade do cenário **Desabilitar durante aquecimento**.

5. Depois de alterar a propriedade, escolha **Salvar** no menu **Arquivo**. Assim, você pode executar o teste de carga usando o novo valor de **Atrasar tempo de início**.

## <a name="enable-and-disable-whether-a-scenario-runs-during-the-warm-up-period"></a>Habilitar e desabilitar se um cenário é executado durante o período de aquecimento

A propriedade **Desabilitar durante o aquecimento** é definida usando a janela **Propriedades**. A edição das propriedades do cenário de teste da carga é definida pelo Editor de testes de carga.

A propriedade **Desabilitar durante aquecimento** é usada para indicar se o cenário deve ou não ser executado durante o período de aquecimento especificado na propriedade **Atrasar tempo de início**. Para obter mais informações, examine o procedimento anterior [Especificar o tempo de início do atraso de um cenário](#specify-the-delay-start-time-of-a-scenario).

> [!NOTE]
> Para obter uma lista completa das propriedades das configurações de execução e suas descrições, confira [Propriedades do cenário de teste de carga](../test/load-test-scenario-properties.md).

### <a name="to-enable-or-disable-the-warm-up-period-for-a-scenario"></a>Para habilitar ou desabilitar o período de aquecimento para um cenário

1. Abra um teste de carga.

     O **Editor de Teste de Carga** é exibido. A árvore do teste de carga é exibida.

2. Na pasta **Cenários** das árvores de teste de carga, escolha o nó do cenário para o qual você quer alterar o comportamento de aquecimento.

3. No menu **Exibir**, selecione **Janela de Propriedades**.

     As categorias e as propriedades do cenário são exibidas na janela **Propriedades**.

     Na propriedade **Desabilitar durante aquecimento**, selecione **Verdadeiro** ou **Falso**.

4. Depois de alterar a propriedade, escolha **Salvar** no menu **Arquivo**. Assim, você pode executar o teste de carga usando o novo valor de **Desabilitar durante aquecimento**.

## <a name="see-also"></a>Veja também

- [Editando cenários de teste de carga](../test/edit-load-test-scenarios.md)
- [Configurar agentes de teste e controladores de teste para testes de carga](../test/configure-test-agents-and-controllers-for-load-tests.md)
- [Propriedades do cenário de teste de carga](../test/load-test-scenario-properties.md)
