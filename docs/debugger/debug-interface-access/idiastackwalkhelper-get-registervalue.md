---
description: 'IDiaStackWalkHelper:: get_registerValue recupera o valor de um registro.'
title: IDiaStackWalkHelper::get_registerValue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2::get_registerValue method
ms.assetid: 46ac5eee-73a3-44a1-8635-6c58ba193cb6
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fa87529f90b20d7d9099dd76e294e406ae0c7a08
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102161176"
---
# <a name="idiastackwalkhelperget_registervalue"></a>IDiaStackWalkHelper::get_registerValue
Recupera o valor de um registro.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_registerValue ( 
   DWORD      index,
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `index`

no Um valor da enumeração de [enumeração de CV_HREG_e](../../debugger/debug-interface-access/cv-hreg-e.md) especificando para qual registro obter o valor.

 `pRetVal`

fora Retorna o valor atual do registro.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Apesar do tamanho do `pRetVal` parâmetro, uma implementação deve armazenar apenas o que o registro normalmente mantém. Por exemplo, um registro de 8 bits mantém apenas os 8 bits mais baixos do valor especificado. Esse valor de 8 bits é expandido para 64 bits quando retornado desse método.

## <a name="see-also"></a>Confira também
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [Enumeração CV_HREG_e](../../debugger/debug-interface-access/cv-hreg-e.md)
