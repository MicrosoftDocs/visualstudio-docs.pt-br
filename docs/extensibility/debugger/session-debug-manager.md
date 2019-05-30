---
title: Sessão de depuração Manager | Microsoft Docs
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
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6c7dd40796fbf0141cc60bf86204bce462594f8f
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66348571"
---
# <a name="session-debug-manager"></a>Gerenciador de sessão de depuração
O Gerenciador de sessão de depuração (SDM) gerencia a qualquer número de mecanismos de depuração (DES) que está depurando qualquer número de programas em vários processos em qualquer número de máquinas. Além de ser um multiplexador de mecanismo de depuração, o SDM oferece uma exibição unificada da sessão de depuração para o IDE.

## <a name="session-debug-manager-operation"></a>Operação do Gerenciador de depuração de sessão
 O Gerenciador de sessão de depuração (SDM) gerencia a Alemanha. Pode haver mais de um mecanismo de depuração em execução em um computador ao mesmo tempo. Para multiplexar o DEs, o SDM encapsula um número de interfaces do DEs e as expõe para o IDE como uma única interface.

 Para aumentar o desempenho, algumas interfaces não são multiplexadas. Em vez disso, eles são usados diretamente a partir DE, e chamadas para essas interfaces não passam pelo SDM. Por exemplo, interfaces usadas com a memória, o código e contextos de documento não são multiplexadas, pois se referem a uma instrução específica, memória ou documento em um determinado programa depurado por um específico DE. Não há outra Alemanha precisa estar envolvido no nível de comunicação.

 Isso não é verdadeiro para todos os contextos. Chamadas para a interface de contexto de avaliação de expressão percorrem o SDM. Durante a avaliação da expressão, o SDM encapsula o [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) interface que ele oferece ao IDE porque quando essa expressão é avaliada, ela pode envolver vários DEs que está depurando programas no mesmo processo que podem ser em execução no mesmo thread.

 O SDM normalmente funciona como um mecanismo de delegação, mas ele pode atuar como um mecanismo de difusão. Por exemplo, durante a avaliação da expressão, o SDM atua como um mecanismo de difusão para notificar o DEs todos os que eles podem executar código em um thread especificado. Da mesma forma, quando o SDM recebe um evento de interrupção, ele transmite para os programas que devem interromper a execução. Quando uma etapa é chamada, o SDM transmite para os programas que eles podem continuar em execução. Pontos de interrupção também forem transmitidos para cada DE.

 O SDM não controla o programa atual, thread ou quadro de pilha. O processo, programa e informações de thread são enviadas para o SDM em conjunto com eventos de depuração específicos.

## <a name="see-also"></a>Consulte também
- [Mecanismo de depuração](../../extensibility/debugger/debug-engine.md)
- [Componentes do depurador](../../extensibility/debugger/debugger-components.md)
- [Contextos do depurador](../../extensibility/debugger/debugger-contexts.md)