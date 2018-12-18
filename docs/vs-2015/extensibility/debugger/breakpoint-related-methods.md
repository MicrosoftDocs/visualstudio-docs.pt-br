---
title: Métodos relacionados ao ponto de interrupção | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- debugging [Debugging SDK], breakpoint methods
- breakpoints, methods
ms.assetid: a6f77bf0-bf81-443f-8683-5f12075bbe10
caps.latest.revision: 9
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: e1767afec32b2b90250a841317e0929fcdd7732c
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51794992"
---
# <a name="breakpoint-related-methods"></a>Métodos relacionados ao ponto de interrupção
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Um mecanismo de depuração (DES) deve dar suporte a configuração de pontos de interrupção. Depuração do Visual Studio suporta os seguintes tipos de pontos de interrupção:  
  
-   Associado  
  
     Solicitado por meio da interface do usuário e associar com êxito para um local de código especificada  
  
-   Pendente  
  
     Solicitado por meio da interface do usuário, mas ainda não é vinculado com o real de instruções  
  
## <a name="discussion"></a>Discussão  
 Por exemplo, um ponto de interrupção pendente ocorre quando as instruções ainda não foram carregadas. Quando o código é carregado, pendentes try pontos de interrupção para associar ao código no local prescrito, ou seja, para inserir instruções de interrupção no código. Eventos são enviados para o Gerenciador de sessão de depuração (SDM) para indicar a associação com êxito ou para notificar que não houve erros de ligação.  
  
 Um ponto de interrupção pendente também gerencia sua própria lista interna de pontos de interrupção associadas correspondentes. Uma pendente do ponto de interrupção pode causar a inserção de vários pontos de interrupção no código. Depuração da interface do usuário do Visual Studio mostra uma exibição de árvore dos pontos de interrupção pendentes e suas respectivas associadas a pontos de interrupção.  
  
 Criação e uso de pontos de interrupção pendentes exigem a implementação do [IDebugEngine2::CreatePendingBreakpoint](../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md) método, bem como os seguintes métodos da [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) interfaces.  
  
|Método|Descrição|  
|------------|-----------------|  
|[CanBind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)|Determina se um especificado pendente do ponto de interrupção pode associar a um local de código.|  
|[Associar](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)|Associa um especificado pendente do ponto de interrupção em um ou mais locais de código.|  
|[GetState](../../extensibility/debugger/reference/idebugpendingbreakpoint2-getstate.md)|Obtém o estado de um ponto de interrupção pendente.|  
|[GetBreakpointRequest](../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)|Obtém a solicitação de ponto de interrupção usada para criar um ponto de interrupção pendente.|  
|[Habilitar](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)|Alterna o estado ativado de um ponto de interrupção pendente.|  
|[EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)|Enumera todos os pontos de interrupção associados de um ponto de interrupção pendente.|  
|[EnumErrorBreakpoints](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)|Enumera todos os pontos de interrupção de erro que resultam de um ponto de interrupção pendente.|  
|[Excluir](../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md)|Exclui um ponto de interrupção pendente e todos os pontos de interrupção associados dele.|  
  
 Para enumerar os pontos de interrupção associados e os pontos de interrupção de erro, você deve implementar todos os métodos de [IEnumDebugBoundBreakpoints2](../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md) e da [IEnumDebugErrorBreakpoints2](../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md).  
  
 Pontos de interrupção que se associam a um código pendentes local exigir a implementação dos seguintes [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md) métodos.  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetPendingBreakpoint](../../extensibility/debugger/reference/idebugboundbreakpoint2-getpendingbreakpoint.md)|Obtém o ponto de interrupção pendente que contém um ponto de interrupção.|  
|[GetState](../../extensibility/debugger/reference/idebugboundbreakpoint2-getstate.md)|Obtém o estado de um ponto de interrupção associado.|  
|[GetBreakpointResolution](../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md)|Obtém a resolução de ponto de interrupção que descreve um ponto de interrupção.|  
|[Habilitar](../../extensibility/debugger/reference/idebugboundbreakpoint2-enable.md)|Habilita ou desabilita um ponto de interrupção.|  
|[Excluir](../../extensibility/debugger/reference/idebugboundbreakpoint2-delete.md)|Exclui um ponto de interrupção associado.|  
  
 Resolução e solicitação de informações exigem a implementação dos seguintes [IDebugBreakpointResolution2](../../extensibility/debugger/reference/idebugbreakpointresolution2.md) métodos.  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetBreakpointType](../../extensibility/debugger/reference/idebugbreakpointresolution2-getbreakpointtype.md)|Obtém o tipo do ponto de interrupção representado por uma resolução.|  
|[GetResolutionInfo](../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)|Obtém as informações de resolução de ponto de interrupção que descreve um ponto de interrupção.|  
  
 Resolução de erros que podem ocorrer durante a vinculação requer a implementação dos seguintes [IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md) métodos.  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetPendingBreakpoint](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md)|Obtém o ponto de interrupção pendente que contém um ponto de interrupção de erro.|  
|[GetBreakpointResolution](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md)|Obtém a resolução de erro de ponto de interrupção que descreve um ponto de interrupção de erro.|  
  
 Resolução de erros que podem ocorrer durante a associação também requer os seguintes métodos de [IDebugErrorBreakpointResolution2](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md).  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetBreakpointType](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getbreakpointtype.md)|Obtém o tipo de um ponto de interrupção.|  
|[GetResolutionInfo](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)|Obtém as informações de resolução de um ponto de interrupção.|  
  
 Exibir o código-fonte em um ponto de interrupção exige que você implemente os métodos de [IDebugStackFrame2::GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md) e/ou os métodos da [IDebugStackFrame2::GetCodeContext](../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md).  
  
## <a name="see-also"></a>Consulte também  
 [Controle de execução e avaliação de estado](../../extensibility/debugger/execution-control-and-state-evaluation.md)

