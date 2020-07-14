---
title: IDiaSymbol::findSymbolsByRVAForAcceleratorPointerTag | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 024ccd78-5867-4ca7-bc26-548758e9ac53
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: de63223afda4ce5d00358fe3c06cabe90f2689aa
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85464432"
---
# <a name="idiasymbolfindsymbolsbyrvaforacceleratorpointertag"></a>IDiaSymbol::findSymbolsByRVAForAcceleratorPointerTag
Dado um valor de marca correspondente, esse método retorna uma enumeração de símbolos que estão contidos nessa função de stub em um endereço virtual relativo especificado.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT findSymbolsByRVAForAcceleratorPointerTag (
   DWORD             tagValue,
   DWORD             rva,
   IDiaEnumSymbols** ppResult);
```

#### <a name="parameters"></a>Parâmetros
 `tagValue`

no O valor da marca do ponteiro para o qual os registros de símbolo do ponto são encontrados.

 `rva`

no O RVA usado para filtrar os símbolos que correspondem à variável de ponto com o valor de marca especificado.

 `ppResult`

fora Um ponteiro para um `IDiaEnumSymbols` ponteiro de interface que é inicializado com o resultado.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

## <a name="remarks"></a>Comentários
 Chame esse método somente em uma `IDiaSymbol` interface que corresponda a uma função de stub de acelerador.

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)