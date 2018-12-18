---
title: IDebugExceptionEvent2::PassToDebuggee | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugExceptionEvent2::PassToDebuggee
helpviewer_keywords:
- IDebugExceptionEvent2::PassToDebuggee
ms.assetid: a20d0f0b-2ca0-4437-bd22-9213c81d2738
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 3b1fb575299000e4b9ab894a4700fdf314d17d6c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49832700"
---
# <a name="idebugexceptionevent2passtodebuggee"></a>IDebugExceptionEvent2::PassToDebuggee
Especifica se a exceção deve ser passada para o programa que está sendo depurado quando a execução é retomada, ou se a exceção deve ser descartada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT PassToDebuggee(  
   BOOL fPass  
);  
```  
  
```csharp  
int PassToDebuggee(  
   int fPass  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `fPass`  
 [in] Diferente de zero (`TRUE`) se a exceção deve ser passada para o programa que está sendo depurado quando a execução é retomada, ou zero (`FALSE`) se a exceção deve ser descartada.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Chamar esse método não provoca nenhum código ser executado no programa que está sendo depurado. A chamada é simplesmente definir o estado para a próxima execução do código. Por exemplo, chamadas para o [CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md) método pode retornar `S_OK` com o [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md).`dwState` campo definido como `EXCEPTION_STOP_SECOND_CHANCE`.  
  
 O IDE pode receber o [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md) evento e a chamada a [continuar](../../../extensibility/debugger/reference/idebugprogram2-continue.md) método. O mecanismo de depuração (DES) deve ter um comportamento padrão para manipular o caso se o `PassToDebuggee` método não é chamado.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)   
 [CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)   
 [Continue](../../../extensibility/debugger/reference/idebugprogram2-continue.md)