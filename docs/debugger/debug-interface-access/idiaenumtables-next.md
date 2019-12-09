---
title: IDiaEnumTables::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumTables::Next method
ms.assetid: 8d7bd359-d33e-4317-9674-d89283efd7de
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 688652fe3915e1974d5d0e1d04fb1ac075863d8c
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72743736"
---
# <a name="idiaenumtablesnext"></a>IDiaEnumTables::Next
Recupera um número especificado de tabelas na sequência de enumeração.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT Next ( 
   ULONG       celt,
   IDiaTable** rgelt,
   ULONG*      pceltFetched
);
```

#### <a name="parameters"></a>Parâmetros
 `celt`

no O número de tabelas no enumerador a ser recuperado.

 `rgelt`

fora Uma matriz que deve ser preenchida com os objetos [IDiaTable](../../debugger/debug-interface-access/idiatable.md) que representam as tabelas desejadas.

 `pceltFetched`

fora Retorna o número de tabelas no enumerador obtido.

## <a name="return-value"></a>Valor retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não houver mais tabelas. Caso contrário, retornará um código de erro.

## <a name="see-also"></a>Consulte também
- [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)
- [IDiaTable](../../debugger/debug-interface-access/idiatable.md)