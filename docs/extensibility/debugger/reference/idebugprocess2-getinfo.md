---
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
ms.openlocfilehash: cf4b8d933729c95eaffa3a0caa44961bb5c87baa
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99894914"
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

## <a name="return-value"></a>Valor de retorno
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [PROCESS_INFO_FIELDS](../../../extensibility/debugger/reference/process-info-fields.md)
- [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)
