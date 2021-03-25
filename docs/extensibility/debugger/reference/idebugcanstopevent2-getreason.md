---
description: Obtém o motivo pelo qual o mecanismo de depuração (DE) deseja parar.
title: 'IDebugCanStopEvent2:: GetReason | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2::GetReason
helpviewer_keywords:
- IDebugCanStopEvent2::GetReason
ms.assetid: f5de31ca-7b8d-4029-9cf9-ba860ac66af6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2125bb90693d5a4c5cc23ac1225d56dea636de2e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085046"
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

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Esse método é normalmente chamado antes do método [CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md) , para que o chamador possa determinar se deve passar um valor diferente de zero ( `TRUE` ) para o `IDebugCanStopEvent2::CanStop` método.

 O motivo da interrupção pode ser `CANSTOP_ENTRYPOINT` , ou seja, o de atingiu um ponto de entrada ou `CANSTOP_STEPIN` , o que significa que o de foi dividido em uma função.

## <a name="see-also"></a>Confira também
- [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)
- [CANSTOP_REASON](../../../extensibility/debugger/reference/canstop-reason.md)
- [CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md)
