---
title: IDiaEnumDebugStreamData::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreamData::Next method
ms.assetid: 114171dd-38fd-4bd7-a702-8ff887ffc99b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 117d16a9c010bbed2c14544f6cc94c4782701e34
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85468444"
---
# <a name="idiaenumdebugstreamdatanext"></a>IDiaEnumDebugStreamData::Next
Recupera um número especificado de registros na sequência enumerada.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT Next ( 
   ULONG  celt,
   DWORD  cbData,
   DWORD* pcbData,
   BYTE   data[],
   ULONG* pceltFetched
);
```

#### <a name="parameters"></a>Parâmetros
 celt

no O número de registros a serem recuperados.

 cbData

no Tamanho do buffer de dados, em bytes.

 pcbData

fora Retorna o número de bytes retornados. Se `data` for NULL, `pcbData` conterá o número total de bytes de dados disponíveis para todos os registros solicitados.

 data[]

fora Um buffer que deve ser preenchido com os dados de registro do fluxo de depuração.

 pceltFetched

[entrada, saída] Retorna o número de registros em `data` .

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não houver mais registros. Caso contrário, retornará um código de erro.

## <a name="see-also"></a>Veja também
- [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)
- [IDiaEnumDebugStreams::Next](../../debugger/debug-interface-access/idiaenumdebugstreams-next.md)