---
title: IDiaFrameData::get_type | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_type method
ms.assetid: efca38b5-c479-4d0a-a164-f903f25c5509
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2526fd4991677eca60b908d6ab1f4b3e6e8189af
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85467193"
---
# <a name="idiaframedataget_type"></a>IDiaFrameData::get_type
Recupera o tipo de quadro específico do compilador.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_type ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna um valor da enumeração de [Enumeração StackFrameTypeEnum](../../debugger/debug-interface-access/stackframetypeenum.md) que indica o tipo de quadro específico do compilador.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não há suporte para essa propriedade. Caso contrário, retornará um código de erro.

## <a name="see-also"></a>Veja também
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
- [Enumeração StackFrameTypeEnum](../../debugger/debug-interface-access/stackframetypeenum.md)