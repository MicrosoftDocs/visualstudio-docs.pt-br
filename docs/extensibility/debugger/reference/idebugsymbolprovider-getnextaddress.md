---
description: Obtém o endereço de depuração que segue um determinado endereço de depuração em um método.
title: 'IDebugSymbolProvider:: GetNextAddress | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetNextAddress
helpviewer_keywords:
- IDebugSymbolProvider::GetNextAddress method
ms.assetid: 704eeb94-cb13-49d1-82b6-7d83ed0f19c0
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d177d03daef4f8d3344941658b85f71551af126b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102168407"
---
# <a name="idebugsymbolprovidergetnextaddress"></a>IDebugSymbolProvider::GetNextAddress
Obtém o endereço de depuração que segue um determinado endereço de depuração em um método.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetNextAddress( 
   IDebugAddress*  pAddress,
   BOOL            fStatementOnly,
   IDebugAddress** ppAddress
);
```

```csharp
int GetNextAddress( 
   IDebugAddress     pAddress,
   bool              fStatementOnly,
   out IDebugAddress ppAddress
);
```

## <a name="parameters"></a>Parâmetros
`pAddress`\
no Endereço de depuração fornecido.

`fStatementOnly`\
no Se for TRUE, limita os endereços de depuração a uma única instrução.

`ppAddress`\
fora Retorna o próximo endereço de depuração.

## <a name="return-value"></a>Valor Retornado
 Retorna um válido `HRESULT` , normalmente S_OK.

## <a name="see-also"></a>Confira também
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
