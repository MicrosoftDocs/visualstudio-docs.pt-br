---
title: IDiaSectionContrib::get_informational | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_informational method
ms.assetid: 5351e89f-7db1-4f8e-9e57-2dd1c74002e0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d804ef0caa2f6fed3ef33e64f97e51fd81e466ec
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85466248"
---
# <a name="idiasectioncontribget_informational"></a>IDiaSectionContrib::get_informational
Recupera um sinalizador que indica se uma seção contém comentários ou informações semelhantes.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_informational(
   BOOL* pRetVal
};
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna `TRUE` se a seção contém comentários ou outras informações; caso contrário, retorna `FALSE` .

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não há suporte para essa propriedade. Caso contrário, retornará um código de erro.

## <a name="remarks"></a>Comentários
 Normalmente, a seção. diretivo contém informações.

## <a name="see-also"></a>Veja também
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)