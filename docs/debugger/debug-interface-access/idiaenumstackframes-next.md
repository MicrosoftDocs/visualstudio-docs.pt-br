---
description: Recupera um número especificado de elementos de quadro de pilha da sequência de enumeração.
title: IDiaEnumStackFrames::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumStackFrames::Next method
ms.assetid: 09378a21-d5e3-4213-b7e2-10f04d85295f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0cee13aa9e26de77cf22cf7a51011a567cb14c25
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102159156"
---
# <a name="idiaenumstackframesnext"></a>IDiaEnumStackFrames::Next
Recupera um número especificado de elementos de quadro de pilha da sequência de enumeração.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT Next( 
   ULONG             celt,
   IDiaStackFrame**  rgelt,
   ULONG*            pceltFetched
);
```

#### <a name="parameters"></a>Parâmetros
 celt

no O número de elementos StackFrame no enumerador a ser recuperado.

 rgelt

fora Uma matriz que deve ser preenchida com os objetos [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md) solicitados.

 pceltFetched

fora Retorna o número de elementos de quadro de pilha no enumerador obtido.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não houver mais quadros de pilha. Caso contrário, retornará um código de erro.

## <a name="see-also"></a>Confira também
- [IDiaEnumStackFrames](../../debugger/debug-interface-access/idiaenumstackframes.md)
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)
