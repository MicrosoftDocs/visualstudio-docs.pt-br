---
description: Esse método redefine a enumeração de campos para o primeiro elemento.
title: 'IEnumDebugFields:: Reset | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugFields::Reset
helpviewer_keywords:
- IEnumDebugFields::Reset method
ms.assetid: 38ff61e4-0120-42e8-971a-16be6050b425
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2edf4751151779297d6ff8ed9ffa930cc7bf3868
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086531"
---
# <a name="ienumdebugfieldsreset"></a>IEnumDebugFields::Reset
Esse método redefine a enumeração para o primeiro elemento.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Reset(void);
```

```csharp
int Reset();
```

#### <a name="parameters"></a>Parâmetros
 Nenhum

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Depois que esse método é chamado, a próxima chamada para [Next](../../../extensibility/debugger/reference/ienumdebugfields-next.md) retorna o primeiro elemento da enumeração.

## <a name="see-also"></a>Confira também
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [Próximo](../../../extensibility/debugger/reference/ienumdebugfields-next.md)
