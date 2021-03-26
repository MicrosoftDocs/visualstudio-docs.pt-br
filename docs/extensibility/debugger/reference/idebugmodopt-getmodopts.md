---
description: Recupera uma lista de modificadores opcionais.
title: 'IDebugModOpt:: GetModOpts | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugModOpt::GetModOpts
- GetModOpts
ms.assetid: cb513fa9-d521-4a65-b968-f55f53a368df
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 614ecb456b6f644dfd389020bbffb23691cfbf43
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081900"
---
# <a name="idebugmodoptgetmodopts"></a>IDebugModOpt::GetModOpts
Recupera uma lista de modificadores opcionais.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetModOpts(
   ULONG  celt,
   BSTR*  rgelt,
   ULONG* pceltFetched
);
```

```csharp
int GetModOpts(
   uint         celt,
   out string[] rgelt,
   ref uint     pceltFetched
);
```

## <a name="parameters"></a>Parâmetros
`celt`\
no Número de elementos a serem retornados.

`rgelt`\
fora Retorna uma matriz que contém as opções.

`pceltFetched`\
[entrada, saída] Número de elementos retornados na `rgelt` matriz.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDebugModOpt](../../../extensibility/debugger/reference/idebugmodopt.md)
