---
description: Esse método avalia a expressão de forma síncrona.
title: 'IDebugExpression2:: EvaluateSync | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpression2::EvaluateSync
helpviewer_keywords:
- IDebugExpression2::EvaluateSync
ms.assetid: 88964915-dce3-4005-b4f3-9f37415e41e4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 85e0dd1c334ce57b5e466ab66a74db4b29a40adc
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105092430"
---
# <a name="idebugexpression2evaluatesync"></a>IDebugExpression2::EvaluateSync
Esse método avalia a expressão de forma síncrona.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT EvaluateSync(
    EVALFLAGS             dwFlags,
    DWORD                 dwTimeout,
    IDebugEventCallback2* pExprCallback,
    IDebugProperty2**     ppResult
);
```

```csharp
int EvaluateSync(
    enum_EVALFLAGS       dwFlags,
    uint                 dwTimeout,
    IDebugEventCallback2 pExprCallback,
    out IDebugProperty2  ppResult
);
```

## <a name="parameters"></a>Parâmetros
`dwFlags`\
no Uma combinação de sinalizadores da enumeração [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md) que controlam a avaliação da expressão.

`dwTimeout`\
no Tempo máximo, em milissegundos, a aguardar antes de retornar deste método. Use `INFINITE` para aguardar indefinidamente.

`pExprCallback`\
no Esse parâmetro é sempre um valor nulo.

`ppResult`\
fora Retorna o objeto [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) que contém o resultado da avaliação da expressão.

## <a name="return-value"></a>Valor Retornado
Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro. Alguns códigos de erro típicos são:

|Erro|Descrição|
|-----------|-----------------|
|E_EVALUATE_BUSY_WITH_EVALUATION|Outra expressão está sendo avaliada no momento e não há suporte para a avaliação de expressão simultânea.|
|E_EVALUATE_TIMEOUT|A avaliação atingiu o tempo limite.|

## <a name="remarks"></a>Comentários
Para avaliação síncrona, não é necessário enviar um evento de volta ao Visual Studio após a conclusão da avaliação.

## <a name="example"></a>Exemplo
O exemplo a seguir mostra como implementar esse método para um `CExpression` objeto simples que implementa a interface [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md) .

```cpp
HRESULT CExpression::EvaluateSync(EVALFLAGS dwFlags,
                                  DWORD dwTimeout,
                                  IDebugEventCallback2* pExprCallback,
                                  IDebugProperty2** ppResult)
{
    // Set the aborted state to FALSE.
    m_bAborted = FALSE;
    // Delegate the evaluation to EvalExpression.
    return EvalExpression(TRUE, ppResult);
}

HRESULT CExpression::EvalExpression(BOOL bSynchronous,
                                    IDebugProperty2** ppResult)
{
    HRESULT hr;

    // Get the value of an environment variable.
    PCSTR pszVal = m_pEnvBlock->GetEnv(m_pszVarName);
    // Create and initialize a CEnvVar object with the retrieved value.
    // CEnvVar implements the IDebugProperty2 interface.
    CComObject<CEnvVar> *pEnvVar;
    CComObject<CEnvVar>::CreateInstance(&pEnvVar);
    pEnvVar->Init(m_pszVarName, pszVal, m_pDoc);

    if (pszVal) {
        // Check for synchronous evaluation.
        if (bSynchronous) {
            // Set and AddRef the result, IDebugProperty2 interface.
            *ppResult = pEnvVar;
            (*ppResult)->AddRef();
            hr = S_OK;
        } else {
            //For asynchronous evaluation, send an evaluation complete event.
            CExprEvalEvent *pExprEvent = new CExprEvalEvent(this, pEnvVar);
            pExprEvent->SendEvent(m_pExprCallback, NULL, NULL, NULL);
        }
    } else {
        // If a valid value is not retrieved, return E_FAIL.
        hr = E_FAIL;
    }
    return hr;
}
```

## <a name="see-also"></a>Confira também
- [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)
- [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
