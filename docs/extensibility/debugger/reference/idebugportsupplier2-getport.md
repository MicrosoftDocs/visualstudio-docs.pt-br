---
description: Obtém uma porta de um fornecedor de porta.
title: 'IDebugPortSupplier2:: GetPort | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2::GetPort
helpviewer_keywords:
- IDebugPortSupplier2::GetPort
ms.assetid: d55d5055-7386-4037-bf22-4c3e434a99ca
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3c5626ce41181a711aafb7dbf26bbe5a65f218c9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072163"
---
# <a name="idebugportsupplier2getport"></a>IDebugPortSupplier2::GetPort
Obtém uma porta de um fornecedor de porta.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetPort( 
   REFGUID       guidPort,
   IDebugPort2** ppPort
);
```

```csharp
int GetPort( 
   ref Guid        guidPort,
   out IDebugPort2 ppPort
);
```

## <a name="parameters"></a>Parâmetros
`guidPort`\
no GUID (identificador global exclusivo) da porta.

`ppPort`\
fora Retorna um objeto [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) que representa a porta.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro. Retorna `E_PORTSUPPLIER_NO_PORT` se não existir nenhuma porta com o identificador fornecido.

## <a name="see-also"></a>Confira também
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
