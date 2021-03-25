---
description: Esse método obtém os utilitários de máquina para um servidor.
title: 'IDebugCoreServer2:: GetMachineUtilities_V7 | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer2::GetMachineUtilities_V7
helpviewer_keywords:
- IDebugCoreServer2::GetMachineUtilities_V7
ms.assetid: 64c1f08f-853b-4498-9810-29791581ef2f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 26d2c042c6f4a08acb7efc558bbc86021b16587e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077948"
---
# <a name="idebugcoreserver2getmachineutilities_v7"></a>IDebugCoreServer2::GetMachineUtilities_V7
Esse método obtém os utilitários de máquina para um servidor.

> [!NOTE]
> Este método é obsoleto: não use ( [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] sempre retorna `E_NOTIMPL` se esse método for chamado). Ele é retido por motivos históricos.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetMachineUtilities_V7(
   IDebugMDMUtil2_V7** ppUtil
);
```

```csharp
int GetMachineUtilities_V7(
   out IDebugMDMUtil2_V7 ppUtil
);
```

## <a name="parameters"></a>Parâmetros
`ppUtil`\
fora Retorna uma `IDebugMDMUtil2_V7` interface que representa as informações de utilitários de computador.

## <a name="return-value"></a>Valor Retornado
 Sempre retorna `E_NOTIMPL` , indicando que o método não está implementado.

## <a name="remarks"></a>Comentários
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] sempre retorna `E_NOTIMPL` se esse método for chamado.

## <a name="see-also"></a>Confira também
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
