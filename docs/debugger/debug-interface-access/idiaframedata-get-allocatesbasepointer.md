---
description: 'IDiaFrameData:: get_allocatesBasePointer recupera um sinalizador que indica se o ponteiro base é alocado para o código nesse intervalo de endereços.'
title: IDiaFrameData::get_allocatesBasePointer | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_allocatesBasePointer method
ms.assetid: 8a33db5d-008c-4fe5-b64f-210c9b77f686
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8fce5e5dbd12be7bae6ba1937b30c8a5d62de3ec
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102157743"
---
# <a name="idiaframedataget_allocatesbasepointer"></a>IDiaFrameData::get_allocatesBasePointer
Recupera um sinalizador que indica se o ponteiro base é alocado para o código neste intervalo de endereços. Esse método é preterido.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_allocatesBasePointer ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna `TRUE` se um ponteiro base é alocado; caso contrário, retorna `FALSE` .

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não há suporte para essa propriedade. Caso contrário, retornará um código de erro.

## <a name="remarks"></a>Comentários
 Essa propriedade deve ser usada somente pelo código que anteriormente acessado FPO_DATA, ou quando a cadeia de caracteres do programa retornada pelo método [IDiaFrameData:: get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md) for `NULL` . Caso contrário, a cadeia de caracteres do programa contém todas as informações necessárias para calcular valores de registro anteriores.

## <a name="see-also"></a>Confira também
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
- [IDiaFrameData::get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md)
