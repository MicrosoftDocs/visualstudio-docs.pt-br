---
description: Define o valor apontado de uma série de bytes consecutivos.
title: 'IDebugPointerObject:: setBytes | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerObject::SetBytes
helpviewer_keywords:
- IDebugPointerObject::SetBytes method
ms.assetid: 8c578b38-38d7-46f3-bb2e-8a730fccd334
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 015a7782fae01f06a9d1cc4a5e64090303d2f2e0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087581"
---
# <a name="idebugpointerobjectsetbytes"></a>IDebugPointerObject::SetBytes
Define o valor apontado de uma série de bytes consecutivos.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT SetBytes( 
   DWORD  dwStart,
   DWORD  dwCount,
   BYTE*  pBytes,
   DWORD* pdwBytes
);
```

```csharp
int SetBytes(
   uint     dwStart,
   uint     dwCount,
   byte[]   pBytes,
   out uint pdwBytes
);
```

## <a name="parameters"></a>Parâmetros
`dwStart`\
no Um deslocamento, em bytes, do início do objeto apontado para.

`dwCount`\
no O número de bytes a serem definidos.

`pBytes`\
no Uma matriz de bytes que representa o novo valor. Esse valor é armazenado no objeto, começando no deslocamento fornecido.

`pdwBytes`\
fora Retorna o número de bytes realmente definidos.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Esse método é usado se o ponteiro conforme representado por esse [IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md) aponta para um tipo primitivo ou uma matriz simples de tipos primitivos (ou seja, uma matriz que pode ser representada por uma sequência simples de bytes). Este `IDebugPointerObject` objeto não pode ser uma referência nula (ele deve apontar para um endereço na memória).

## <a name="see-also"></a>Confira também
- [GetBytes](../../../extensibility/debugger/reference/idebugpointerobject-getbytes.md)
- [IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)
