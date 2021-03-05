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
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3a246cda3f5b9395ae013b4bca9d4d27d6f8a5c1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102158534"
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
