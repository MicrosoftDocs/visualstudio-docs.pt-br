---
title: IDiaSymbol::get_liveRangeStartAddressSection | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_liveRangeStartAddressSection
ms.assetid: 892b80ff-5957-4233-b4d7-6144167be289
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 05355c9031aa588c8e9ed4ddceb69920fa485f51
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99863000"
---
# <a name="idiasymbolget_liverangestartaddresssection"></a>IDiaSymbol::get_liveRangeStartAddressSection
Retorna a parte da seção do endereço inicial do intervalo no qual o símbolo local é válido.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_liveRangeStartAddressSection ( 
   DWORD* section
);
```

#### <a name="parameters"></a>Parâmetros
 `section`

fora Retorna a parte da seção do intervalo de endereços inicial.

## <a name="return-value"></a>Valor retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

> [!NOTE]
> Um código de erro retornado significa que o símbolo não tem informações de intervalo dinâmico.

## <a name="remarks"></a>Comentários
 O endereço formado pela seção e deslocamento é o início do intervalo no qual o símbolo é válido.

 Para obter a parte de deslocamento do endereço, use [IDiaSymbol:: get_liveRangeStartAddressOffset](../../debugger/debug-interface-access/idiasymbol-get-liverangestartaddressoffset.md).

## <a name="requirements"></a>Requisitos
 Cabeçalho: dia2. h

 Biblioteca: diaguids. lib

 DLL: msdia100.dll

## <a name="see-also"></a>Consulte também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)