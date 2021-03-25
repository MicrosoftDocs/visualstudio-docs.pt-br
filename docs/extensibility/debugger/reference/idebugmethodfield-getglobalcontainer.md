---
description: Obtém o contêiner global do método.
title: 'IDebugMethodField:: GetGlobalContainer | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::GetGlobalContainer
helpviewer_keywords:
- IDebugMethodField::GetGlobalContainer method
ms.assetid: 041ac5aa-0b80-4310-b9ae-b88f8e7e0e5f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e35082faf076bd0242d9dcc34552c31ba159fb08
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058372"
---
# <a name="idebugmethodfieldgetglobalcontainer"></a>IDebugMethodField::GetGlobalContainer
Obtém o contêiner global do método.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetGlobalContainer(
   IDebugClassField** ppClass
);
```

```csharp
int GetGlobalContainer(
   out IDebugClassField ppClass
);
```

## <a name="parameters"></a>Parâmetros
`ppClass`\
fora Retorna um [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) que representa o módulo no qual esse método é definido.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 O objeto [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) retornado representa o módulo inteiro e é um objeto artificial, ou seja, o próprio módulo não tem uma classe real, mas pode ser representado por um `IDebugClassField` objeto, permitindo que os vários elementos do módulo sejam enumerados e descobertos.

## <a name="see-also"></a>Confira também
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
