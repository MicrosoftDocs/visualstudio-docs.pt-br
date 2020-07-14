---
title: Pontos de interrupção de associação | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- breakpoints, binding
ms.assetid: 70737387-c52f-4dae-8865-77d4b203bf25
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e839b6e0e7967c4802bee5617da3334c5d4033c5
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903233"
---
# <a name="bind-breakpoints"></a>Associar pontos de interrupção
Se o usuário definir um ponto de interrupção, talvez pressionando **F9**, o IDE formula a solicitação e solicita que a sessão de depuração crie o ponto de interrupção.

## <a name="set-a-breakpoint"></a>Definir um ponto de interrupção
 Definir um ponto de interrupção é um processo de duas etapas, pois o código ou os dados afetados pelo ponto de interrupção podem ainda não estar disponíveis. Primeiro, o ponto de interrupção deve ser descrito e, em seguida, à medida que o código ou os dados ficam disponíveis, ele deve ser associado a esse código ou dados, da seguinte maneira:

1. O ponto de interrupção é solicitado dos mecanismos de depuração relevantes (DEs) e, em seguida, o ponto de interrupção é vinculado ao código ou aos dados conforme eles ficam disponíveis.

2. A solicitação de ponto de interrupção é enviada para a sessão de depuração, que a envia para todos os DEs relevantes. Qualquer DE que escolha tratar o ponto de interrupção cria um ponto de interrupção pendente correspondente.

3. A sessão de depuração coleta os pontos de interrupção pendentes e os envia de volta para o pacote de depuração (o componente de depuração do Visual Studio).

4. O pacote de depuração solicita que a sessão de depuração vincule o ponto de interrupção pendente a código ou dados. A sessão de depuração envia essa solicitação a todos os DEs relevantes.

5. Se o DE for capaz de associar o ponto de interrupção, ele enviará um evento vinculado de ponto de interrupção de volta para a sessão de depuração. Caso contrário, ele enviará um evento de erro de ponto de interrupção.

## <a name="pending-breakpoints"></a>Pontos de interrupção pendentes
 Um ponto de interrupção pendente pode ser associado a vários locais de código. Por exemplo, uma linha de código-fonte para um modelo C++ pode ser associada a cada sequência de código gerada a partir do modelo. A sessão de depuração pode usar um evento de limite de ponto de interrupção para enumerar os contextos de código associados a um ponto de interrupção no momento em que o evento foi enviado. Mais contextos DE código podem ser associados mais tarde, portanto, o DE pode enviar vários eventos vinculados de ponto de interrupção para cada solicitação de associação. No entanto, um DE deve enviar apenas um evento DE erro DE ponto de interrupção por solicitação DE associação.

## <a name="implementation"></a>Implementação
 Programaticamente, o pacote de depuração chama o SDM (Gerenciador de depuração de sessão) e fornece a ele uma interface [IDebugBreakpointRequest2](../../extensibility/debugger/reference/idebugbreakpointrequest2.md) que encapsula uma estrutura de [BP_REQUEST_INFO](../../extensibility/debugger/reference/bp-request-info.md) , que descreve o ponto de interrupção a ser definido. Embora os pontos de interrupção possam ser de várias formas, eles finalmente resolvem para um contexto de código ou de dados.

 O SDM passa essa chamada para cada relevante DE chamando seu método [CreatePendingBreakpoint](../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md) . Se o DE escolher para manipular o ponto de interrupção, ele cria e retorna uma interface [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) . O SDM coleta essas interfaces e as passa de volta para o pacote de depuração como uma única `IDebugPendingBreakpoint2` interface.

 Até agora, nenhum evento foi gerado.

 O pacote de depuração tenta associar o ponto de interrupção pendente a código ou dados chamando [BIND](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md), que é implementado pelo de.

 Se o ponto de interrupção estiver associado, o DE enviará uma interface de evento [IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md) para o pacote de depuração. O pacote de depuração usa essa interface para enumerar todos os contextos de código (ou o contexto de dados único) vinculado ao ponto de interrupção chamando [EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md), que retorna uma ou mais interfaces [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md) . A interface [GetBreakpointResolution](../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md) retorna uma interface [IDebugBreakpointResolution2](../../extensibility/debugger/reference/idebugbreakpointresolution2.md) e [GetResolutionInfo](../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md) retorna um [BP_RESOLUTION_INFO](../../extensibility/debugger/reference/bp-resolution-info.md) Union que contém o contexto do código ou dos dados.

 Se o DE não puder associar o ponto de interrupção, ele enviará uma única interface de evento [IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md) para o pacote de depuração. O pacote de depuração recupera o tipo de erro (erro ou aviso) e a mensagem informativa chamando [GetErrorBreakpoint](../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md), seguido por [GetBreakpointResolution](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md) e [GetResolutionInfo](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md). Isso retorna uma estrutura de [BP_ERROR_RESOLUTION_INFO](../../extensibility/debugger/reference/bp-error-resolution-info.md) que contém o tipo de erro e a mensagem.

 Se um DE manipula um ponto de interrupção, mas não pode associá-lo, ele retorna um erro do tipo `BPET_TYPE_ERROR` . O pacote de depuração responde exibindo uma caixa de diálogo de erro, e o IDE coloca um glifo de exclamação dentro do glifo do ponto de interrupção à esquerda da linha do código-fonte.

 Se um dos manipular um ponto de interrupção, o não pode associá-lo, mas alguns outros podem associá-lo, ele retorna um aviso. O IDE responde colocando um glifo de pergunta dentro do glifo do ponto de interrupção à esquerda da linha do código-fonte.

## <a name="see-also"></a>Confira também
- [Tarefas de depuração](../../extensibility/debugger/debugging-tasks.md)
