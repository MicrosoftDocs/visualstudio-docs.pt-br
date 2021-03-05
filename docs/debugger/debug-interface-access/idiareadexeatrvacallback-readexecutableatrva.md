---
description: Lê o número especificado de bytes começando no endereço virtual relativo (RVA) especificado do arquivo executável.
title: IDiaReadExeAtRVACallback::ReadExecutableAtRVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaReadExeAtRVACallback::ReadExecutableAtRVA method
ms.assetid: 3c1e965f-8f05-41a8-86d8-01830b2377c9
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4c3d51ce1d2a54583df41fb4c6dd17dcfd679ad1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102157325"
---
# <a name="idiareadexeatrvacallbackreadexecutableatrva"></a>IDiaReadExeAtRVACallback::ReadExecutableAtRVA
Lê o número especificado de bytes começando no endereço virtual relativo (RVA) especificado do arquivo executável.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT ReadExecutableAtRVA ( 
   DWORD  relativeVirtualAddress,
   DWORD  cbData,
   DWORD* pcbData,
   BYTE   data[]
);
```

#### <a name="parameters"></a>Parâmetros
 `relativeVirtualAddress`

no O RVA no arquivo executável para começar a ler.

 `cbData`

no Número de bytes a serem lidos.

 `pcbData`

fora Retorna o número de bytes lidos.

 `data[]`

[entrada, saída] Uma matriz que é preenchida com bytes lidos do arquivo.

## <a name="remarks"></a>Comentários
 Esse método é chamado pelo código de suporte do DIA para carregar bytes de dados de um executável usando um endereço virtual relativo. Esse método é chamado no suporte do método [IDiaDataSource:: loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) .

## <a name="see-also"></a>Confira também
- [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
