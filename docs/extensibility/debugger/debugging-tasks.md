---
title: Tarefas de depuração | Microsoft Docs
description: Saiba mais sobre as tarefas necessárias para depurar um programa, como anexá-lo a um mecanismo de depuração, gerar eventos de inicialização e atingir pontos de interrupção.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: overview
helpviewer_keywords:
- debugging [Debugging SDK], tasks
ms.assetid: 5d60e9e8-305e-4a48-829f-b9440fc8af7b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 69cc1d40b2a0e61c0cf7ad32cb8187d0dad16994
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094764"
---
# <a name="debug-tasks"></a>Tarefas de depuração
Para depurar um programa, ele deve ser iniciado e um mecanismo DE depuração (DE) deve ser anexado a ele, caso contrário, o DE deve ser anexado a um programa iniciado anteriormente. Uma vez anexado, o DE deve gerar determinados eventos DE inicialização. Em resposta, o pacote de depuração tenta associar os pontos de interrupção definidos no IDE. Quando o programa atinge um ponto de interrupção associado, ele é interrompido e aguarda a entrada do usuário.

## <a name="in-this-section"></a>Nesta seção
 [Problemas de segurança](../../extensibility/debugger/security-issues.md) Discute as etapas de segurança necessárias para depurar um programa.

 [Iniciar um programa](../../extensibility/debugger/launching-a-program.md) Apresenta instruções passo a passo sobre como especificar um DE, que chama o sistema operacional para iniciar o programa.

 [Anexar diretamente a um programa](../../extensibility/debugger/attaching-directly-to-a-program.md) Descreve o processo usado para depurar um programa em um processo que já está em execução.

 [Enviar eventos de inicialização após uma inicialização](../../extensibility/debugger/sending-startup-events-after-a-launch.md) Lista os eventos que ocorrem quando o DE é anexado ao programa, até que o programa esteja em seu ponto de entrada principal e esteja pronto para depuração.

 [Controle de execução](../../extensibility/debugger/control-of-execution.md) Explica como o DE normalmente envia um evento de ponto de entrada, um evento de carregamento completo ou um evento de interrupção, dependendo das circunstâncias.

 [Associar pontos de interrupção](../../extensibility/debugger/binding-breakpoints.md) Descreve como, se o usuário definir um ponto de interrupção, o IDE formula a solicitação e solicita que a sessão de depuração crie o ponto de interrupção.

 [Avaliar expressões](../../extensibility/debugger/evaluating-expressions.md) Explica como as expressões são criadas e o que acontece quando uma expressão é avaliada.

 [Visualizar e exibir dados](../../extensibility/debugger/visualizing-and-viewing-data.md) Explica como visualizeres de tipo e visualizadores personalizados têm suporte do avaliador de expressão (EE).

## <a name="related-sections"></a>Seções relacionadas
 [Conceitos do depurador](../../extensibility/debugger/debugger-concepts.md) Descreve os principais conceitos de arquitetura da depuração.

 [Componentes do depurador](../../extensibility/debugger/debugger-components.md) Fornece uma visão geral dos componentes de depuração do Visual Studio, que incluem os manipuladores DE, EE e símbolo (SH).

 [Contextos do depurador](../../extensibility/debugger/debugger-contexts.md) Explica como o DE Opera simultaneamente em código, documentação e contextos de avaliação de expressão. Descreve, para cada um dos três contextos, o local, a posição ou a avaliação relevante para ele.

## <a name="see-also"></a>Confira também
 [Introdução](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)
