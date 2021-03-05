---
description: Recupera os bytes de dados de um símbolo OEM.
title: IDiaSymbol::get_dataBytes | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_dataBytes method
ms.assetid: 5eb37179-20d8-44ae-a72a-405c1b0435c4
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 09156b8d99daa5cbfd065110073c3c185c3ac0a1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102161012"
---
# <a name="idiasymbolget_databytes"></a>IDiaSymbol::get_dataBytes
Recupera os bytes de dados de um símbolo OEM.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_dataBytes ( 
   DWORD  cbData,
   DWORD* pcbData,
   BYTE   data[]
);
```

#### <a name="parameters"></a>Parâmetros
 `cbData`

no Tamanho do buffer para armazenar os dados.

 `pcbData`

fora Retorna o número de bytes gravados ou, se o `data` parâmetro for `NULL` , retorna o número de bytes disponíveis.

 `data[]`
- [fora,] Um buffer que é preenchido com os bytes de dados.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="requirements"></a>Requisitos

|Requisito|Descrição|
|-----------------|-----------------|
|Cabeçalho:|dia2.h|
|Versão:|DIA SDK v 7.0|

## <a name="see-also"></a>Confira também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
