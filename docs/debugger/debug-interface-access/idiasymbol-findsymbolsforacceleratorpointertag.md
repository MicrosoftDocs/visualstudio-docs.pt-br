---
description: Retorna o número de marcas do ponteiro do acelerador em uma C++ AMP função de stub.
title: IDiaSymbol::findSymbolsForAcceleratorPointerTag | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: fb66852c-c5f7-4140-b9fe-20cb4e51a9fe
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a8dcdae4c430a07114f37e39bef2ce685c19ba15
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102156611"
---
# <a name="idiasymbolfindsymbolsforacceleratorpointertag"></a>IDiaSymbol::findSymbolsForAcceleratorPointerTag
Retorna o número de marcas do ponteiro do acelerador em uma C++ AMP função de stub.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT findSymbolsForAccleratorPointerTag (
   DWORD             tagValue,
   IDiaEnumSymbols** ppResult);
```

#### <a name="parameters"></a>Parâmetros
 `tagValue`

no O valor da marca do ponteiro para o qual os registros de símbolo do ponto são encontrados.

 `ppResult`

fora Um ponteiro para um `IDiaEnumSymbols` ponteiro de interface que é inicializado com o resultado.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

## <a name="see-also"></a>Confira também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
