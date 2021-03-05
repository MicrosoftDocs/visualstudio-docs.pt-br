---
description: Recupera uma matriz de valores de identificador de tipo específicos do compilador para este símbolo.
title: IDiaSymbol::get_typeIds | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_typeIds method
ms.assetid: 5166e647-fde5-4efe-92bf-77f8ae3fbc9b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 04a39af21ebb8a409656bd8b8ae0b4323da33c60
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102155610"
---
# <a name="idiasymbolget_typeids"></a>IDiaSymbol::get_typeIds
Recupera uma matriz de valores de identificador de tipo específicos do compilador para este símbolo.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_typeIds ( 
   DWORD  cTypeIds,
   DWORD* pcTypeIds,
   DWORD  typeIds[]
);
```

#### <a name="parameters"></a>Parâmetros
 `cTypeIds`

no Tamanho do buffer para armazenar os dados.

 `pcTypeIds`

fora Retorna o número de `typeIds` gravados ou, se `typeIds` for `NULL` , o número total de identificadores de tipo disponíveis.

 `typeIds[]`

fora Uma matriz que deve ser preenchida com os identificadores de tipo.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno de `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="see-also"></a>Confira também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
