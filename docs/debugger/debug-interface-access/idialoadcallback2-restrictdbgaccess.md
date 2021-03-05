---
description: Determina se procurar informações de depuração é permitida a partir de arquivos. dbg.
title: IDiaLoadCallback2::RestrictDBGAccess | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback2::RestrictDBGAccess method
ms.assetid: 63b67a93-2910-4fff-aa70-6b2eaa08e5c8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 529d617b833a6dc3013a71f5c132ca5654c89d08
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102148265"
---
# <a name="idialoadcallback2restrictdbgaccess"></a>IDiaLoadCallback2::RestrictDBGAccess
Determina se procurar informações de depuração é permitida a partir de arquivos. dbg.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT RestrictDBGAccess();
```

## <a name="return-value"></a>Valor retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Qualquer valor de retorno diferente de `S_OK` para evitar a procura de informações de depuração de arquivos. dbg.

## <a name="see-also"></a>Confira também
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)
