---
description: Recupera um nome amigável para o servidor.
title: 'IDebugCoreServer3:: GetServerFriendlyName | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::GetServerFriendlyName
helpviewer_keywords:
- IDebugCoreServer3::GetServerFriendlyName
ms.assetid: 7035b904-b3d7-4d9b-98d9-65714b8a8b9f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a1ccb77cca920706dc7622e98dfca62743bf3b65
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102163103"
---
# <a name="idebugcoreserver3getserverfriendlyname"></a>IDebugCoreServer3::GetServerFriendlyName
Recupera um nome amigável para o servidor.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetServerFriendlyName(
   BSTR* pbstrName
);
```

```csharp
int GetServerFriendlyName(
   out string pbstrName
);
```

## <a name="parameters"></a>Parâmetros
`pbstrName`\
fora Retorna um nome amigável para o servidor.

> [!NOTE]
> O chamador é responsável por liberar a cadeia de caracteres.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna o código de erro.

## <a name="remarks"></a>Comentários
 Para servidores iniciados pelo usuário, o nome retornado por esse método é o nome completo do servidor. Para servidores iniciados automaticamente, o nome é o do computador no qual o servidor está sendo executado.

 Para um nome orientado a computador, chame o método [getServerName](../../../extensibility/debugger/reference/idebugcoreserver3-getservername.md) .

## <a name="see-also"></a>Confira também
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
- [GetServerName](../../../extensibility/debugger/reference/idebugcoreserver3-getservername.md)
