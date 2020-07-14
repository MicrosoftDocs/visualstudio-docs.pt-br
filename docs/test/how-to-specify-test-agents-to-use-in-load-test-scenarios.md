---
title: Especificar os agentes de teste a serem usados em cenários de teste de carga
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- test agents, load tests
- load tests, scenarios
- load tests, specifying for load tests
- tests agents, load tests, specifying
- load tests, test agents
ms.assetid: e86806dd-5897-4e4c-bfd4-8d687fb72a6e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5d9e22200a63544b4539f7bf78c48d5711974776
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85287487"
---
# <a name="how-to-specify-test-agents-to-use-in-load-test-scenarios"></a>Como especificar agentes de teste a serem usados em cenários de teste de carga

Depois de criar o teste de carga usando o **novo assistente de teste de carga**, você pode usar o **Editor de teste de carga** para alterar as propriedades de cenários para atender às suas necessidades e metas de teste.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

> [!NOTE]
> Para obter uma lista completa das propriedades de cenário de teste de carga e suas descrições, confira [Propriedades do cenário de teste de carga](../test/load-test-scenario-properties.md).

Os agentes são especificados usando o **Editor de teste de carga** para alterar os **agentes para usar** a propriedade na janela **Propriedades** .

Você pode especificar os agentes que deseja que seu cenário use se estiver usando controladores e agentes para executar o teste de carga remotamente. Por exemplo, talvez seja conveniente especificar um determinado conjunto de agentes para que você possa manter consistência ao analisar tendências de desempenho. Além disso, os agentes podem ser distribuídos geograficamente para que haja uma afinidade entre quais scripts eles executam e onde o agente está localizado.

> [!TIP]
> Em vez de colocar fisicamente um agente no site remoto, outra opção é usar a emulação de rede para emular a rede lenta. Para obter mais informações, confira [Especificar tipos de rede virtual](../test/specify-virtual-network-types-in-a-load-test-scenario.md).

Para obter mais informações, consulte [Controladores e agentes de teste](configure-test-agents-and-controllers-for-load-tests.md).

Outro motivo é que alguns, mas não todos, agentes podem ter software instalado neles que é necessário para determinado cenário.

Você pode controlar a seleção do agente para uma determinada execução de teste usando funções nas configurações de teste. Para obter mais informações, consulte [coletar informações de diagnóstico usando configurações de teste](../test/collect-diagnostic-information-using-test-settings.md).

Se um computador de agente de teste tiver mais de 75% de utilização de CPU ou menos de 10% de memória física disponível, adicione mais agentes ao seu teste de carga para garantir que o computador do agente não se torne o gargalo em seu teste de carga.

## <a name="to-specify-the-agents-to-use-for-a-scenario"></a>Para especificar os agentes a usar em um cenário

1. Abra um teste de carga.

     O **Editor de Teste de Carga** é exibido. A árvore do teste de carga é exibida.

2. Na pasta **Cenários** das árvores de teste de carga, escolha o nó do cenário para o qual você deseja especificar os agentes a serem usados.

3. No menu **Exibir**, selecione **Janela de Propriedades**.

     As categorias e as propriedades do cenário são exibidas na janela **Propriedades**.

4. Na caixa de texto da propriedade **Agentes a usar**, digite a lista de agentes em que o cenário pode ser executado.

     Os agentes devem ser separados por vírgulas, por exemplo, "**Agent1, Agent2, Agent3**". Deixar a propriedade em branco especifica que esse cenário deve usar todos os agentes disponíveis.

    > [!NOTE]
    > A propriedade **Agentes a usar** é ignorada para execuções locais. Para execuções remotas, se nenhum dos agentes especificados em **Agentes a usar** existir, os testes no cenário não serão executados.

5. Depois de alterar a propriedade, escolha **Salvar** no menu **Arquivo**. Em seguida, você pode executar o teste de carga usando o novo valor de **Agentes a usar**.

## <a name="see-also"></a>Veja também

- [Editar cenários de teste de carga](../test/edit-load-test-scenarios.md)
- [Passo a passo: Criar e executar um teste de carga](../test/walkthrough-create-and-run-a-load-test.md)
- [Controladores de teste e agentes de teste](configure-test-agents-and-controllers-for-load-tests.md)
- [Propriedades do cenário de teste de carga](../test/load-test-scenario-properties.md)
