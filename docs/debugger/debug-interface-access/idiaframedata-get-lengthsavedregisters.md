---
title: IDiaFrameData::get_lengthSavedRegisters | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_lengthSavedRegisters method
ms.assetid: dfda4e91-9bfa-4b9d-9133-b73015bfa4d5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a3ebe80840ca2b243b789496f61919da1bf17ef0
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85467298"
---
# <a name="idiaframedataget_lengthsavedregisters"></a>IDiaFrameData::get_lengthSavedRegisters
Recupera o número de bytes de registros salvos enviados por push na pilha.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_lengthSavedRegisters ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna o número de bytes de registros salvos.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não há suporte para essa propriedade. Caso contrário, retornará um código de erro.

## <a name="remarks"></a>Comentários
 O valor retornado por esse método normalmente é usado na interpretação de uma cadeia de caracteres de programa (consulte o método [IDiaFrameData:: get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md) para a definição de uma cadeia de caracteres de programa).

## <a name="see-also"></a>Veja também
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
- [IDiaFrameData::get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md)