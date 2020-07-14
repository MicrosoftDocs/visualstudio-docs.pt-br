---
title: IDiaEnumTables::Skip | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumTables::Skip method
ms.assetid: 5c9db956-0654-4f1a-8775-530aa980d8ec
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 27daf70a3cc5f155bfbe6b2678cce42b50801153
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85467459"
---
# <a name="idiaenumtablesskip"></a>IDiaEnumTables::Skip
Ignora um número especificado de tabelas em uma sequência de enumeração.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT Skip ( 
   ULONG celt
);
```

#### <a name="parameters"></a>Parâmetros
 `celt`

no O número de tabelas na sequência de enumeração a serem ignoradas.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK` ; caso contrário, retornará `S_FALSE` se não houver mais tabelas a serem ignoradas.

## <a name="see-also"></a>Veja também
- [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)