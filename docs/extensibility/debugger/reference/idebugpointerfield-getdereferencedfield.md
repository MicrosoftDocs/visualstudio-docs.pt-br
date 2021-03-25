---
description: Esse método retorna o tipo de objeto para o qual esse objeto ponteiro aponta.
title: 'IDebugPointerField:: GetDereferencedField | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerField::GetDereferencedField
helpviewer_keywords:
- IDebugPointerField::GetDereferencedField method
ms.assetid: 8de988ab-cd79-4287-be72-3c900f2fe407
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e54b378475cec191ca8395a7af5652ea6e93125f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053666"
---
# <a name="idebugpointerfieldgetdereferencedfield"></a>IDebugPointerField::GetDereferencedField
Esse método retorna o tipo de objeto para o qual esse objeto ponteiro aponta.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetDereferencedField(
   IDebugField** ppField
);
```

```csharp
int GetDereferencedField(
   out IDebugField ppField
);
```

## <a name="parameters"></a>Parâmetros
`ppField`\
fora Retorna um [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) que descreve o tipo de objeto de destino.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Se, por exemplo, o objeto [IDebugPointerField](../../../extensibility/debugger/reference/idebugpointerfield.md) apontar para um inteiro, o tipo [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) retornado por esse método descreverá o tipo inteiro.

## <a name="see-also"></a>Confira também
- [IDebugPointerField](../../../extensibility/debugger/reference/idebugpointerfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
