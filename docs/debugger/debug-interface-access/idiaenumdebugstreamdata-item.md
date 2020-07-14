---
title: IDiaEnumDebugStreamData::Item | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreamData::Item method
ms.assetid: 761e61a5-44a6-4d5d-a98e-c2e9b89d2343
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4696d8fdab9720796db1c6b5dff25b7bcfe49e01
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85468451"
---
# <a name="idiaenumdebugstreamdataitem"></a>IDiaEnumDebugStreamData::Item
Recupera o registro especificado.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT Item ( 
   DWORD  index,
   DWORD  cbData,
   DWORD* pcbData,
   BYTE   data[]
);
```

#### <a name="parameters"></a>Parâmetros
 índice

no Índice do registro a ser recuperado. O índice está no intervalo de 0 a `count` -1, em que `count` é retornado por [IDiaEnumDebugStreamData:: get_Count](../../debugger/debug-interface-access/idiaenumdebugstreamdata-get-count.md).

 cbData

no Tamanho do buffer de dados, em bytes.

 pcbData

fora Retorna o número de bytes retornados. Se `data` for `NULL` , `pcbData` conterá o número total de bytes de dados disponíveis no registro especificado.

 data[]

fora Um buffer que é preenchido com os dados de registro do fluxo de depuração.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro. Retorna `E_INVALIDARG` para parâmetros inválidos e se o `index` parâmetro está fora dos limites.

## <a name="see-also"></a>Veja também
- [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)
- [IDiaEnumDebugStreamData::Next](../../debugger/debug-interface-access/idiaenumdebugstreamdata-next.md)
- [IDiaEnumDebugStreams::Item](../../debugger/debug-interface-access/idiaenumdebugstreams-item.md)
- [IDiaEnumDebugStreamData::get_Count](../../debugger/debug-interface-access/idiaenumdebugstreamdata-get-count.md)
- [IDiaEnumDebugStreamData::Skip](../../debugger/debug-interface-access/idiaenumdebugstreamdata-skip.md)