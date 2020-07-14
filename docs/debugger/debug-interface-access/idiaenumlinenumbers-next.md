---
title: IDiaEnumLineNumbers::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumLineNumbers::Next method
ms.assetid: 363d5b40-1316-4ab8-836f-63637f619e0a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1546c0bc7b8682b918d583769a9f580323c9dda4
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85468206"
---
# <a name="idiaenumlinenumbersnext"></a>IDiaEnumLineNumbers::Next
Recupera um número especificado de números de linha na sequência de enumeração.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT Next ( 
   ULONG            celt,
   IDiaLineNumber** rgelt,
   ULONG*           pceltFetched
);
```

#### <a name="parameters"></a>Parâmetros
 celt

no O número de números de linha no enumerador a ser recuperado.

 rgelt

fora Retorna uma matriz de objetos [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md) que representam os números de linha desejados.

 pceltFetched

fora Retorna o número de números de linha no enumerador obtido.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não houver mais números de linha. Caso contrário, retornará um código de erro.

## <a name="see-also"></a>Veja também
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)
- [IDiaSession::findLinesByLinenum](../../debugger/debug-interface-access/idiasession-findlinesbylinenum.md)