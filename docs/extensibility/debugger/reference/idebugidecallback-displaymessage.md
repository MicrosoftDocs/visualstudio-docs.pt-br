---
description: Envia a cadeia de caracteres da mensagem especificada para a janela de saída do depurador.
title: IDebugIDECallback::D isplayMessage | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugIDECallback::DisplayMessage
ms.assetid: c19b48ee-b370-4fce-91fe-f82bf1e63179
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6968c524559280756014bb6b26f55f688bc38ab3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091936"
---
# <a name="idebugidecallbackdisplaymessage"></a>IDebugIDECallback::DisplayMessage
Envia a cadeia de caracteres da mensagem especificada para a janela de saída do depurador.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT DisplayMessage (
   LPCOLESTR szMessage
);
```

```csharp
int DisplayMessage (
   string szMessage
);
```

## <a name="parameters"></a>Parâmetros
`szMessage`\
no Cadeia de caracteres de mensagem a ser exibida na janela de saída do depurador.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDebugIDECallback](../../../extensibility/debugger/reference/idebugidecallback.md)
