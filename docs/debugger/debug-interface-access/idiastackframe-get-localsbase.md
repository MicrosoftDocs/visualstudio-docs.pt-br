---
title: IDiaStackFrame::get_localsBase | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_localsBase method
ms.assetid: eb0bd73e-d92d-468e-a0b1-fbc279919f54
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7f7c3f442ba814e2f59f33ea0ad837cec472e511
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85465027"
---
# <a name="idiastackframeget_localsbase"></a>IDiaStackFrame::get_localsBase
Recupera o endereço base das variáveis locais para o quadro.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_localsBase ( 
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna o endereço base das variáveis locais.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se a propriedade não tem suporte. Caso contrário, retornará um código de erro.

## <a name="see-also"></a>Veja também
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)