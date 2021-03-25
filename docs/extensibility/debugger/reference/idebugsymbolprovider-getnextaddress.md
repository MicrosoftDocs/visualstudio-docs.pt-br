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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dc269dcfc472c2f8bb3e5a9ed9a91ecd25292870
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075569"
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
