---
description: Alterna o estado habilitado do ponto de interrupção pendente.
title: 'IDebugPendingBreakpoint2:: habilitar | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2::Enable
helpviewer_keywords:
- IDebugPendingBreakpoint2::Enable method
- Enable method
ms.assetid: 09e32d05-464b-40a6-a41d-76f2759cf2cd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bd3539d7be7930ecc04958c9a005ed873f8282d4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087750"
---
# <a name="idebugpendingbreakpoint2enable"></a>IDebugPendingBreakpoint2::Enable
Alterna o estado habilitado do ponto de interrupção pendente.

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

## <a name="parameters"></a>Parâmetros
`fEnable`\
no Defina como diferente de zero ( `TRUE` ) para habilitar um ponto de interrupção pendente ou para zero ( `FALSE` ) para desabilitar.

## <a name="return-value"></a>Valor Retornado
Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro. Retorna `E_BP_DELETED` se o ponto de interrupção foi excluído.

## <a name="remarks"></a>Comentários
Quando um ponto de interrupção pendente é habilitado ou desabilitado, todos os pontos de interrupção associados a ele são definidos para o mesmo estado.

Esse método pode ser chamado quantas vezes forem necessárias, mesmo que o ponto de interrupção já esteja habilitado ou desabilitado.

## <a name="example"></a>Exemplo
O exemplo a seguir mostra como implementar esse método para um `CPendingBreakpoint` objeto simples que expõe a interface [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) .

```cpp
HRESULT CPendingBreakpoint::Enable(BOOL fEnable)
{
    HRESULT hr;

    // Verify that the pending breakpoint has not been deleted. If deleted,
    // then return hr = E_BP_DELETED.
    if (m_state.state != PBPS_DELETED)
    {
        // If the bound breakpoint member variable is valid, then enable or
        // disable the bound breakpoint.
        if (m_pBoundBP)
        {
            m_pBoundBP->Enable(fEnable);
        }
        // Set the PENDING_BP_STATE in the PENDING_BP_STATE_INFO structure
        // to enabled or disabled depending on the passed BOOL condition.
        m_state.state = fEnable ? PBPS_ENABLED : PBPS_DISABLED;
        hr = S_OK;

    }
    else
    {
        hr = E_BP_DELETED;
    }

    return hr;
}
```

## <a name="see-also"></a>Confira também
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
