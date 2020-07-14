---
title: IDiaSession::getEnumDebugStreams | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::getEnumDebugStreams method
ms.assetid: d294954b-80e9-476c-b9f0-5ca6fd575f68
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 62088c1ff7dd3dea8016a18d7c41425fdd584661
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85465435"
---
# <a name="idiasessiongetenumdebugstreams"></a>IDiaSession::getEnumDebugStreams
Recupera uma sequência enumerada de fluxos de dados de depuração.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT getEnumDebugStreams ( 
   IDiaEnumDebugStreams** ppEnumDebugStreams
)
```

#### <a name="parameters"></a>Parâmetros
 `ppEnumDebugStreams`

fora Retorna um objeto [IDiaEnumDebugStreams](../../debugger/debug-interface-access/idiaenumdebugstreams.md) que contém uma lista de fluxos de depuração.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Veja também
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaEnumDebugStreams](../../debugger/debug-interface-access/idiaenumdebugstreams.md)