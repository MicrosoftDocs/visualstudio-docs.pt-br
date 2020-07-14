---
title: 'IDiaSymbol:: get_numberOfAcceleratorPointerTags | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 1886e3ec-b227-4187-8d93-c5144b4b77ae
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a4690afe754db2c5e82d200de780d28aae3c652e
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85462766"
---
# <a name="idiasymbolget_numberofacceleratorpointertags"></a>IDiaSymbol::get_numberOfAcceleratorPointerTags
Retorna o número de marcas do ponteiro do acelerador em uma C++ AMP função de stub.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_numberOfAcceleratorPointerTags(
   DWORD* count);
```

#### <a name="parameters"></a>Parâmetros
 `count`

fora Um ponteiro para um `DWORD` que contém o número de marcas de ponteiro de acelerador em uma C++ amp função de stub.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

## <a name="remarks"></a>Comentários
 Esse método é chamado em uma `IDiaSymbol` interface que corresponde a uma função de stub de C++ amp Accelerator.

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)