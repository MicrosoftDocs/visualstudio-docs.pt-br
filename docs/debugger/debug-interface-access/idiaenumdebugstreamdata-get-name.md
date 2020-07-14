---
title: IDiaEnumDebugStreamData::get_name | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreamData::get_Name method
ms.assetid: e6cf2bed-ee2b-4122-886d-c20d93df7ff2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 37cd52af7326454b0b684ad97f9cde088a8a5679
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85468465"
---
# <a name="idiaenumdebugstreamdataget_name"></a>IDiaEnumDebugStreamData::get_name
Recupera o nome de um fluxo de dados de depuração.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_Name ( 
   BSTR * pRetVal
)
```

#### <a name="parameters"></a>Parâmetros
 pRetVal

fora Retorna o nome de um fluxo de dados de depuração.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Veja também
- [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)