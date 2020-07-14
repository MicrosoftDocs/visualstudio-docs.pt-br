---
title: IDiaLoadCallback2::RestrictReferencePathAccess | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback2::RestrictReferencePathAccess method
ms.assetid: e20cb45c-0360-4ff0-a92c-b1b6f76d6e85
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 32cad25220cc2248039e4b64c158092ffee8431f
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85466626"
---
# <a name="idialoadcallback2restrictreferencepathaccess"></a>IDiaLoadCallback2::RestrictReferencePathAccess
Determina se é permitido procurar um arquivo. pdb no caminho em que o arquivo. exe está localizado.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT RestrictReferencePathAccess();
```

## <a name="return-value"></a>Valor retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Qualquer código de retorno diferente de `S_OK` para evitar a procura de um arquivo. pdb no caminho em que o arquivo. exe está localizado.

## <a name="see-also"></a>Veja também
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)