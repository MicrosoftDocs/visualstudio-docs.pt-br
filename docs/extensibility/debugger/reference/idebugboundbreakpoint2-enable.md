---
title: IDebugBoundBreakpoint2:Habilitar | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBoundBreakpoint2::Enable
helpviewer_keywords:
- Enable method
- IDebugBoundBreakpoint2::Enable method
ms.assetid: 1b4e3f73-c94d-4aa3-9aa8-0d8cb8a6c5ca
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ed933b1abf67fbe357462e86d54b23e3b19fa548
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735570"
---
# <a name="idebugboundbreakpoint2enable"></a>IDebugBoundBreakpoint2::Enable
Ativa ou desativa o ponto de ruptura.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Enable(
    BOOL fEnable
);
```

```csharp
int Enable( 
    int fEnable
);
```

## <a name="parameters"></a>parâmetros
`fEnable`\
[em] Defina-se como`TRUE`não-zero (`FALSE`) para habilitar ou zerar ( ) para desativar o ponto de ruptura.

## <a name="return-value"></a>Valor retornado
Se for `S_OK`bem sucedido, retorna; caso contrário, retorna um código de erro. Retorna `E_BP_DELETED` se o estado do objeto de `BPS_DELETED` ponto de ruptura vinculado estiver definido como (parte da [enumeração BP_STATE).](../../../extensibility/debugger/reference/bp-state.md)

## <a name="example"></a>Exemplo
O exemplo a seguir mostra como `CBoundBreakpoint` implementar este método para um objeto simples que expõe a interface [IDebugBoundBreakpoint2.](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)

```
HRESULT CBoundBreakpoint::Enable(BOOL fEnable)
{
    HRESULT hr;

    // Verify that the bound breakpoint has not been deleted. If deleted,
    // then return hr = E_BP_DELETED.
    if (m_state != BPS_DELETED)
    {
        // Check the state of the bound breakpoint. If the breakpoint is
        // supposed to be, but has not already been, enabled, then have the
        // interpreter set the breakpoint.
        if (fEnable && m_state != BPS_ENABLED)
        {
            hr = m_pInterp->SetBreakpoint(m_sbstrDoc, this);
            if (hr == S_OK)
            {
                // Change the state of the breakpoint to BPS_ENABLED.
                m_state = BPS_ENABLED;
            }
        }
        // Check the state of the bound breakpoint. If the breakpoint is
        // supposed to be, but has not already been, disabled, then have the
        // interpreter remove the breakpoint.
        else if (!fEnable && m_state != BPS_DISABLED)
        {
            hr = m_pInterp->RemoveBreakpoint(m_sbstrDoc, this);
            if (hr == S_OK)
            {
                // Change the state of the breakpoint to BPS_DISABLED.
                m_state = BPS_DISABLED;
            }
        }
        else
        {
            hr = S_FALSE;
        }
    }
    else
    {
        hr = E_BP_DELETED;
    }

    return hr;
}
```

## <a name="see-also"></a>Confira também
- [IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)
- [BP_STATE](../../../extensibility/debugger/reference/bp-state.md)
