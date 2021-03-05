---
description: Recupera o endereço de retorno do quadro.
title: 'IDiaStackFrame:: get_returnAddress | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_returnAddress method
ms.assetid: 0df91981-919f-48ed-9c70-4121567d645b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c8a491f2b76457479f765c4387571d2524d26a78
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102161183"
---
# <a name="idiastackframeget_returnaddress"></a>IDiaStackFrame::get_returnAddress
Recupera o endereço de retorno do quadro.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_returnAddress ( 
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna o endereço de retorno do quadro.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se a propriedade não tem suporte. Caso contrário, retornará um código de erro.

## <a name="see-also"></a>Confira também
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)
