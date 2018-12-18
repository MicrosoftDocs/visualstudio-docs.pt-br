---
title: Editando teste de carga
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- Load Test Editor
- load tests, Load Test Editor
ms.assetid: ba16ed02-137e-40bf-a4cb-45d87d922d37
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: a2bc06ed17522eef36841b72859554163068afa6
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53048627"
---
# <a name="edit-load-tests"></a>Editar testes de carga

Testes de carga executam testes de desempenho Web ou testes de unidade para simular muitos usuários acessando um servidor ao mesmo tempo. Um teste de carga fornece acesso a dados de estresse e desempenho do aplicativo. Um teste de carga pode ser configurado para emular várias condições de carga, como cargas e tipos de rede.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

Um teste de carga é definido por *cenários*, *conjuntos de contadores* e *configurações de execução*. A ilustração a seguir explica as diferenças entre [cenários](../test/edit-load-test-scenarios.md), [conjuntos de contadores](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md) e [configurações de execução](../test/load-test-run-settings-properties.md):

![Arquitetura de teste de carga](../test/media/load_test_editor.png)

## <a name="software-requirements"></a>Requisitos de software

Projetos de teste de carga e de desempenho Web só estão disponíveis na edição Enterprise do Visual Studio.

## <a name="edit-load-test-scenario-settings"></a>Editar configurações de cenário de teste de carga

Um cenário é usado para modelar como um grupo de usuários interage com um aplicativo para servidores. Um cenário consiste em um padrão de carga, um modelo de combinação de testes, uma combinação de navegadores e de redes. Um teste de carga pode ter mais de um cenário, e um único cenário podem conter testes de desempenho na Web e testes de unidade. Agrupando configurações semelhantes, um cenário permite agrupar e executar testes de uma natureza semelhante.

Para saber mais, confira [Editar cenários de teste de carga](../test/edit-load-test-scenarios.md) e [Propriedades de cenário de teste de carga](../test/load-test-scenario-properties.md).

## <a name="configure-and-manage-performance-counter-sets"></a>Configurar e gerenciar conjuntos de contadores de desempenho

Os testes de carga oferecem conjuntos de contadores nomeados, organizados por tecnologia, úteis para quando você analisar dados de contadores de desempenho. Os conjuntos de contadores incluem Teste de Carga, IIS, ASP.NET e SQL. Quando você cria um teste de carga com o **Novo Assistente de Teste de Carga**, um conjunto inicial de contadores predefinidos importantes é configurado para os computadores que você especifica para incluir no teste de carga. Você gerencia os contadores no **Editor de Teste de Carga**.

Para saber mais, confira [Especificar os conjuntos de contadores e as regras de limite para computadores em um teste de carga](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md).

## <a name="configure-and-manage-load-test-run-settings"></a>Definir e gerenciar configurações de execução de teste de carga

Configurações de execução são propriedades que influenciam a maneira como um teste de carga é executado. As configurações de execução são organizadas por categorias na janela **Propriedades**.

Para saber mais, confira [Definir configurações de execução de teste de carga](../test/configure-load-test-run-settings.md) e [Propriedades de configurações de execução de teste de carga](../test/load-test-run-settings-properties.md).

## <a name="see-also"></a>Consulte também

- [Analisar resultados do teste de carga](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
- [Analisar violações de regra de limite](../test/analyze-threshold-rule-violations-in-load-tests.md)