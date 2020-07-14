---
title: IDiaLoadCallback::NotifyOpenDBG | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback::NotifyOpenDBG method
ms.assetid: dbc4dcf0-4ace-4dce-9790-0fdaf3a23d3b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0d4572df216e04e645cae92bf479d17166edc256
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85466745"
---
# <a name="idialoadcallbacknotifyopendbg"></a>IDiaLoadCallback::NotifyOpenDBG
Chamado quando um arquivo Candidate. dbg é aberto.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT NotifyOpenDBG ( 
   LPCOLESTR dbgPath,
   HRESULT   resultCode
);
```

#### <a name="parameters"></a>Parâmetros
 `dbgPath`

no O caminho completo do arquivo. dbg.

 `resultCode`

no Código que indica o êxito ( `S_OK` ) ou a falha da carga, conforme aplicado a esse arquivo.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro. O código de retorno é normalmente ignorado.

## <a name="see-also"></a>Veja também
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)