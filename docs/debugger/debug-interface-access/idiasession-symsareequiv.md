---
description: Verifica se dois símbolos são equivalentes.
title: IDiaSession::symsAreEquiv | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::symsAreEquiv method
ms.assetid: 9941d520-e203-46c0-83c3-b3a967f4fc59
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c5f887b13195bdde133c4bca845291b1255b99ea
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102156982"
---
# <a name="idiasessionsymsareequiv"></a>IDiaSession::symsAreEquiv
Verifica se dois símbolos são equivalentes.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT symsAreEquiv ( 
   IDiaSymbol* symbolA,
   IDiaSymbol* symbolB
);
```

#### <a name="parameters"></a>Parâmetros
 `symbolA`

no O primeiro objeto [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) usado na comparação.

 `symbolB`

no O segundo `IDiaSymbol` objeto usado na comparação.

## <a name="return-value"></a>Valor Retornado
 Se os símbolos forem equivalentes, retorna `S_OK` ; caso contrário, retorna `S_FALSE` , os símbolos não são equivalentes. Caso contrário, retorne um código de erro.

## <a name="see-also"></a>Confira também
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
