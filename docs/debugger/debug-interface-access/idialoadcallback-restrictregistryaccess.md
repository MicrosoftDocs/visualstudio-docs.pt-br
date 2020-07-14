---
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 18436d28fbee7ba12cea2398eb1fa6abbd8ac23b
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85466731"
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

## <a name="see-also"></a>Veja também
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)