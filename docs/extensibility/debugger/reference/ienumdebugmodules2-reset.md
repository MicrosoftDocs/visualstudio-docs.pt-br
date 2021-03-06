---
description: Redefine a enumeração de módulos para o primeiro elemento.
title: 'IEnumDebugModules2:: Reset | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugModules2::Reset
helpviewer_keywords:
- IEnumDebugModules2::Reset
ms.assetid: f6ff364c-2644-4919-b950-3cb82eb6f601
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a395a31b029b0d6a63eda670b10cbe8d4132b5b2
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102224714"
---
# <a name="ienumdebugmodules2reset"></a>IEnumDebugModules2::Reset
Redefine a enumeração para o primeiro elemento.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Reset(
   void
);
```

```csharp
int Reset();
```

## <a name="return-value"></a>Valor retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Depois que esse método é chamado, a próxima chamada para o [próximo](../../../extensibility/debugger/reference/ienumdebugmodules2-next.md) método retorna o primeiro elemento da enumeração.

## <a name="see-also"></a>Confira também
- [IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)
