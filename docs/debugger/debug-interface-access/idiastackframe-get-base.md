---
title: 'IDiaStackFrame:: get_base | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_base method
ms.assetid: f27477d7-26fe-4c1c-a08a-c52cb20c8293
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 26717fc229bcd167bb344db6a82d81902de1d890
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85465111"
---
# <a name="idiastackframeget_base"></a>IDiaStackFrame::get_base
Recupera o endereço base do quadro.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_base ( 
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna o endereço base.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se a propriedade não tem suporte. Caso contrário, retornará um código de erro.

## <a name="see-also"></a>Veja também
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)