---
description: Chamado quando um arquivo Candidate. pdb é aberto.
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ab1f72c6f22f70bb94262c57327ab91f96a02183
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102148293"
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

## <a name="see-also"></a>Confira também
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)
