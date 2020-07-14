---
title: IDiaEnumLineNumbers::Item | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumLineNumbers::Item method
ms.assetid: 08efbeaf-22f7-49e9-96a8-bb906dfe4fd8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f1eae34788cfed9f509e979df8efae6657f330d5
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85468213"
---
# <a name="idiaenumlinenumbersitem"></a>IDiaEnumLineNumbers::Item
Recupera um número de linha por meio de um índice.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT Item ( 
   DWORD            index,
   IDiaLineNumber** lineNumber
);
```

#### <a name="parameters"></a>Parâmetros
 índice

no Índice do objeto [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md) a ser recuperado. O índice está no intervalo de 0 a `count` -1, em que `count` é retornado pelo método [IDiaEnumLineNumbers:: get_Count](../../debugger/debug-interface-access/idiaenumlinenumbers-get-count.md) .

 lineNumber

fora Retorna um objeto [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md) que representa o número de linha desejado.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Veja também
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)