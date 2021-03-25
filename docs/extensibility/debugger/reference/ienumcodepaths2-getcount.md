---
description: Retorna o número de elementos na enumeração de caminhos de código.
title: 'IEnumCodePaths2:: GetCount | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumCodePaths2::GetCount
helpviewer_keywords:
- IEnumCodePaths2::GetCount
ms.assetid: 988c5092-fcc5-43a1-a94c-c261edd56ebf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9b2b91673b850d7c9db184798a89f805feddb54b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080210"
---
# <a name="ienumcodepaths2getcount"></a>IEnumCodePaths2::GetCount
Retorna o número de elementos na enumeração.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetCount(
   ULONG* pcelt
);
```

```csharp
int GetCount(
   out uint pcelt
);
```

## <a name="parameters"></a>Parâmetros
`pcelt`\
fora Retorna o número de elementos na enumeração.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Esse método não faz parte da interface de enumeração com personalizada que especifica que apenas os `Next` métodos, `Clone` , `Skip` e `Reset` precisam ser implementados.

## <a name="see-also"></a>Confira também
- [IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md)
