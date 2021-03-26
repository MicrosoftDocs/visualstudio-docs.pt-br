---
description: Obtém o motivo pelo qual o ponto de interrupção foi desassociado.
title: 'IDebugBreakpointUnboundEvent2:: GetReason | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointUnboundEvent2::GetReason
helpviewer_keywords:
- IDebugBreakpointUnboundEvent2::GetReason
ms.assetid: 0f8a4fec-d3eb-417d-8516-4f7b51904033
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 814ca3e925a63c53b584f8c4e28d8d224adba46d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088699"
---
# <a name="idebugbreakpointunboundevent2getreason"></a>IDebugBreakpointUnboundEvent2::GetReason
Obtém o motivo pelo qual o ponto de interrupção foi desassociado.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetReason(
    BP_UNBOUND_REASON* pdwUnboundReason
);
```

```csharp
int GetReason(
    out enum_ BP_UNBOUND_REASON pdwUnboundReason
);
```

## <a name="parameters"></a>Parâmetros
`pdwUnboundReason`\
fora Retorna um valor da enumeração [BP_UNBOUND_REASON](../../../extensibility/debugger/reference/bp-unbound-reason.md) especificando o motivo pelo qual o ponto de interrupção foi desassociado.

## <a name="return-value"></a>Valor Retornado
Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
Os motivos incluem um ponto de interrupção sendo reassociado a um local diferente após uma operação de editar e continuar ou uma determinação de que um ponto de interrupção foi associado a um erro.

## <a name="example"></a>Exemplo
O exemplo a seguir mostra como implementar esse método para um objeto **CBreakpointUnboundDebugEventBase** que expõe a interface [IDebugBreakpointUnboundEvent2](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md) .

```cpp
STDMETHODIMP CBreakpointUnboundDebugEventBase::GetReason(
    BP_UNBOUND_REASON* pdwUnboundReason)
{
    HRESULT hRes = E_FAIL;

    if ( EVAL(pdwUnboundReason) )
    {
        *pdwUnboundReason = m_dwReason;

        hRes = S_OK;
    }
    else
        hRes = E_INVALIDARG;

    return ( hRes );
}
```

## <a name="see-also"></a>Confira também
- [IDebugBreakpointUnboundEvent2](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md)
