---
title: IDebugAddress2::GetProcessID | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAddress2::GetProcessID
helpviewer_keywords:
- IDebugAddress2::GetProcessID method
ms.assetid: 2c18889d-074a-4b95-87b4-bf1a067f44ed
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 94873e9a9c05a0c5e9253ce53240ab6b4ca39064
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736582"
---
# <a name="idebugaddress2getprocessid"></a>IDebugAddress2::GetProcessID
Recupera o ID do processo que possui o objeto representado por esta interface [IDebugAddress2.](../../../extensibility/debugger/reference/idebugaddress2.md)

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetProcessID (
   DWORD* pProcID
);
```

```csharp
int GetProcessID (
   out uint pProcID
);
```

## <a name="parameters"></a>parâmetros
`pProcID`\
[fora] A id do processo.

## <a name="return-value"></a>Valor retornado
 Se for bem sucedido, retorna S_OK; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDebugAddress2](../../../extensibility/debugger/reference/idebugaddress2.md)
