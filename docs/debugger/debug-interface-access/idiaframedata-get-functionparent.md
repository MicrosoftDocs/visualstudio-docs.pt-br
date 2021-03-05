---
description: Recupera uma interface de dados de quadro para a função de circunscrição.
title: IDiaFrameData::get_functionParent | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_functionParent method
ms.assetid: f00b9ab1-d4da-4818-973a-58f8f0e66769
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c03eb86e7575652fd260aa9a7018081992b78010
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102157738"
---
# <a name="idiaframedataget_functionparent"></a>IDiaFrameData::get_functionParent
Recupera uma interface de dados de quadro para a função de circunscrição.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_functionParent ( 
   IDiaFrameData** pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna um objeto [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md) para a função de circunscrição.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
