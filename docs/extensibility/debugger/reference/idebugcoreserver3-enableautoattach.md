---
description: Habilita a anexação automática para os mecanismos de depuração especificados.
title: 'IDebugCoreServer3:: EnableAutoAttach | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::EnableAutoAttach
helpviewer_keywords:
- IDebugCoreServer3::EnableAutoAttach
ms.assetid: 06aa633b-263b-4e08-8844-9a52d5120b94
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 644d238db11c117b9068de8f7903361b9712f3aa
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102163142"
---
# <a name="idebugcoreserver3enableautoattach"></a>IDebugCoreServer3::EnableAutoAttach
Habilita a anexação automática para os mecanismos de depuração especificados.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT EnableAutoAttach(
   GUID*     rgguidSpecificEngines,
   DWORD     celtSpecificEngines,
   LPCOLESTR pszStartPageUrl,
   BSTR*     pbstrSessionId
);
```

```csharp
int EnableAutoAttach(
   Guid[]     rgguidSpecificEngines,
   uint       celtSpecificEngines,
   string     pszStartPageUrl,
   out string pbstrSessionId
);
```

## <a name="parameters"></a>Parâmetros
`rgguidSpecificEngines`\
no Matriz de GUIDs para cada mecanismo de depuração a ser marcado como anexação automática.

`celtSpecificEngines`\
no O número de mecanismos especificado em `rgguidSpecificEngines` .

`pszStartPageUrl`\
no A URL inicial a ser usada ao anexar automaticamente.

`pbstrSessionID`\
fora ID da sessão que foi anexada automaticamente.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna o código de erro. Um código de erro é `E_AUTO_ATTACH_NOT_REGISTERED` , que indica que a fábrica de classes de anexação automática não foi registrada.

## <a name="remarks"></a>Comentários
 Quando um programa associado à URL especificada é iniciado, os mecanismos de depuração especificados são iniciados e anexados automaticamente.

## <a name="see-also"></a>Confira também
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
