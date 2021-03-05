---
description: Obtém a mensagem de exibição.
title: 'IDebugOutputStringEvent2:: GetString | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugOutputStringEvent2::GetString
helpviewer_keywords:
- IDebugOutputStringEvent2::GetString
ms.assetid: f059f8e0-ad44-49ac-ba90-73576ada5e06
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 958ea04c3366aebf248f50915668709a8438a2dc
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102169971"
---
# <a name="idebugoutputstringevent2getstring"></a>IDebugOutputStringEvent2::GetString
Obtém a mensagem de exibição.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetString( 
   BSTR* pbstrString
);
```

```csharp
int GetString( 
   out string pbstrString
);
```

## <a name="parameters"></a>Parâmetros
`pbstrString`\
fora Retorna a mensagem de exibição.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDebugOutputStringEvent2](../../../extensibility/debugger/reference/idebugoutputstringevent2.md)
