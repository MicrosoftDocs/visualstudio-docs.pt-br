---
title: 'Idiastackframe:: Get_maxstack | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_maxStack method
ms.assetid: 6352e972-7105-4d0e-aeba-b8fc16d62dec
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f7e860830b5169a71d7757e1ee39b223559456de
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62575990"
---
# <a name="idiastackframegetmaxstack"></a>IDiaStackFrame::get_maxStack
Recupera o número máximo de bytes enviados por push na pilha do quadro.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_maxStack ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

[out] Retorna o número máximo de bytes enviados por push na pilha.

## <a name="return-value"></a>Valor de retorno
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não há suporte para a propriedade. Caso contrário, retornará um código de erro.

## <a name="see-also"></a>Consulte também
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)