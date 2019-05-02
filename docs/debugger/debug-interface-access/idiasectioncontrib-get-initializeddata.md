---
title: IDiaSectionContrib::get_initializedData | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_initializedData method
ms.assetid: f5c108be-a0cc-408b-9590-b8d44361810c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ef878dcae9f8d6d29761bcda5f5aa9588f26d66c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62828161"
---
# <a name="idiasectioncontribgetinitializeddata"></a>IDiaSectionContrib::get_initializedData
Recupera um sinalizador que indica se a seção contém dados inicializados.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_initializedData ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

[out] Retorna `TRUE` se a seção contém dados inicializados; caso contrário, retornará `FALSE`.

## <a name="return-value"></a>Valor de retorno
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não há suporte para essa propriedade. Caso contrário, retornará um código de erro.

## <a name="see-also"></a>Consulte também
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)