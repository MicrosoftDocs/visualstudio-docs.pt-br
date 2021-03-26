---
description: Obtém o fornecedor da porta para esta porta.
title: 'IDebugPort2:: GetPortSupplier | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPort2::GetPortSupplier
helpviewer_keywords:
- IDebugPort2::GetPortSupplier
ms.assetid: 7a7b0615-df6b-4726-ab35-39dfa1ebed8f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dde5dc8545926aa74f7e2bc70df073f5f18952ce
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087360"
---
# <a name="idebugport2getportsupplier"></a>IDebugPort2::GetPortSupplier
Obtém o fornecedor da porta para esta porta.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetPortSupplier( 
   IDebugPortSupplier2** ppSupplier
);
```

```csharp
int GetPortSupplier( 
   out IDebugPortSupplier2 ppSupplier
);
```

## <a name="parameters"></a>Parâmetros
`ppSupplier`\
fora Retorna um objeto [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md) representa o fornecedor da porta para uma porta.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
