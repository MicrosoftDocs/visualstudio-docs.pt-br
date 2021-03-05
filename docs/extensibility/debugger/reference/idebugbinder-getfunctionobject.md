---
description: Esse método obtém um objeto IDebugFunctionObject usado para criar parâmetros de função.
title: 'IDebugBinder:: GetFunctionObject | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder::GetFunctionObject
helpviewer_keywords:
- IDebugBinder::GetFunctionObject method
ms.assetid: 8fb789df-8f30-420d-8ca5-bb496a6738f1
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9868edafb18a129d119a818d9e51363d4964afa2
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102143643"
---
# <a name="idebugbindergetfunctionobject"></a>IDebugBinder::GetFunctionObject
Esse método obtém um objeto [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) usado para criar parâmetros de função.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetFunctionObject( 
   IDebugFunctionObject **ppFunction
);
```

```csharp
int GetFunctionObject(
   out IDebugFunctionObject ppFunction
);
```

## <a name="parameters"></a>Parâmetros
`ppFunction`\
fora Retorna a interface [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) que é usada para criar parâmetros de função.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
