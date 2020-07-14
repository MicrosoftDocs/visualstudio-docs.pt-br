---
title: IDiaLineNumber::get_length | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLineNumber::get_length method
ms.assetid: 2c55a6f7-4ef5-45fb-9fd1-d72deaaa2829
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3804d018569a0b2e0ee5a11a3bb5edc8363cfffc
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85466885"
---
# <a name="idialinenumberget_length"></a>IDiaLineNumber::get_length
Recupera o número de bytes em um bloco.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_length ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna o número de bytes em um bloco.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não há suporte para essa propriedade. Caso contrário, retornará um código de erro.

## <a name="remarks"></a>Comentários
 O bloco é o comprimento do código-fonte na linha, conforme representado pelo objeto [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md) .

## <a name="see-also"></a>Veja também
- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)