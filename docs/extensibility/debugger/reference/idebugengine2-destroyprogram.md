---
description: Informa que um mecanismo de depuração (DE) que o programa especificou foi encerrado atypically e que o DE deve limpar todas as referências ao programa e enviar um evento de destruição de programa.
title: IDebugEngine2::D estroyProgram | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::DestroyProgram
helpviewer_keywords:
- IDebugEngine2::DestroyProgram
ms.assetid: 0c9e2698-c70f-4770-a7bb-39650e9c3a1f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7ee646b48a36a2b2c5d707eab6c5a32145d55439
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102162674"
---
# <a name="idebugengine2destroyprogram"></a>IDebugEngine2::DestroyProgram
Informa que um mecanismo de depuração (DE) que o programa especificou foi encerrado atypically e que o DE deve limpar todas as referências ao programa e enviar um evento de destruição de programa.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT DestroyProgram( 
   IDebugProgram2* pProgram
);
```

```cpp
int DestroyProgram( 
   IDebugProgram2 pProgram
);
```

## <a name="parameters"></a>Parâmetros
`pProgram`\
no Um objeto [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) que representa o programa que foi atypically finalizado.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Depois que esse método é chamado, o DE subseqüentemente envia um evento [IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) de volta para o SDM (Gerenciador de depuração de sessão).

 Esse método não é implementado (retorna `E_NOTIMPL` ) se o de for executado no mesmo processo que o programa que está sendo depurado. Esse método é implementado somente se o DE for executado no mesmo processo que o SDM.

## <a name="see-also"></a>Confira também
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
