---
title: Gerenciador de Depuração de Sessão | Microsoft Docs
description: Saiba mais sobre o gerenciador de depuração de sessão, que gerencia vários mecanismos de depuração de programas em vários processos em qualquer número de máquinas.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
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
ms.openlocfilehash: 217a2d401e61c58a58d958bb754265a19a2a367d
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902079"
---
# <a name="session-debug-manager"></a>Gerenciador de depuração de sessão
O SDM (gerenciador de depuração de sessão) gerencia qualquer número de DE (mecanismos de depuração) que estão depurando qualquer número de programas em vários processos em qualquer número de máquinas. Além de ser um multiplexador do mecanismo de depuração, o SDM fornece uma exibição unificada da sessão de depuração para o IDE.

## <a name="session-debug-manager-operation"></a>Operação do gerenciador de depuração de sessão
 O SDM (gerenciador de depuração de sessão) gerencia o DE. Pode haver mais de um mecanismo de depuração em execução em um computador ao mesmo tempo. Para multiplexar os DEs, o SDM envolve várias interfaces dos DEs e as expõe ao IDE como uma única interface.

 Para aumentar o desempenho, algumas interfaces não são multiplexadas. Em vez disso, eles são usados diretamente do DE e as chamadas para essas interfaces não passam pelo SDM. Por exemplo, as interfaces usadas com contextos de memória, código e documento não são multiplexadas, pois se referem a uma instrução, memória ou documento específico em um programa específico depurado por uma DE específica. Nenhuma outra DE precisa estar envolvida nesse nível de comunicação.

 Isso não é verdadeiro para todos os contextos. Chamadas para a interface de contexto de avaliação de expressão passam pelo SDM. Durante a avaliação da expressão, o SDM envolve a interface [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) que ele fornece ao IDE porque, quando essa expressão é avaliada, pode envolver vários DEs que estão depurando programas no mesmo processo que pode estar em execução no mesmo thread.

 O SDM normalmente atua como um mecanismo de delegação, mas pode atuar como um mecanismo de difusão. Por exemplo, durante a avaliação da expressão, o SDM atua como um mecanismo de difusão para notificar todos os DEs de que eles podem executar código em um thread especificado. Da mesma forma, quando o SDM recebe um evento de interrupção, ele transmite para os programas que eles devem parar de executar. Quando uma etapa é chamada, o SDM transmite para os programas que eles podem continuar em execução. Os pontos de interrupção também são transmitidos para cada DE.

 O SDM não acompanha o programa atual, thread ou quadro de pilha. As informações de processo, programa e thread são enviadas ao SDM em conjunto com eventos de depuração específicos.

## <a name="see-also"></a>Confira também
- [Mecanismo de depuração](../../extensibility/debugger/debug-engine.md)
- [Componentes do depurador](../../extensibility/debugger/debugger-components.md)
- [Contextos do depurador](../../extensibility/debugger/debugger-contexts.md)
