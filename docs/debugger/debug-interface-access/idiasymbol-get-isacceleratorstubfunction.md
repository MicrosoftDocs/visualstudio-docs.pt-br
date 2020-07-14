---
title: IDiaSymbol::get_isAcceleratorStubFunction | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: cc4ea375-76f6-4ba8-baed-c5fa82108137
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: dcc8128ec5c9693b399c08a134326b1f6d135d1b
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85463487"
---
# <a name="idiasymbolget_isacceleratorstubfunction"></a>IDiaSymbol::get_isAcceleratorStubFunction
Indica se o símbolo corresponde a um símbolo de função de nível superior para um sombreador compilado para um acelerador que corresponde a uma `parallel_for_each` chamada.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_isAcceleratorStubFunction(
   BOOL* pFlag);
```

#### <a name="parameters"></a>Parâmetros
 `pFlag`

fora Um ponteiro para um `BOOL` que indica se o símbolo corresponde a um símbolo de função de nível superior para um sombreador compilado para um acelerador que corresponde a uma `parallel_for_each` chamada.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)