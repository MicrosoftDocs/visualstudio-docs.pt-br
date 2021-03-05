---
description: Cria um ponto de interrupção pendente no mecanismo de depuração (DE).
title: 'IDebugEngine2:: CreatePendingBreakpoint | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::CreatePendingBreakpoint
helpviewer_keywords:
- IDebugEngine2::CreatePendingBreakpoint
ms.assetid: 92e85b90-a931-48d9-89a7-a6edcb83ae5a
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c364778fa857049139c058f144651edc28bb4692
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102160155"
---
# <a name="idebugengine2creatependingbreakpoint"></a>IDebugEngine2::CreatePendingBreakpoint
Cria um ponto de interrupção pendente no mecanismo de depuração (DE).

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT CreatePendingBreakpoint(
    IDebugBreakpointRequest2*  pBPRequest,
    IDebugPendingBreakpoint2** ppPendingBP
);
```

```csharp
int CreatePendingBreakpoint(
    IDebugBreakpointRequest2     pBPRequest,
    out IDebugPendingBreakpoint2 ppPendingBP
);
```

## <a name="parameters"></a>Parâmetros
`pBPRequest`\
no Um objeto [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md) que descreve o ponto de interrupção pendente a ser criado.

`ppPendingBP`\
fora Retorna um objeto [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) que representa o ponto de interrupção pendente.

## <a name="return-value"></a>Valor Retornado
Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro. Normalmente retorna `E_FAIL` se o `pBPRequest` parâmetro não corresponde a nenhum idioma suportado pelo de se o `pBPRequest` parâmetro for inválido ou incompleto.

## <a name="remarks"></a>Comentários
Um ponto de interrupção pendente é essencialmente uma coleção de todas as informações necessárias para associar um ponto de interrupção ao código. O ponto de interrupção pendente retornado desse método não está associado ao código até que o método [BIND](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md) seja chamado.

Para cada ponto de interrupção pendente que o usuário define, o SDM (Gerenciador de depuração de sessão) chama esse método em cada um dos anexados. Cabe ao DE um verificar se o ponto de interrupção é válido para programas em execução naquele DE.

Quando o usuário define um ponto de interrupção em uma linha de código, o DE é livre para associar o ponto de interrupção à linha mais próxima do documento que corresponde a esse código. Isso possibilita ao usuário definir um ponto de interrupção na primeira linha de uma instrução de várias linhas, mas associá-la à última linha (onde todo o código é atribuído nas informações de depuração).

## <a name="example"></a>Exemplo
O exemplo a seguir mostra como implementar esse método para um `CProgram` objeto simples. Em seguida, a implementação de de de `IDebugEngine2::CreatePendingBreakpoint` pode encaminhar todas as chamadas para essa implementação do método em cada programa.

```
HRESULT CProgram::CreatePendingBreakpoint(IDebugBreakpointRequest2* pBPRequest, IDebugPendingBreakpoint2** ppPendingBP)
{
    // Create and initialize the CPendingBreakpoint object.
    CComObject<CPendingBreakpoint> *pPending;
    CComObject<CPendingBreakpoint>::CreateInstance(&pPending);
    pPending->Initialize(pBPRequest, m_pInterp, m_pCallback, m_pEngine);
    return pPending->QueryInterface(ppPendingBP);
}
```

## <a name="see-also"></a>Confira também
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [Associa](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)
- [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
