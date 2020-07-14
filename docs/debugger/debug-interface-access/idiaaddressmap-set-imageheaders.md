---
title: IDiaAddressMap::set_imageHeaders | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::set_imageHeaders method
ms.assetid: a46b9d0e-43e6-433f-b2c7-aa203981e4e4
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8ded09d64a071c12e14de1597c21aad3872cacf4
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85468542"
---
# <a name="idiaaddressmapset_imageheaders"></a>IDiaAddressMap::set_imageHeaders
Define cabeçalhos de imagem para habilitar a conversão de endereço virtual relativa.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT set_imageHeaders ( 
   DWORD cbData,
   BYTE  data[],
   BOOL  originalHeaders
);
```

#### <a name="parameters"></a>Parâmetros
 cbData

no Número de bytes de dados de cabeçalho. Deve ser `n*sizeof(IMAGE_SECTION_HEADER)` onde `n` é o número de cabeçalhos de seção no executável.

 data[]

no Uma matriz de `IMAGE_SECTION_HEADER` estruturas a ser usada como cabeçalhos de imagem.

 originalHeaders

no Defina como `FALSE` se os cabeçalhos de imagem forem da nova imagem, `TRUE` se eles refletirem a imagem original antes de uma atualização. Normalmente, isso seria definido como `TRUE` somente em combinação com chamadas para o método [IDiaAddressMap:: set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md) .

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 A `IMAGE_SECTION_HEADER` estrutura é declarada em Winnt. h e representa o formato de cabeçalho da seção de imagem do executável.

 Cálculos de endereço virtual relativo dependem dos `IMAGE_SECTION_HEADER` valores. Normalmente, o DIA recupera esses arquivos do banco de dados do programa (. pdb). Se esses valores estiverem ausentes, o DIA não poderá calcular os endereços virtuais relativos e o método [IDiaAddressMap:: get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md) retornará `FALSE` . O cliente deve, então, chamar o método [IDiaAddressMap::p ut_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-relativevirtualaddressenabled.md) para habilitar os cálculos de endereço virtual relativo depois de fornecer os cabeçalhos de imagem ausentes da própria imagem.

## <a name="see-also"></a>Veja também
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)
- [IDiaAddressMap::get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md)
- [IDiaAddressMap::put_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-relativevirtualaddressenabled.md)