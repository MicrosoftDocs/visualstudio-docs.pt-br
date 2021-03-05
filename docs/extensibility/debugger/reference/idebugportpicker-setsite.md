---
description: Define o provedor de serviços.
title: 'IDebugPortPicker:: SetSite | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortPicker::SetSite
ms.assetid: 7319e187-adfe-4b3f-aec9-521356fb5a8a
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d1c222bd06a974e7f2b1a57096a120399b554b82
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102169269"
---
# <a name="idebugportpickersetsite"></a>IDebugPortPicker::SetSite
Define o provedor de serviços.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT SetSite(
   IServiceProvider * pSP
);
```

```csharp
public int SetSite(
   IServiceProvider pSP
);
```

## <a name="parameters"></a>Parâmetros
`pSP`\
no Referência à interface do provedor de serviços.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Esse método será chamado antes que quaisquer outros métodos sejam chamados.

## <a name="see-also"></a>Confira também
- [IDebugPortPicker](../../../extensibility/debugger/reference/idebugportpicker.md)
