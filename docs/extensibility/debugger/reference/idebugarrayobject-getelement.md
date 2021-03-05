---
description: Obtém um elemento da matriz.
title: 'IDebugArrayObject:: GetElement | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayObject::GetElement
helpviewer_keywords:
- IDebugArrayObject::GetElement method
ms.assetid: 08b44341-7bf1-4a8c-8b79-98ae5785b195
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ea10afac9f5503288d257833d6dd59f9ba56fc6f
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102158651"
---
# <a name="idebugarrayobjectgetelement"></a>IDebugArrayObject::GetElement
Obtém um elemento da matriz.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetElement( 
   DWORD          dwIndex,
   IDebugObject** ppElement
);
```

```csharp
int GetElement(
   [In] uint dwIndex,
   out IDebugObject ppElement
);
```

## <a name="parameters"></a>Parâmetros
`dwIndex`\
no O índice do elemento.

`ppElement`\
fora Retorna uma interface [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) que representa o elemento.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Esse método vê todos os elementos de um objeto de matriz como uma matriz unidimensional, mesmo que o objeto de matriz seja multidimensional. Por exemplo, considerando a matriz `myarray[3][2][6]` e um `dwIndex` parâmetro de 20, esse método retornaria o elemento de e `myarray[1][1][2]` um `dwIndex` parâmetro de 21 retornaria o elemento de `myarray[1][1][3]` . Use o método [GetCount](../../../extensibility/debugger/reference/idebugarrayobject-getcount.md) para determinar o número total de elementos na matriz.

## <a name="see-also"></a>Confira também
- [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
