---
description: Esse método obtém o idioma que foi usado para compilar o código no endereço de depuração.
title: 'IDebugSymbolProvider:: GetLanguage | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetLanguage
helpviewer_keywords:
- IDebugSymbolProvider::GetLanguage method
ms.assetid: e4142183-3d8b-418f-907f-4ee4c753d8ce
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 86387e86261a91b77793e9a31ae4b415983e2c5c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102168550"
---
# <a name="idebugsymbolprovidergetlanguage"></a>IDebugSymbolProvider::GetLanguage
Esse método obtém o idioma que foi usado para compilar o código no endereço de depuração.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetLanguage( 
   IDebugAddress* pAddress,
   GUID*          pguidLanguage,
   GUID*          pguidLanguageVendor
);
```

```csharp
int GetLanguage(
   IDebugAddress pAddress,
   out Guid      pguidLanguage,
   out Guid      pguidLanguageVendor
);
```

## <a name="parameters"></a>Parâmetros
`pAddress`\
no Um objeto de endereço representado por uma interface [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) .

`pguidLanguage`\
fora Retorna um `GUID` que especifica o idioma.

`pguidLanguageVendor`\
fora Retorna um `GUID` que especifica o fornecedor do idioma.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 O mecanismo de depuração chama esse método para obter as informações necessárias para selecionar o avaliador de expressão correto.

## <a name="see-also"></a>Confira também
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
