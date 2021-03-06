---
description: Recupera um sinalizador que indica se a seção não deve ser preenchida para o próximo limite de memória.
title: IDiaSectionContrib::get_nopad | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_nopad method
ms.assetid: f5c08603-0b3e-4e81-acf1-1b95a6a83bed
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 48bbfdbd14cd7f2d00a9c0ba4530c78fed62141d
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102157206"
---
# <a name="idiasectioncontribget_nopad"></a>IDiaSectionContrib::get_nopad
Recupera um sinalizador que indica se a seção não deve ser preenchida para o próximo limite de memória.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_nopad(
   BOOL* pRetVal
};
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna `TRUE` se a seção não deve ser preenchida para o próximo limite de memória; caso contrário, retorna `FALSE` .

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não há suporte para essa propriedade. Caso contrário, retornará um código de erro.

## <a name="remarks"></a>Comentários
 Essa é uma propriedade normalmente vista apenas em arquivos mais antigos.

## <a name="see-also"></a>Confira também
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
