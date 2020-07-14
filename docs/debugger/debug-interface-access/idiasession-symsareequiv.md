---
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fe609d53571e6ffcd8e18919f0351e29c0329b46
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85465359"
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

## <a name="see-also"></a>Veja também
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)