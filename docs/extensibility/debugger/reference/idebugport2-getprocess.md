---
description: Obtém o processo especificado em execução em uma porta.
title: 'IDebugPort2:: GetProcess | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPort2::GetPortSupplier
helpviewer_keywords:
- IDebugPort2::GetPortSupplier
ms.assetid: 3e2431b0-0e19-450d-8e1d-d7c314c8f872
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b2ae7031a747ac31b2ec56b78de52dbc156973e5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087347"
---
# <a name="idebugport2getprocess"></a>IDebugPort2::GetProcess
Obtém o processo especificado em execução em uma porta.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetProcess( 
   AD_PROCESS_ID    ProcessId,
   IDebugProcess2** ppProcess
);
```

```csharp
int GetProcess( 
   AD_PROCESS_ID      ProcessId,
   out IDebugProcess2 ppProcess
);
```

## <a name="parameters"></a>Parâmetros
`ProcessId`\
no Uma estrutura de [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) que especifica o identificador do processo.

`ppProcess`\
fora Retorna um objeto [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) que representa o processo.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)
