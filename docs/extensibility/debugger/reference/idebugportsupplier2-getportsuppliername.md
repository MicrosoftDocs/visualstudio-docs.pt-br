---
title: IDebugPortSupplier2:GetPortSupplierName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2::GetPortSupplierName
helpviewer_keywords:
- IDebugPortSupplier2::GetPortSupplierName
ms.assetid: e4c368ab-640d-4b5b-9f74-810dc9364d8f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 24eac6d1dee8e76caf70fed9071bd1ae7412fdc6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724586"
---
# <a name="idebugportsupplier2getportsuppliername"></a>IDebugPortSupplier2::GetPortSupplierName
Pega o nome do fornecedor do porto.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetPortSupplierName( 
   BSTR* pbstrName
);
```

```csharp
int GetPortSupplierName( 
   out string pbstrName
);
```

## <a name="parameters"></a>parâmetros
`pbstrName`\
[fora] Retorna o nome do fornecedor do porto.

## <a name="return-value"></a>Valor retornado
 Se for `S_OK`bem sucedido, retorna; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
