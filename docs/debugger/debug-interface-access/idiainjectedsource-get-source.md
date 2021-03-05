---
description: Recupera os bytes do código-fonte.
title: IDiaInjectedSource::get_source | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaInjectedSource::get_source method
ms.assetid: 3c0b5386-321f-4f8f-85cc-e2ee7b4cc3d2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 248fc00320f94b297a9b0697742dff6e3fbd2004
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102148412"
---
# <a name="idiainjectedsourceget_source"></a>IDiaInjectedSource::get_source
Recupera os bytes do código-fonte.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_source ( 
   DWORD  cbData,
   DWORD* pcbData,
   BYTE   data[]
);
```

#### <a name="parameters"></a>Parâmetros
 `cbData`

no O número de bytes que representa o tamanho do buffer de dados.

 `pcbData`

fora Retorna o número de bytes que representa os bytes retornados. Se `data` for `NULL` , `pcbData` será o número total de bytes de dados disponíveis.

 `data[]`

fora Um buffer que deve ser preenchido com os bytes de origem.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não há suporte para essa propriedade. Caso contrário, retornará um código de erro.

## <a name="see-also"></a>Confira também
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)
