---
description: Ignora um número especificado de contribuições de seção em uma sequência de enumeração.
title: IDiaEnumSectionContribs::Skip | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSectionContribs::Skip method
ms.assetid: 7471a178-5134-41b2-80a6-51ff96abe916
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 345aa9219071a64fdd497a9e5409ee7dab3068ad
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102159296"
---
# <a name="idiaenumsectioncontribsskip"></a>IDiaEnumSectionContribs::Skip
Ignora um número especificado de contribuições de seção em uma sequência de enumeração.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT Skip( 
   ULONG celt
);
```

#### <a name="parameters"></a>Parâmetros
 `celt`

no O número de contribuições de seção na sequência de enumeração a serem ignoradas.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK` ; caso contrário, retornará `S_FALSE` se não houver mais contribuições de seção a serem ignoradas.

## <a name="see-also"></a>Confira também
- [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)
