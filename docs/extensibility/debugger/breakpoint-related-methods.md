---
title: Métodos de Breakpoint-Related | Microsoft Docs
description: A depuração do Visual Studio dá suporte a pontos de interrupção associados, que são associados com êxito a um local no código e pontos de interrupção pendentes, que ainda não estão associados.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], breakpoint methods
- breakpoints, methods
ms.assetid: a6f77bf0-bf81-443f-8683-5f12075bbe10
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ec218cea05dffc1c558cabdef47895da9ad7ba9c
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901494"
---
# <a name="breakpoint-related-methods"></a>Métodos relacionados ao ponto de interrupção
Um mecanismo de depuração (DE) deve dar suporte à configuração de pontos de interrupção. A depuração do Visual Studio dá suporte aos seguintes tipos de pontos de interrupção:

- Bound

     Solicitado por meio da interface do usuário e associado com êxito a um local de código especificado

- Pendente

     Solicitado por meio da interface do usuário, mas ainda não associado a instruções reais

## <a name="discussion"></a>Discussão
 Por exemplo, um ponto de interrupção pendente ocorre quando as instruções ainda não foram carregadas. Quando o código é carregado, os pontos de interrupção pendentes tentam se associar ao código no local prescrito, ou seja, inserir instruções de quebra no código. Os eventos são enviados para o SDM (Gerenciador de depuração de sessão) para indicar uma associação bem-sucedida ou para notificar que houve erros de associação.

 Um ponto de interrupção pendente também gerencia sua própria lista interna de pontos de interrupção associados correspondentes. Um ponto de interrupção pendente pode causar a inserção de vários pontos de interrupção no código. A interface do usuário de depuração do Visual Studio mostra um modo de exibição de árvore de pontos de interrupção pendentes e seus pontos de interrupção associados correspondentes.

 A criação e o uso de pontos de interrupção pendentes exigem a implementação do método [IDebugEngine2:: CreatePendingBreakpoint](../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md) , bem como os seguintes métodos de interfaces [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) .

|Método|Descrição|
|------------|-----------------|
|[CanBind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)|Determina se um ponto de interrupção pendente especificado pode ser associado a um local de código.|
|[Associa](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)|Associa um ponto de interrupção pendente especificado a um ou mais locais de código.|
|[GetState](../../extensibility/debugger/reference/idebugpendingbreakpoint2-getstate.md)|Obtém o estado de um ponto de interrupção pendente.|
|[GetBreakpointRequest](../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)|Obtém a solicitação de ponto de interrupção usada para criar um ponto de interrupção pendente.|
|[Habilitar](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)|Alterna o estado habilitado de um ponto de interrupção pendente.|
|[EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)|Enumera todos os pontos de interrupção associados a um ponto de interrupção pendente.|
|[EnumErrorBreakpoints](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)|Enumera todos os pontos de interrupção de erro resultantes de um ponto de interrupção pendente.|
|[Excluir](../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md)|Exclui um ponto de interrupção pendente e todos os pontos de interrupção associados a ele.|

 Para enumerar os pontos de interrupção e os pontos de interrupção de erro associados, você deve implementar todos os métodos de [IEnumDebugBoundBreakpoints2](../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md) e de [IEnumDebugErrorBreakpoints2](../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md).

 Os pontos de interrupção pendentes que se associam a um local de código exigem a implementação dos seguintes métodos [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md) .

|Método|Descrição|
|------------|-----------------|
|[GetPendingBreakpoint](../../extensibility/debugger/reference/idebugboundbreakpoint2-getpendingbreakpoint.md)|Obtém o ponto de interrupção pendente que contém um ponto de interrupção.|
|[GetState](../../extensibility/debugger/reference/idebugboundbreakpoint2-getstate.md)|Obtém o estado de um ponto de interrupção associado.|
|[GetBreakpointResolution](../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md)|Obtém a resolução do ponto de interrupção que descreve um ponto de interrupção.|
|[Habilitar](../../extensibility/debugger/reference/idebugboundbreakpoint2-enable.md)|Habilita ou desabilita um ponto de interrupção.|
|[Excluir](../../extensibility/debugger/reference/idebugboundbreakpoint2-delete.md)|Exclui um ponto de interrupção associado.|

 A resolução e as informações de solicitação exigem a implementação dos seguintes métodos [IDebugBreakpointResolution2](../../extensibility/debugger/reference/idebugbreakpointresolution2.md) .

|Método|Descrição|
|------------|-----------------|
|[GetBreakpointType](../../extensibility/debugger/reference/idebugbreakpointresolution2-getbreakpointtype.md)|Obtém o tipo do ponto de interrupção representado por uma resolução.|
|[GetResolutionInfo](../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)|Obtém as informações de resolução do ponto de interrupção que descrevem um ponto de interrupção.|

 A resolução de erros que podem ocorrer durante a associação requer a implementação dos seguintes métodos [IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md) .

|Método|Descrição|
|------------|-----------------|
|[GetPendingBreakpoint](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md)|Obtém o ponto de interrupção pendente que contém um ponto de interrupção de erro.|
|[GetBreakpointResolution](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md)|Obtém a resolução de erro de ponto de interrupção que descreve um ponto de interrupção de erro.|

 A resolução de erros que podem ocorrer durante a ligação também requer os seguintes métodos de [IDebugErrorBreakpointResolution2](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md).

|Método|Descrição|
|------------|-----------------|
|[GetBreakpointType](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getbreakpointtype.md)|Obtém o tipo de um ponto de interrupção.|
|[GetResolutionInfo](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)|Obtém as informações de resolução de um ponto de interrupção.|

 A exibição do código-fonte em um ponto de interrupção exige que você implemente os métodos de [IDebugStackFrame2:: GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md) e/ou os métodos de [IDebugStackFrame2:: GetCodeContext](../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md).

## <a name="see-also"></a>Confira também
- [Controle de execução e avaliação de estado](../../extensibility/debugger/execution-control-and-state-evaluation.md)
