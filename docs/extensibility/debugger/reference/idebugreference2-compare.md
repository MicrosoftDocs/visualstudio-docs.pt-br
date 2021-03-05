---
description: Compara uma referência a outra.
title: 'IDebugReference2:: Compare | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::Compare
helpviewer_keywords:
- IDebugReference2::Compare
ms.assetid: 3361c495-2673-4b7c-82e3-dee74e1fa58d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ef006cba574e0cc5f51d2ec45eb6187b1076543a
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102165995"
---
# <a name="idebugreference2compare"></a>IDebugReference2::Compare
Compara uma referência a outra. Reservado para uso futuro.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Compare ( 
   REFERENCE_COMPARE dwCompare,
   IDebugReference2* pReference
);
```

```csharp
int Compare ( 
   enum_REFERENCE_COMPARE dwCompare,
   IDebugReference2       pReference
);
```

## <a name="parameters"></a>Parâmetros
`dwCompare`\
no Um valor da enumeração [REFERENCE_COMPARE](../../../extensibility/debugger/reference/reference-compare.md) que especifica a operação de comparação, por exemplo, igual a, menor que ou maior que.

`pReference`\
no Um objeto [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) que representa a referência a ser comparado com.

## <a name="return-value"></a>Valor Retornado
 Sempre retorna `E_NOTIMPL`.

## <a name="see-also"></a>Confira também
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [REFERENCE_COMPARE](../../../extensibility/debugger/reference/reference-compare.md)
