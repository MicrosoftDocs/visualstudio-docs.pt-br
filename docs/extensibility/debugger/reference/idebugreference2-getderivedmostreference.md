---
description: Obtém a referência mais derivada de uma referência.
title: 'IDebugReference2:: GetDerivedMostReference | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::GetDerivedMostReference
helpviewer_keywords:
- IDebugReference2::GetDerivedMostReference
ms.assetid: 07253b74-7d39-48e0-8e85-ac8dfd919f6e
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1517b1be34b62defcd5f19792baa2ac6c343b85b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102168970"
---
# <a name="idebugreference2getderivedmostreference"></a>IDebugReference2::GetDerivedMostReference
Obtém a referência mais derivada de uma referência. Reservado para uso futuro.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetDerivedMostReference( 
   IDebugReference2** ppDerivedMost
);
```

```csharp
int GetDerivedMostReference( 
   out IDebugReference2 ppDerivedMost
);
```

## <a name="parameters"></a>Parâmetros
`ppDerivedMost`\
fora Retorna um objeto [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) que representa a propriedade mais derivada.

## <a name="return-value"></a>Valor Retornado
 Sempre retorna `E_NOTIMPL`.

## <a name="remarks"></a>Comentários
 Por exemplo, se essa propriedade descrever um objeto que implementa, `ClassRoot` mas que, na verdade, é uma instanciação de `ClassDerived` que é derivada de `ClassRoot` , esse método retornará um objeto [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) que representa uma referência ao `ClassDerived` objeto.

## <a name="see-also"></a>Confira também
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
