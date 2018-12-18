---
title: IDebugCanStopEvent2::GetReason | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugCanStopEvent2::GetReason
helpviewer_keywords:
- IDebugCanStopEvent2::GetReason
ms.assetid: f5de31ca-7b8d-4029-9cf9-ba860ac66af6
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: d32f8be53d88b8268fdbbc82e6d774bffe3d7c3a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49898404"
---
# <a name="idebugcanstopevent2getreason"></a>IDebugCanStopEvent2::GetReason
Obtém o motivo por que deseja interromper o mecanismo de depuração (DES).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetReason(   
   CANSTOP_REASON* pcr  
);  
```  
  
```csharp  
int GetReason(   
   out enum_CANSTOP_REASON pcr  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pcr`  
 [out] Retorna um valor da [CANSTOP_REASON](../../../extensibility/debugger/reference/canstop-reason.md) enumeração que descreve o motivo para esse evento.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Normalmente, esse método é chamado antes do [CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md) método para que o chamador possa determinar se deve passar diferente de zero (`TRUE`) para o `IDebugCanStopEvent2::CanStop` método.  
  
 O motivo para interrupção pode ser `CANSTOP_ENTRYPOINT`, que significa que o DE atingiu um ponto de entrada, ou `CANSTOP_STEPIN`, que significa que o DE tiver entrado em uma função.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)   
 [CANSTOP_REASON](../../../extensibility/debugger/reference/canstop-reason.md)   
 [CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md)