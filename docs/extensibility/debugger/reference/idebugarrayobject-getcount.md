---
description: Obtém a contagem de elementos na matriz.
title: 'IDebugArrayObject:: GetCount | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayObject::GetCount
helpviewer_keywords:
- IDebugArrayObject::GetCount method
ms.assetid: 7931f3f7-033c-4bf8-8abd-95183952ebb0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c3a5d052fcb2c40f9dad76791aa992dbfbde72b0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058892"
---
# <a name="idebugarrayobjectgetcount"></a>IDebugArrayObject::GetCount
Obtém a contagem de elementos na matriz.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetCount( 
   DWORD* pdwElements
);
```

```csharp
int GetCount(
   out uint pdwElements
);
```

## <a name="parameters"></a>Parâmetros
`pdwElements`\
fora Retorna a contagem.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Esse método vê todos os elementos de um objeto de matriz como uma matriz unidimensional, mesmo que o objeto de matriz seja multidimensional. Por exemplo, dada a matriz `myarray[3][2][6]` , esse método retornaria 36 no `pdwElements` parâmetro. Use o método [GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md) para recuperar os elementos individuais um de cada vez.

## <a name="see-also"></a>Confira também
- [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
