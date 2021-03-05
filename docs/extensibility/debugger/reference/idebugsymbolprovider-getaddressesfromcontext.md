---
description: Esse método mapeia um contexto de documento em uma matriz de endereços de depuração.
title: 'IDebugSymbolProvider:: GetAddressesFromContext | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetAddressesFromContext
helpviewer_keywords:
- IDebugSymbolProvider::GetAddressesFromContext method
ms.assetid: a3124883-a255-4543-a5ec-e1c7a97beb69
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7fcbc974fe3556f16d339f8be8b8f1738fa8eb74
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102159686"
---
# <a name="idebugsymbolprovidergetaddressesfromcontext"></a>IDebugSymbolProvider::GetAddressesFromContext
Esse método mapeia um contexto de documento em uma matriz de endereços de depuração.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetAddressesFromContext( 
   IDebugDocumentContext2* pDocContext,
   BOOL                    fStatmentOnly,
   IEnumDebugAddresses**   ppEnumBegAddresses,
   IEnumDebugAddresses**   ppEnumEndAddresses
);
```

```csharp
int GetAddressesFromContext(
   IDebugDocumentContext2  pDocContext,
   bool                    fStatmentOnly,
   out IEnumDebugAddresses ppEnumBegAddresses,
   out IEnumDebugAddresses ppEnumEndAddresses
);
```

## <a name="parameters"></a>Parâmetros
`pDocContext`\
no O contexto do documento.

`fStatmentOnly`\
no Se for TRUE, limita os endereços de depuração a uma única instrução.

`ppEnumBegAddresses`\
fora Retorna um enumerador para os endereços de depuração inicial associados a esta instrução ou linha.

`ppEnumEndAddresses`\
fora Retorna um enumerador [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md) para os endereços de depuração finais associados a esta instrução ou linha.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Um contexto de documento normalmente indica um intervalo de linhas de origem. Esse método fornece os endereços de depuração inicial e final associados a essas linhas. Algumas linguagens permitem instruções que abrangem várias linhas ou linhas que contêm mais de uma instrução. Esse método fornece um sinalizador para limitar os endereços de depuração a uma única instrução.

 É possível que uma única instrução tenha vários endereços de depuração, como no caso de modelos.

## <a name="see-also"></a>Confira também
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)
- [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)
