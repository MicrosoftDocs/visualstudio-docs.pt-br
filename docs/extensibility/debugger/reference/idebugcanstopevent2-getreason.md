---
title: 'IDebugCanStopEvent2:: GetReason | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2::GetReason
helpviewer_keywords:
- IDebugCanStopEvent2::GetReason
ms.assetid: f5de31ca-7b8d-4029-9cf9-ba860ac66af6
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2aadf18dbf45f8b10791c69ed4f189c38491636d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99890286"
---
# <a name="idebugcanstopevent2getreason"></a>IDebugCanStopEvent2::GetReason
Obtém o motivo pelo qual o mecanismo de depuração (DE) deseja parar.

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

## <a name="parameters"></a>Parâmetros
`pcr`\
fora Retorna um valor da enumeração [CANSTOP_REASON](../../../extensibility/debugger/reference/canstop-reason.md) que descreve o motivo para esse evento.

## <a name="return-value"></a>Valor de retorno
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Esse método é normalmente chamado antes do método [CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md) , para que o chamador possa determinar se deve passar um valor diferente de zero ( `TRUE` ) para o `IDebugCanStopEvent2::CanStop` método.

 O motivo da interrupção pode ser `CANSTOP_ENTRYPOINT` , ou seja, o de atingiu um ponto de entrada ou `CANSTOP_STEPIN` , o que significa que o de foi dividido em uma função.

## <a name="see-also"></a>Confira também
- [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)
- [CANSTOP_REASON](../../../extensibility/debugger/reference/canstop-reason.md)
- [CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md)
