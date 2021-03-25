---
description: Obtém a classificação da matriz, ou seja, o número de dimensões.
title: 'IDebugArrayObject:: getrank | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayObject::GetRank
helpviewer_keywords:
- IDebugArrayObject::GetRank method
ms.assetid: 9948551a-e334-4ff6-979c-08dab633b9b6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1440ff2fa82c8296bf54b106b622556a8eebb611
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094322"
---
# <a name="idebugarrayobjectgetrank"></a>IDebugArrayObject::GetRank
Obtém a classificação da matriz, ou seja, o número de dimensões.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetRank( 
   DWORD* pdwRank
);
```

```csharp
int GetRank(
   out uint pdwRank
);
```

## <a name="parameters"></a>Parâmetros
`pdwRank`\
fora Retorna a classificação.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Use o método [GetDimensions](../../../extensibility/debugger/reference/idebugarrayobject-getdimensions.md) para recuperar o tamanho de cada dimensão do objeto de matriz.

## <a name="see-also"></a>Confira também
- [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
