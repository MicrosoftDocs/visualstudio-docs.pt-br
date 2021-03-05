---
description: Obtém uma descrição do processo.
title: 'IDebugProcess2:: GetInfo | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::GetInfo
helpviewer_keywords:
- IDebugProcess2::GetInfo
ms.assetid: 46021dce-bb97-46c3-b0cc-e5b3b68acc35
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a6e6b8e0c14cee960d1991ae4f5a482f66e89465
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102169204"
---
# <a name="idebugprocess2getinfo"></a>IDebugProcess2::GetInfo
Obtém uma descrição do processo.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetInfo(
   PROCESS_INFO_FIELDS  Fields,
   PROCESS_INFO*        pProcessInfo
);
```

```csharp
int GetInfo(
   enum_PROCESS_INFO_FIELDS  Fields,
   PROCESS_INFO[]            pProcessInfo
);
```

## <a name="parameters"></a>Parâmetros
`Fields`\
no Uma combinação de valores da enumeração [PROCESS_INFO_FIELDS](../../../extensibility/debugger/reference/process-info-fields.md) que especifica quais campos do `pProcessInfo` parâmetro devem ser preenchidos.

`pProcessInfo`\
fora Uma estrutura de [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md) que é preenchida com uma descrição do processo.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [PROCESS_INFO_FIELDS](../../../extensibility/debugger/reference/process-info-fields.md)
- [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)
