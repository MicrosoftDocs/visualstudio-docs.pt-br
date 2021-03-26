---
title: Gerenciador de depuração de sessão | Microsoft Docs
description: Saiba mais sobre o Gerenciador de depuração de sessão, que gerencia vários programas de depuração de mecanismos de depuração em vários processos em qualquer número de computadores.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- session debug manager, unifying session views
- session debug manager, broadcasting
- debugging [Debugging SDK], session debug manager
- session debug manager
- session debug manager, debug engine multiplexing
- session debug manager, delegating
ms.assetid: fbb1928d-dddc-43d1-98a4-e23b0ecbae09
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2e5a206b8ece21b14758dfeb02563d4d323dcf60
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079456"
---
# <a name="session-debug-manager"></a>Gerenciador de depuração de sessão
O SDM (Gerenciador de depuração de sessão) gerencia qualquer número de mecanismos de depuração (DE) que estejam Depurando qualquer número de programas em vários processos em qualquer número de computadores. Além de ser um multiplexador de mecanismo de depuração, o SDM fornece uma exibição unificada da sessão de depuração para o IDE.

## <a name="session-debug-manager-operation"></a>Operação do Gerenciador de depuração de sessão
 O SDM (Gerenciador de depuração de sessão) gerencia o DE. Pode haver mais de um mecanismo de depuração em execução em um computador ao mesmo tempo. Para multiplexar o DEs, o SDM encapsula várias interfaces do DEs e as expõe para o IDE como uma única interface.

 Para aumentar o desempenho, algumas interfaces não são multiplexada. Em vez disso, eles são usados diretamente de DE e as chamadas para essas interfaces não passam pelo SDM. Por exemplo, as interfaces usadas com memória, código e contextos de documento não são multiplexada, pois se referem a uma instrução, memória ou documento específico em um programa específico depurado por um DE. Nenhum outro DE precisa estar envolvido nesse nível de comunicação.

 Isso não é verdade para todos os contextos. As chamadas para a interface de contexto de avaliação da expressão passam pelo SDM. Durante a avaliação da expressão, o SDM encapsula a interface [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) que ela fornece ao IDE porque, quando essa expressão é avaliada, ela pode envolver vários des que estão Depurando programas no mesmo processo que pode estar em execução no mesmo thread.

 O SDM normalmente atua como um mecanismo de delegação, mas pode atuar como um mecanismo de difusão. Por exemplo, durante a avaliação da expressão, o SDM atua como um mecanismo de difusão para notificar todos os DEs que eles podem executar código em um thread especificado. Da mesma forma, quando o SDM recebe um evento de parada, ele difunde para os programas que eles devem parar de executar. Quando uma etapa é chamada, o SDM transmite para os programas que eles podem continuar em execução. Os pontos DE interrupção também são transmitidos a cada DE.

 O SDM não rastreia o programa atual, o thread ou o registro de ativação. As informações de processo, programa e thread são enviadas para o SDM em conjunto com eventos de depuração específicos.

## <a name="see-also"></a>Confira também
- [Mecanismo de depuração](../../extensibility/debugger/debug-engine.md)
- [Componentes do depurador](../../extensibility/debugger/debugger-components.md)
- [Contextos do depurador](../../extensibility/debugger/debugger-contexts.md)
