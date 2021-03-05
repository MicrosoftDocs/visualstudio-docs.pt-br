---
description: Obtém a ID do processo da porta em si.
title: 'IDebugPortEx2:: GetPortProcessId | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEx2::GetPortProcessId
helpviewer_keywords:
- IDebugPortEx2::GetPortProcessId
ms.assetid: be85be66-47e6-415f-b0ca-24599aa5f13c
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e10dbc648f8233a826c440c261308c6c3688fa30
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102169425"
---
# <a name="idebugportex2getportprocessid"></a>IDebugPortEx2::GetPortProcessId
Obtém a ID do processo da porta em si.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetPortProcessId ( 
   DWORD* pdwProcessId
);
```

```csharp
int GetPortProcessId ( 
   out uint pdwProcessId
);
```

## <a name="parameters"></a>Parâmetros
`pdwProcessId`\
fora Retorna a ID de processo físico da porta em si.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 No tempo de execução do Win32, por exemplo, esse método normalmente chama a função do Win32 `GetCurrentProcessId` para obter a ID do processo físico.

## <a name="see-also"></a>Confira também
- [IDebugPortEx2](../../../extensibility/debugger/reference/idebugportex2.md)
