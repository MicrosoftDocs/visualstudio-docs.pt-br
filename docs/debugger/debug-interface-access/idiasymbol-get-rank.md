---
description: Recupera a classificação (número de dimensões) de uma matriz multidimensional FORTRAN.
title: IDiaSymbol::get_rank | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_rank method
ms.assetid: 14cc9c4b-a5ec-414a-b01f-4a142c17b7cc
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4da2bb7dc41d06e113e0bd278ef08917771cfb2e
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102161910"
---
# <a name="idiasymbolget_rank"></a>IDiaSymbol::get_rank
Recupera a classificação (número de dimensões) de uma matriz multidimensional FORTRAN.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_rank ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna o número de dimensões em uma matriz multidimensional FORTRAN.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno de `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="remarks"></a>Comentários
 Rank refere-se ao número de dimensões em uma matriz em que a matriz é declarada como `myarray[1,2,3]` . Este exemplo tem uma classificação de 3 e 3 dimensões. A classificação não se aplica ao C++ que usa o conceito de uma matriz de matrizes para cada dimensão (ou seja, `myarray[1][2][3]` ).

## <a name="see-also"></a>Confira também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
