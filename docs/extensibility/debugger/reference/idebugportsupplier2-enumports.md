---
description: Recupera uma lista de todas as portas fornecidas por um fornecedor de porta.
title: 'IDebugPortSupplier2:: EnumPorts | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2::EnumPorts
helpviewer_keywords:
- IDebugPortSupplier2::EnumPorts
ms.assetid: 88b57fd2-eba1-44fa-bd34-cf2ad2b1ff87
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b68ce91913af8d42a4a5e023089bb45bcb5563b5
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102169217"
---
# <a name="idebugportsupplier2enumports"></a>IDebugPortSupplier2::EnumPorts
Recupera uma lista de todas as portas fornecidas por um fornecedor de porta.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT EnumPorts( 
   IEnumDebugPorts2** ppEnum
);
```

```csharp
int EnumPorts( 
   out IEnumDebugPorts2 ppEnum
);
```

## <a name="parameters"></a>Parâmetros
`ppEnum`\
fora Retorna um objeto [IEnumDebugPorts2](../../../extensibility/debugger/reference/ienumdebugports2.md) que contém uma lista de portas fornecidas.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IEnumDebugPorts2](../../../extensibility/debugger/reference/ienumdebugports2.md)
