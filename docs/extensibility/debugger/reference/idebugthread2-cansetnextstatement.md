---
description: Determina se o ponteiro de instrução atual pode ser definido para o determinado registro de ativação.
title: 'IDebugThread2:: CanSetNextStatement | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::CanSetNextStatement
helpviewer_keywords:
- IDebugThread2::CanSetNextStatement
ms.assetid: 7014af80-ff4f-4790-a34b-0528918d1fa3
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4b07eb23127abedc4e41af2795c3452401c3e670
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102168381"
---
# <a name="idebugthread2cansetnextstatement"></a>IDebugThread2::CanSetNextStatement
Determina se o ponteiro de instrução atual pode ser definido para o determinado registro de ativação.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT CanSetNextStatement ( 
   IDebugStackFrame2*  pStackFrame,
   IDebugCodeContext2* pCodeContext
);
```

```csharp
int CanSetNextStatement ( 
   IDebugStackFrame2  pStackFrame,
   IDebugCodeContext2 pCodeContext
);
```

## <a name="parameters"></a>Parâmetros
`pStackFrame`\
Reservado para uso futuro; Defina como um valor nulo. Se esse for um valor nulo, use o registro de ativação atual.

`pCodeContext`\
no Um objeto [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) que descreve o local do código a ser executado e seu contexto.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Se esse método retornar `S_OK` , chame o método [SetNextStatement](../../../extensibility/debugger/reference/idebugthread2-setnextstatement.md) para realmente definir a próxima instrução.

## <a name="see-also"></a>Confira também
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [SetNextStatement](../../../extensibility/debugger/reference/idebugthread2-setnextstatement.md)
