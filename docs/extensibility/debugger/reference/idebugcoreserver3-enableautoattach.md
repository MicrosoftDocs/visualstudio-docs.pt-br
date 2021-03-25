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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0e3b78744d67183c368345af8c6c26e57edec8d1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058671"
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
