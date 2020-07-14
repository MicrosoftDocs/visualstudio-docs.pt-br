---
title: 'IDiaSymbol:: get_acceleratorPointerTags | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 30e13cee-e511-49ec-affd-99b0097071b2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e2da182992999a582ea30f570734b366178a9521
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85464404"
---
# <a name="idiasymbolget_acceleratorpointertags"></a>IDiaSymbol::get_acceleratorPointerTags
Retorna todos os valores de marca do ponteiro de aceleração que correspondem a uma função de stub de C++ AMP Accelerator.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_acceleratorPointerTags(
   DWORD          cnt,
   DWORD*         pcnt,
   DWORD*         pPointerTags);
```

#### <a name="parameters"></a>Parâmetros
 `cnt`

no O tamanho da matriz de saída `pPointerTags` .

 `pcnt`

fora A contagem de marcas do ponteiro do acelerador na função de stub do acelerador de C++ AMP.

 `pPointerTags`

fora Um `DWORD` ponteiro de matriz que é preenchido com os valores de marca do ponteiro de acelerador na função de stub C++ amp Accelerator.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

## <a name="remarks"></a>Comentários
 Esse método é chamado em uma `IDiaSymbol` interface que corresponde a uma função de stub de C++ amp Accelerator.

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)