---
title: 'IDebugSymbolProvider:: GetTypeByName | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetTypeByName
helpviewer_keywords:
- IDebugSymbolProvider::GetTypeByName method
ms.assetid: b9d88d3b-8b75-484a-b9cc-dc8c0fbb4bc8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ce4dfab898190eb89c58503e378b410ddfc240de
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "80719189"
---
# <a name="idebugsymbolprovidergettypebyname"></a>IDebugSymbolProvider::GetTypeByName
Esse método mapeia um nome de símbolo para um tipo de símbolo.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetTypeByName( 
   LPCOLESTR     pszClassName,
   NAME_MATCH    nameMatch,
   IDebugField** ppField
);
```

```csharp
int GetTypeByName(
   string          pszClassName,
   NAME_MATCH      nameMatch,
   out IDebugField ppField
);
```

## <a name="parameters"></a>Parâmetros
`pszClassName`\
no O nome do símbolo.

`nameMatch`\
no Seleciona o tipo de correspondência, por exemplo, diferencia maiúsculas de minúsculas. Um valor da enumeração de [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md) .

`ppField`\
fora Retorna o tipo de símbolo como um objeto [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) .

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Este método é uma versão genérica do [GetClassTypeByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getclasstypebyname.md).

## <a name="see-also"></a>Confira também
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md)
- [GetClassTypeByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getclasstypebyname.md)
