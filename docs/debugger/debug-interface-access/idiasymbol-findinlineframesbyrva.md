---
description: 'IDiaSymbol:: findInlineFramesByRVA recupera uma enumeração que permite que um cliente Itere em todos os quadros embutidos em um endereço virtual relativo (RVA) específico.'
title: IDiaSymbol::findInlineFramesByRVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: e7a6d9cb-2726-4ac7-9f38-415ad215bf9c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 22ecafb604f31c23f503bbfcbedcd13ee2a42e95
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102156660"
---
# <a name="idiasymbolfindinlineframesbyrva"></a>IDiaSymbol::findInlineFramesByRVA
Recupera uma enumeração que permite que um cliente Itere em todos os quadros embutidos em um endereço virtual relativo (RVA) específico.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT findInlineFramesByRVA (    DWORD             rva,
   IDiaEnumSymbols** ppResult
);
```

#### <a name="parameters"></a>Parâmetros
 `rva`

no Especifica o endereço como um RVA.

 `ppResult`

fora Mantém um `IDiaEnumSymbols` objeto que contém a lista de quadros recuperados.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
