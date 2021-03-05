---
description: Obtém a classificação ou o número de dimensões da matriz.
title: 'IDebugArrayField:: getrank | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayField::GetRank
helpviewer_keywords:
- IDebugArrayField::GetRank method
ms.assetid: 2364b876-5be1-4bab-9b8f-3b6121da35c6
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d9e3d822bac6fa16314f5d2962d69adbf74d0bc3
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102143708"
---
# <a name="idebugarrayfieldgetrank"></a>IDebugArrayField::GetRank
Obtém a classificação ou o número de dimensões da matriz.

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
 A classificação de uma matriz corresponde ao número de dimensões. Em C++ e C#, matrizes multidimensionais são realmente matrizes de matrizes e, portanto, podem ser consideradas apenas uma matriz unidimensional (e o `GetRank` método sempre retorna 1). Em [!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)] , por outro lado, as matrizes multidimensionais são tratadas de forma diferente e a classificação de tal matriz reflete o número de dimensões (e o `GetRank` método sempre retorna o número de dimensões).

## <a name="see-also"></a>Confira também
- [IDebugArrayField](../../../extensibility/debugger/reference/idebugarrayfield.md)
