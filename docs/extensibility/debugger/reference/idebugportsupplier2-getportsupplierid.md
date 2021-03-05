---
description: Obtém o identificador do fornecedor da porta.
title: 'IDebugPortSupplier2:: GetPortSupplierId | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2::GetPortSupplierId
helpviewer_keywords:
- IDebugPortSupplier2::GetPortSupplierId
ms.assetid: 741d0829-0943-49bf-b56e-61e836043006
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bbed2ba8dfa46477770815376046083a8f7c92f1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102145385"
---
# <a name="idebugportsupplier2getportsupplierid"></a>IDebugPortSupplier2::GetPortSupplierId
Obtém o identificador do fornecedor da porta.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetPortSupplierId( 
   GUID* pguidPortSupplier
);
```

```csharp
HRESULT GetPortSupplierId( 
   out Guid pguidPortSupplier
);
```

## <a name="parameters"></a>Parâmetros
`pguidPortSupplier`\
fora Retorna o GUID do fornecedor da porta.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
