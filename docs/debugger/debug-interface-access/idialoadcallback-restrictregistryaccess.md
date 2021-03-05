---
description: Determina se as consultas do registro podem ser usadas para localizar caminhos de pesquisa de símbolos.
title: IDiaLoadCallback::RestrictRegistryAccess | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback::RestrictRegistryAccess method
ms.assetid: de4760c3-a746-4bab-8065-1388fed31b67
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 5b94821dc2ebf3a3af6b6b560d972c8376e56e6a
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102157457"
---
# <a name="idialoadcallbackrestrictregistryaccess"></a>IDiaLoadCallback::RestrictRegistryAccess
Determina se as consultas do registro podem ser usadas para localizar caminhos de pesquisa de símbolos.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT RestrictRegistryAccess();
```

## <a name="return-value"></a>Valor retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Qualquer código de retorno diferente de `S_OK` impede a consulta do registro em busca de caminhos de pesquisa de símbolo.

## <a name="see-also"></a>Confira também
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)
