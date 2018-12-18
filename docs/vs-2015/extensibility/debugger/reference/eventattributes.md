---
title: EVENTATTRIBUTES | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- EVENTATTRIBUTES
helpviewer_keywords:
- EVENTATTRIBUTES enumeration
ms.assetid: 04db10f7-df31-4464-98e8-b3777428179e
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 17ef2d6813183d230a9d24a6e881352361fb247e
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51730759"
---
# <a name="eventattributes"></a>EVENTATTRIBUTES
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Especifica os atributos do evento.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
enum enum_EVENTATTRIBUTES {   
   EVENT_ASYNCHRONOUS          = 0x0000,  
   EVENT_SYNCHRONOUS           = 0x0001,  
   EVENT_STOPPING              = 0x0002,  
   EVENT_ASYNC_STOP            = 0x0002,  
   EVENT_SYNC_STOP             = 0x0003,  
   EVENT_IMMEDIATE             = 0x0004,  
   EVENT_EXPRESSION_EVALUATION = 0x0008  
};  
typedef DWORD EVENTATTRIBUTES;  
```  
  
```csharp  
public enum enum_EVENTATTRIBUTES {   
   EVENT_ASYNCHRONOUS          = 0x0000,  
   EVENT_SYNCHRONOUS           = 0x0001,  
   EVENT_STOPPING              = 0x0002,  
   EVENT_ASYNC_STOP            = 0x0002,  
   EVENT_SYNC_STOP             = 0x0003,  
   EVENT_IMMEDIATE             = 0x0004,  
   EVENT_EXPRESSION_EVALUATION = 0x0008  
};  
```  
  
## <a name="members"></a>Membros  
 EVENT_ASYNCHRONOUS  
 Indica que o evento é assíncrono e não é necessária nenhuma resposta ao evento.  
  
 EVENT_SYNCHRONOUS  
 Indica que o evento é síncrono; responder por meio da [ContinueFromSynchronousEvent](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md).  
  
 EVENT_STOPPING  
 Indica que se trata de um evento de interrupção. Deve ser combinado com o `EVENT_ASYNCHRONOUS` ou `EVENT_SYNCHRONOUS`.  
  
 EVENT_ASYNC_STOP  
 Indica um evento de interrupção assíncrono. Atualmente, não há nenhum evento do tipo. Este sinalizador é apenas um espaço reservado.  
  
 EVENT_SYNC_STOP  
 Indica um evento de interrupção síncrona (uma combinação de `EVENT_SYNCHRONOUS` e `EVENT_STOPPING`). Esse valor é usado por um mecanismo de depuração (DES) quando ele envia um evento de interrupção. A resposta é feita por meio de uma chamada para [Execute](../../../extensibility/debugger/reference/idebugprogram2-execute.md), [etapa](../../../extensibility/debugger/reference/idebugprogram2-step.md), ou [continuar](../../../extensibility/debugger/reference/idebugprogram2-continue.md).  
  
 EVENT_IMMEDIATE  
 Indica um evento que é enviado imediatamente e de forma síncrona para o IDE. Esse sinalizador é combinado com outros sinalizadores como `EVENT_ASYNCHRONOUS`, `EVENT_SYNCHRONOUS`, ou `EVENT_SYNC_STOP` para indicar o tipo de evento e o fato de que o mecanismo de resposta (se houver) é conhecido.  
  
 EVENT_EXPRESSION_EVALUATION  
 O evento é um resultado da avaliação de expressão.  
  
## <a name="remarks"></a>Comentários  
 Esses valores são passados no `dwAttrib` parâmetro do [evento](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) método.  
  
 Esses valores podem ser combinados com um bit a bit `OR`.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [ContinueFromSynchronousEvent](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)   
 [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)

