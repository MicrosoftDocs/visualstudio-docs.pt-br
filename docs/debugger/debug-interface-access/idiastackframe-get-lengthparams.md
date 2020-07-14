---
title: 'IDiaStackFrame:: get_lengthParams | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_lengthParams method
ms.assetid: 78005efa-2883-4823-b4e4-711a66672c78
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b454c90e67573a248f9359b25968866d7383e072
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85465083"
---
# <a name="idiastackframeget_lengthparams"></a>IDiaStackFrame::get_lengthParams
Recupera o número de bytes de parâmetros enviados por push na pilha.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_lengthParams ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna o número de bytes de parâmetros.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se a propriedade não tem suporte. Caso contrário, retornará um código de erro.

## <a name="see-also"></a>Veja também
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)