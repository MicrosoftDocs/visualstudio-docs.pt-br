---
title: IDebugReference2::GetParent | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::GetParent
helpviewer_keywords:
- IDebugReference2::GetParent
ms.assetid: e3061665-ad3e-4c1b-b33f-82755fa21be3
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ddef1d78d64f0e034aed9d48b59bf3e46ccba24f
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66339804"
---
# <a name="idebugreference2getparent"></a>IDebugReference2::GetParent
Obtém a referência pai de uma referência. Reservado para uso futuro.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetParent ( 
   IDebugReference2** ppParent
);
```

```csharp
int GetParent ( 
   out IDebugReference2 ppParent
);
```

## <a name="parameters"></a>Parâmetros
`ppParent`\
[out] Retorna um [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) objeto que representa o pai desta propriedade.

## <a name="return-value"></a>Valor de retorno
 Sempre retorna `E_NOTIMPL`.

## <a name="see-also"></a>Consulte também
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)