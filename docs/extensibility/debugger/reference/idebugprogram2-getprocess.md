---
description: Obtenha o processo em que este programa está sendo executado.
title: 'IDebugProgram2:: GetProcess | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetProcess
helpviewer_keywords:
- IDebugProgram2::GetProcess
ms.assetid: 1d602485-ebaf-451c-9165-f2e226f20a90
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1d87d863b954a9865ff3960f2f2cdd45ac40ce58
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065392"
---
# <a name="idebugprogram2getprocess"></a>IDebugProgram2::GetProcess
Obtenha o processo em que este programa está sendo executado.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetProcess(
   IDebugProcess2** ppProcess
);
```

```csharp
int GetProcess(
   out IDebugProcess2 ppProcess
);
```

## <a name="parameters"></a>Parâmetros
`ppProcess`\
fora Retorna a interface [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) que representa o processo.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 A menos que um mecanismo DE depuração (DE) implemente a interface [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md) , a implementação de de desse método sempre deve retornar `E_NOTIMPL` porque um de não pode determinar qual processo está sendo executado e, portanto, não pode atender a uma implementação desse método.

 Implementar a `IDebugEngineLaunch2` interface significa que o de deve saber como criar um processo; portanto, a implementação de de da interface [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) é capaz de saber em qual processo ele está sendo executado.

## <a name="see-also"></a>Confira também
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
