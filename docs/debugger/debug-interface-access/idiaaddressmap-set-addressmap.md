---
title: IDiaAddressMap::set_addressMap | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::set_addressMap method
ms.assetid: 81e82073-089b-43d5-af39-49d7a4907c7a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4af506da822a7f8e38a8952d7c1d0d15fc1995d2
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85468549"
---
# <a name="idiaaddressmapset_addressmap"></a>IDiaAddressMap::set_addressMap
Fornece um mapa de endereços para dar suporte a traduções de layout de imagem.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT set_addressMap ( 
   DWORD                     cbData,
   struct DiaAddressMapEntry data[],
   BOOL                      imagetoSymbols
);
```

#### <a name="parameters"></a>Parâmetros
 `cbData`

no O número de elementos no `data` parâmetro.

 `data[]`

no Uma matriz de estruturas de [estrutura DiaAddressMapEntry](../../debugger/debug-interface-access/diaaddressmapentry.md) que definem o mapa de tradução.

 `imagetoSymbols`

[in] `TRUE` Se o `data` parâmetro definir um mapa do layout da nova imagem para o layout original (conforme descrito pelos símbolos de depuração). `FALSE`Se `data` é um mapa para o novo layout de imagem obtido do layout original.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Normalmente, o DIA recupera mapas de conversão de endereços do arquivo de banco de dados do programa (. pdb). Se esses valores estiverem ausentes, o método [IDiaAddressMap:: set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md) será chamado duas vezes, uma vez com o `imagetoSymbols` parâmetro definido como `TRUE` e com o `imagetoSymbols` parâmetro definido como `FALSE` . As traduções do mapa de endereços não podem ser habilitadas usando o método [IDiaAddressMap::p ut_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-addressmapenabled.md) , a menos que ambos os mapas de tradução sejam fornecidos.

## <a name="see-also"></a>Veja também
- [Estrutura DiaAddressMapEntry](../../debugger/debug-interface-access/diaaddressmapentry.md)
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaAddressMap::put_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-addressmapenabled.md)
- [IDiaAddressMap::set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)