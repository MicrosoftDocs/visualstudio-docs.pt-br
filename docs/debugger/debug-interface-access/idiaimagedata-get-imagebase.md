---
description: Recupera o local da memória onde a imagem deve ser baseada.
title: IDiaImageData::get_imageBase | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaImageData::get_imageBase method
ms.assetid: 4ba3d9e4-b205-4ee6-a41d-6996972f1f85
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 82f80f95689a176118d5be6dcc5cfe4fdb903e0f
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102148447"
---
# <a name="idiaimagedataget_imagebase"></a>IDiaImageData::get_imageBase
Recupera o local da memória onde a imagem deve ser baseada.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_imageBase ( 
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna o valor base da imagem sugerida.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Devido a conflitos na base da imagem, uma imagem pode ser reutilizada automaticamente para um local de memória não utilizado quando ela é carregada. Esse método retorna a dica de base (local da memória sugerida) que foi armazenada no módulo no momento da compilação.

## <a name="see-also"></a>Confira também
- [IDiaImageData](../../debugger/debug-interface-access/idiaimagedata.md)
