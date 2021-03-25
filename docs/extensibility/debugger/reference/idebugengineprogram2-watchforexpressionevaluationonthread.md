---
description: Permite que a avaliação de expressão (ou não permite) ocorra no thread determinado, mesmo que o programa tenha sido interrompido.
title: IDebugEngineProgram2::WatchForExpressionEvaluationOnThread
titleSuffix: ''
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2::WatchForExpressionEvaluationOnThread
helpviewer_keywords:
- IDebugEngineProgram2::WatchForExpressionEvaluationOnThread
ms.assetid: 01d05e77-8cac-4d1b-b19f-25756767ed27
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 820babb655f04da40fdd44aae55f963539e5ffa8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105093854"
---
# <a name="idebugengineprogram2watchforexpressionevaluationonthread"></a>IDebugEngineProgram2::WatchForExpressionEvaluationOnThread
Permite que a avaliação de expressão (ou não permite) ocorra no thread determinado, mesmo que o programa tenha sido interrompido.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT WatchForExpressionEvaluationOnThread( 
   IDebugProgram2*       pOriginatingProgram,
   DWORD                 dwTid,
   DWORD                 dwEvalFlags,
   IDebugEventCallback2* pExprCallback,
   BOOL                  fWatch
);
```

```csharp
int WatchForExpressionEvaluationOnThread( 
   IDebugProgram2       pOriginatingProgram,
   uint                  dwTid,
   uint                  dwEvalFlags,
   IDebugEventCallback2 pExprCallback,
   int                   fWatch
);
```

## <a name="parameters"></a>Parâmetros
`pOriginatingProgram`\
no Um objeto [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) que representa o programa que está avaliando uma expressão.

`dwTid`\
no Especifica o identificador do thread.

`dwEvalFlags`\
no Uma combinação de sinalizadores da enumeração [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md) que especificam como a avaliação deve ser executada.

`pExprCallback`\
no Um objeto [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) a ser usado para enviar eventos de depuração que ocorrem durante a avaliação da expressão.

`fWatch`\
no Se não for zero ( `TRUE` ), permitirá a avaliação da expressão no thread identificado por `dwTid` ; caso contrário, zero ( `FALSE` ) não permitirá a avaliação da expressão nesse thread.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Quando o SDM (Gerenciador de depuração de sessão) solicita um programa, identificado pelo `pOriginatingProgram` parâmetro, para avaliar uma expressão, ele notifica todos os outros programas anexados chamando esse método.

 A avaliação de expressão em um programa pode fazer com que o código seja executado em outro, devido à avaliação de função ou avaliação de qualquer `IDispatch` propriedade. Por isso, esse método permite que a avaliação de expressão seja executada e concluída mesmo que o thread possa ser interrompido neste programa.

## <a name="see-also"></a>Confira também
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
