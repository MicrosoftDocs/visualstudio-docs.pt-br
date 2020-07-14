---
title: IDiaAddressMap::get_imageAlign | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::get_imageAlign method
ms.assetid: f1ba8071-669c-4cf7-9ac0-02f26d99f366
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 814381cb4792d9c21825ab1be5ebc4da415bc974
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85468584"
---
# <a name="idiaaddressmapget_imagealign"></a>IDiaAddressMap::get_imageAlign
Recupera o alinhamento da imagem atual.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_imageAlign ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna o valor de alinhamento da imagem do executável.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 As imagens são alinhadas a limites de memória específicos, dependendo de como a imagem foi carregada e criada. O alinhamento é normalmente em limites de 1, 2, 4, 8, 16, 32 ou 64 bytes. O alinhamento da imagem pode ser definido com uma chamada para o método [IDiaAddressMap::p ut_imageAlign](../../debugger/debug-interface-access/idiaaddressmap-put-imagealign.md) .

## <a name="see-also"></a>Veja também
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaAddressMap::put_imageAlign](../../debugger/debug-interface-access/idiaaddressmap-put-imagealign.md)