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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 92e616ded029c22b16b81ccd5f25086b11be6ff4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094387"
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
