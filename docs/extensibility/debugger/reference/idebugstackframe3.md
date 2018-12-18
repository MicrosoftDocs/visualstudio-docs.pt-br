---
title: IDebugStackFrame3 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugStackFrame3
helpviewer_keywords:
- IDebugStackFrame3 interface
ms.assetid: 39af2f57-0a01-42b8-b093-b7fbc61e2909
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 635b53bf63eb83cc868e4bf9b7d5fbb31fe5aa08
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31120616"
---
# <a name="idebugstackframe3"></a>IDebugStackFrame3
Essa interface estende [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) para lidar com exceções interceptadas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugStackFrame3 : IDebugStackFrame2  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 O mecanismo de depuração (DE) implementa essa interface no mesmo objeto que implementa o [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) interface para oferecer suporte a exceções interceptadas.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Chamar [QueryInterface](/cpp/atl/queryinterface) em um `IDebugStackFrame2` interface para obter essa interface.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
 Além dos métodos herdados de [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md), `IDebugStackFrame3` expõe os métodos a seguir.  
  
|Método|Descrição|  
|------------|-----------------|  
|[InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)|Lida com uma exceção para o quadro de pilhas atual antes de qualquer manipulação de exceção regular.|  
|[GetUnwindCodeContext](../../../extensibility/debugger/reference/idebugstackframe3-getunwindcodecontext.md)|Retorna um contexto de código, caso um desenrolamento de pilha.|  
  
## <a name="remarks"></a>Comentários  
 Uma exceção interceptada significa que um depurador pode processar uma exceção antes de quaisquer rotinas de tratamento de exceção normais são chamadas pelo tempo de execução. Interceptar uma exceção essencialmente significa fazer com que o tempo de execução fingir que há um manipulador de exceção presente mesmo quando não há.  
  
 [InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md) é chamado durante a todos os eventos de retorno de chamada de exceção normal (a única exceção a isso é se você estiver depurando código de modo misto (gerenciado e código não gerenciado), caso em que a exceção não pode ser interceptada durante a retorno de última chance). Se o DE não implementar `IDebugStackFrame3`, ou o DE retorna um erro de IDebugStackFrame3::`InterceptCurrentException` (como `E_NOTIMPL`), em seguida, o depurador tratará a exceção normalmente.  
  
 Ao interceptar uma exceção, o depurador pode permitir que o usuário fazer alterações para o estado do programa que está sendo depurado e, em seguida, retomar a execução no ponto em que a exceção foi lançada.  
  
> [!NOTE]
>  Exceções interceptadas são permitidas apenas em código gerenciado, ou seja, em um programa que está executando sob o tempo de execução do CLR (Common Language).  
  
 Um mecanismo de depuração indica que ele oferece suporte a exceções interceptando definindo "metricExceptions" com um valor de 1 em tempo de execução usando o `SetMetric` função. Para obter mais informações, consulte [auxiliares do SDK para depuração](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md).  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de núcleo](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)   
 [Auxiliares do SDK para depuração](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)