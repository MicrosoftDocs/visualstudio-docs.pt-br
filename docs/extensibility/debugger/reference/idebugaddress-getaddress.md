---
description: Retorna uma estrutura que descreve um objeto e sua localização dentro de seu escopo ou contêiner.
title: 'IDebugAddress:: GetAddress | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAddress::GetAddress
helpviewer_keywords:
- IDebugAddress:GetAddress method
ms.assetid: 2590387b-5d36-4116-9a75-737957b8898e
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 52c52d12d8c357f4dbadeef673a3dc4474713ce9
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102145437"
---
# <a name="idebugaddressgetaddress"></a>IDebugAddress::GetAddress
Retorna uma estrutura que descreve um objeto e sua localização dentro de seu escopo ou contêiner.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetAddress (
   DEBUG_ADDRESS * pAddress
);
```

```csharp
int GetAddress(
   DEBUG_ADDRESS[] pAddress
);
```

## <a name="parameters"></a>Parâmetros
`pAddress`\
[entrada, saída] Uma estrutura de [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md) que é preenchida por este método.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 A estrutura de [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md) é passada para esse método, que o preenche com as informações apropriadas. A forma como essas informações são interpretadas depende do tipo de informação retornado e do próprio manipulador de símbolos. Consulte [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md) para obter mais detalhes.

## <a name="see-also"></a>Confira também
- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)
