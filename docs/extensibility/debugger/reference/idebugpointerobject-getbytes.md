---
description: Obtém o valor apontado como uma série de bytes consecutivos.
title: 'IDebugPointerObject:: GetBytes | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerObject::GetBytes
helpviewer_keywords:
- IDebugPointerObject::GetBytes method
ms.assetid: e986c188-87fb-4b51-86e9-ee6a0035bdab
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4a150f819610de97ee292302d89e2007c6235aae
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087620"
---
# <a name="idebugpointerobjectgetbytes"></a>IDebugPointerObject::GetBytes
Obtém o valor apontado como uma série de bytes consecutivos.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetBytes( 
   DWORD  dwStart,
   DWORD  dwCount,
   BYTE*  pBytes,
   DWORD* pdwBytes
);
```

```csharp
int GetBytes(
   uint       dwStart,
   uint       dwCount,
   out byte[] pBytes,
   out uint   pdwBytes
);
```

## <a name="parameters"></a>Parâmetros
`dwStart`\
no Um deslocamento, em bytes, do início do objeto apontado para.

`dwCount`\
no O número de bytes a recuperar.

`pBytes`\
[entrada, saída] Uma matriz que é preenchida com o valor como uma série de bytes consecutivos, começando no deslocamento fornecido a partir do objeto apontado para.

`pdwBytes`\
fora Retorna o número de bytes realmente recuperados.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Esse método é usado se o ponteiro conforme representado por esse [IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md) aponta para um tipo primitivo ou uma matriz simples de tipos primitivos (ou seja, uma matriz que pode ser representada por uma sequência simples de bytes).

## <a name="see-also"></a>Confira também
- [IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)
- [SetBytes](../../../extensibility/debugger/reference/idebugpointerobject-setbytes.md)
