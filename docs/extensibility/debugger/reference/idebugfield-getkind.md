---
title: IDebugField::GetKind | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::GetKind
helpviewer_keywords:
- IDebugField::GetKind method
ms.assetid: e7c9c60a-8e55-4ecc-aa63-0c814a1e92cc
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9967351e4b0654a21cab21c2f17eedcbcb471fff
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/22/2019
ms.locfileid: "56678653"
---
# <a name="idebugfieldgetkind"></a>IDebugField::GetKind
Esse método obtém o tipo de campo.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetKind( 
   FIELD_KIND* pdwKind
);
```

```csharp
int GetKind(
   out enum_FIELD_KIND pdwKind
);
```

#### <a name="parameters"></a>Parâmetros
 `pdwKind`

 [out] Retorna o tipo de campo como uma combinação de [FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md) constantes.

## <a name="return-value"></a>Valor de retorno
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Consulte também
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md)