---
title: IDiaSymbol::get_isOptimizedAway | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: c18b1e38-b152-4a13-aba0-59faded5b2e6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a78d1d11fcc03901a3c2ac6607b5ba50fc2a9c72
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85463298"
---
# <a name="idiasymbolget_isoptimizedaway"></a>IDiaSymbol::get_isOptimizedAway
Especifica se a variável é otimizada para fora.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_isOptimizedAway(
   BOOL* pRetVal);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Um ponteiro para um `BOOL` que especifica se a variável é otimizada para fora.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)