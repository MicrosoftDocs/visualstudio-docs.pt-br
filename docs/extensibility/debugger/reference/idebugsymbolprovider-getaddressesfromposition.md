---
description: Esse método mapeia uma posição de documento em uma matriz de endereços de depuração.
title: 'IDebugSymbolProvider:: GetAddressesFromPosition | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetAddressesFromPosition
helpviewer_keywords:
- IDebugSymbolProvider::GetAddressesFromPosition method
ms.assetid: 1b0f02cb-8ace-4614-88f3-0e10239012b3
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d4437055ccd693b40fe4f1f7d6364d9601c827a3
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102159673"
---
# <a name="idebugsymbolprovidergetaddressesfromposition"></a>IDebugSymbolProvider::GetAddressesFromPosition
Esse método mapeia uma posição de documento em uma matriz de endereços de depuração.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetAddressesFromPosition( 
   IDebugDocumentPosition2* pDocPos,
   BOOL                     fStatmentOnly,
   IEnumDebugAddresses**    ppEnumBegAddresses,
   IEnumDebugAddresses**    ppEnumEndAddresses
);
```

```csharp
int GetAddressesFromPosition( 
   IDebugDocumentPosition2  pDocPos,
   bool                     fStatmentOnly,
   out IEnumDebugAddresses  ppEnumBegAddresses,
   out IEnumDebugAddresses  ppEnumEndAddresses
);
```

## <a name="parameters"></a>Parâmetros
`pDocPos`\
no A posição do documento.

`fStatmentOnly`\
no Se for TRUE, limita os endereços de depuração a uma única instrução.

`ppEnumBegAddresses`\
fora Retorna um enumerador para os endereços de depuração inicial associados a esta instrução ou linha.

`ppEnumEndAddresses`\
fora Retorna um enumerador [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md) para os endereços de depuração finais associados a esta instrução ou linha.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Uma posição de documento normalmente indica um intervalo de linhas de origem. Esse método fornece os endereços de depuração inicial e final associados a essas linhas. Algumas linguagens permitem instruções que abrangem várias linhas ou linhas que contêm mais de uma instrução. Esse método fornece um sinalizador para limitar os endereços de depuração a uma única instrução.

 É possível que uma única instrução tenha vários endereços de depuração, como no caso de modelos.

## <a name="see-also"></a>Confira também
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [GetAddressesFromContext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md)
- [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)
