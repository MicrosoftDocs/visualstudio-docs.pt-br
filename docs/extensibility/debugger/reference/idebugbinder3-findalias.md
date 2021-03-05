---
description: Esse método localiza um alias, dado um nome.
title: 'IDebugBinder3:: FindAlias | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3::FindAlias
helpviewer_keywords:
- IDebugBinder3::FindAlias method
ms.assetid: b8333701-2718-4983-8513-0875fb7cb730
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: db4d5cad6d0c2990141e0dd3a824425b8b53145b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102167718"
---
# <a name="idebugbinder3findalias"></a>IDebugBinder3::FindAlias
Esse método localiza um alias, dado um nome. Isso pesquisará todos os aliases no programa.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT FindAlias(
   LPCOLESTR     pcstrName,
   IDebugAlias** ppAlias
);
```

```csharp
int FindAlias(
   string          pcstrName,
   out IDebugAlias ppAlias
);
```

## <a name="parameters"></a>Parâmetros
`pcstrName`\
no Nome do alias a ser localizado.

`ppAlias`\
fora Alias encontrado (se houver) representado pela interface [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md) .

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` (se o alias não for encontrado) ou um código de erro.

## <a name="remarks"></a>Comentários
 Esse método inicializa o objeto de destino como nulo antes de chamar; em seguida, ele testa um valor nulo posteriormente para determinar se o alias foi encontrado ou não.

## <a name="see-also"></a>Confira também
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
