---
title: IDiaFrameData::get_functionStart | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_functionStart method
ms.assetid: 49fd24fb-65c2-4812-8303-56a968353e1b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1e4ee5de3c27d1ba16aed25c59555880901c010b
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85467368"
---
# <a name="idiaframedataget_functionstart"></a>IDiaFrameData::get_functionStart
Recupera um sinalizador que indica se o bloco contém o ponto de entrada de uma função.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_functionStart ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna `TRUE` se o bloco contém o ponto de entrada; caso contrário, retorna `FALSE` .

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não há suporte para essa propriedade. Caso contrário, retornará um código de erro.

## <a name="remarks"></a>Comentários
 É possível que um registro de ativação não seja o início de uma função porque o quadro representa um método embutido ou função inserida em uma função.

## <a name="see-also"></a>Veja também
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)