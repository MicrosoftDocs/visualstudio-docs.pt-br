---
description: Recupera uma descrição do computador no qual o servidor principal está sendo executado.
title: 'IDebugCoreServer2:: GetMachineInfo | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer2::GetInfo
helpviewer_keywords:
- IDebugCoreServer2::GetInfo
ms.assetid: 8fa1a1d3-9fcb-4fb3-bf4e-e7172ac08d77
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 710738bc2284d4cba29a451209a91dd12091f1af
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077870"
---
# <a name="idebugcoreserver2getmachineinfo"></a>IDebugCoreServer2::GetMachineInfo
Recupera uma descrição do computador no qual o servidor principal está sendo executado.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetMachineInfo( 
   MACHINE_INFO_FIELDS Fields,
   MACHINE_INFO*       pMachineInfo
);
```

```csharp
int GetMachineInfo( 
   enum_ MACHINE_INFO_FIELDS  Fields,
   MACHINE_INFO[]             pMachineInfo
);
```

## <a name="parameters"></a>Parâmetros
`Fields`\
no Uma combinação de sinalizadores da enumeração [MACHINE_INFO_FIELDS](../../../extensibility/debugger/reference/machine-info-fields.md) que especifica quais campos do `pMachineInfo` devem ser preenchidos.

 `pMachineInfo`\

 [entrada, saída] Uma estrutura de [MACHINE_INFO](../../../extensibility/debugger/reference/machine-info.md) que é preenchida com uma descrição do computador.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
- [MACHINE_INFO_FIELDS](../../../extensibility/debugger/reference/machine-info-fields.md)
- [MACHINE_INFO](../../../extensibility/debugger/reference/machine-info.md)
