---
title: Especificar os agentes de teste a serem usados em cenários de teste de carga no Visual Studio
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- test agents, load tests
- load tests, scenarios
- load tests, specifying for load tests
- tests agents, load tests, specifying
- load tests, test agents
ms.assetid: e86806dd-5897-4e4c-bfd4-8d687fb72a6e
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 1d153e3ab237e87764b8805c91f4e4c4e5512c60
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895178"
---
# <a name="how-to-specify-test-agents-to-use-in-load-test-scenarios"></a>Como especificar agentes de teste a serem usados em cenários de teste de carga

Depois de criar seu teste de carga usando o **Novo Assistente de Teste de Carga**, você poderá usar o **Editor de Teste de Carga** para alterar as propriedades de cenários para que eles atendam às suas metas e necessidades de teste.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

> [!NOTE]
> Para obter uma lista completa das propriedades de cenário de teste de carga e suas descrições, confira [Propriedades do cenário de teste de carga](../test/load-test-scenario-properties.md).

Os agentes são especificados usando o **Editor de Teste de Carga** para alterar a propriedade **Agentes a usar** na janela **Propriedades**.

Você pode especificar os agentes que deseja que seu cenário use se estiver usando controladores e agentes para executar o teste de carga remotamente. Por exemplo, talvez seja conveniente especificar um determinado conjunto de agentes para que você possa manter consistência ao analisar tendências de desempenho. Além disso, os agentes podem ser distribuídos geograficamente para que haja uma afinidade entre quais scripts eles executam e onde o agente está localizado.

> [!TIP]
> Em vez de colocar fisicamente um agente no site remoto, outra opção é usar a emulação de rede para emular a rede lenta. Para obter mais informações, confira [Especificar tipos de rede virtual](../test/specify-virtual-network-types-in-a-load-test-scenario.md).

Para obter mais informações, consulte [Controladores e agentes de teste](configure-test-agents-and-controllers-for-load-tests.md).

Outro motivo é que alguns, mas não todos, agentes podem ter software instalado neles que é necessário para determinado cenário.

Você pode controlar a seleção do agente para uma determinada execução de teste usando funções nas configurações de teste. Para obter mais informações, confira [Coletar informações de diagnóstico usando configurações de teste](../test/collect-diagnostic-information-using-test-settings.md).

Se um computador de agente de teste tiver mais de 75% de utilização de CPU ou menos de 10% de memória física disponível, adicione mais agentes ao seu teste de carga para garantir que o computador do agente não se torne o gargalo em seu teste de carga.

## <a name="to-specify-the-agents-to-use-for-a-scenario"></a>Para especificar os agentes a usar em um cenário

1.  Abra um teste de carga.

     O **Editor de Teste de Carga** é exibido. A árvore do teste de carga é exibida.

2.  Na pasta **Cenários** das árvores de teste de carga, escolha o nó do cenário para o qual você deseja especificar os agentes a serem usados.

3.  No menu **Exibir**, selecione **Janela de Propriedades**.

     As categorias e as propriedades do cenário são exibidas na janela **Propriedades**.

4.  Na caixa de texto da propriedade **Agentes a usar**, digite a lista de agentes em que o cenário pode ser executado.

     Os agentes devem ser separados por vírgulas, por exemplo, "**Agent1, Agent2, Agent3**". Deixar a propriedade em branco especifica que esse cenário deve usar todos os agentes disponíveis.

    > [!NOTE]
    > A propriedade **Agentes a usar** é ignorada para execuções locais. Para execuções remotas, se nenhum dos agentes especificados em **Agentes a usar** existir, os testes no cenário não serão executados.

5.  Depois de alterar a propriedade, escolha **Salvar** no menu **Arquivo**. Em seguida, você pode executar o teste de carga usando o novo valor de **Agentes a usar**.

## <a name="see-also"></a>Consulte também

- [Editar cenários de teste de carga](../test/edit-load-test-scenarios.md)
- [Passo a passo: criar e executar um teste de carga](../test/walkthrough-create-and-run-a-load-test.md)
- [Controladores e agentes de teste](configure-test-agents-and-controllers-for-load-tests.md)
- [Propriedades do cenário de teste de carga](../test/load-test-scenario-properties.md)