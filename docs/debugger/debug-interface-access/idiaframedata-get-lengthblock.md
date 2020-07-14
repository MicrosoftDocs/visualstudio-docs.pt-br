---
title: IDiaFrameData::get_lengthBlock | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_lengthBlock method
ms.assetid: 2e54deb7-7744-428e-913c-1d47a2aa89b0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 82f09b454b167fbba9ff267ed4293100162af237
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85467319"
---
# <a name="idiaframedataget_lengthblock"></a>IDiaFrameData::get_lengthBlock
Recupera o comprimento, em bytes, do bloco de código descrito pelo quadro.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_lengthBlock ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna o número de bytes de código no quadro.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não há suporte para essa propriedade. Caso contrário, retornará um código de erro.

## <a name="remarks"></a>Comentários
 O valor retornado por esse método normalmente é usado na interpretação de uma cadeia de caracteres de programa (consulte o método [IDiaFrameData:: get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md) para a definição de uma cadeia de caracteres de programa).

## <a name="see-also"></a>Veja também
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
- [IDiaFrameData::get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md)