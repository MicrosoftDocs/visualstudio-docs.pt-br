---
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ef646016433ecfe19106a17dff391c2dd8ce8382
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85467382"
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

## <a name="see-also"></a>Veja também
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)