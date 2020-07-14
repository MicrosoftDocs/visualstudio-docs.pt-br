---
title: IDiaLoadCallback::NotifyOpenPDB | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback::NotifyOpenPDB method
ms.assetid: c0547f99-8468-4e57-82ca-9ef7d6707c8a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 468aef9faf4aa6c7c1b7ddebb1fd0c15445d61a2
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85466738"
---
# <a name="idialoadcallbacknotifyopenpdb"></a>IDiaLoadCallback::NotifyOpenPDB
Chamado quando um arquivo Candidate. pdb é aberto.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT NotifyOpenPDB ( 
   LPCOLESTR pdbPath,
   HRESULT   resultCode
);
```

#### <a name="parameters"></a>Parâmetros
 `pdbPath`

no O caminho completo do arquivo. pdb.

 `resultCode`

no Código que indica o êxito ( `S_OK` ) ou a falha da carga, conforme aplicado a esse arquivo.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro. O código de retorno é normalmente ignorado.

## <a name="see-also"></a>Veja também
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)