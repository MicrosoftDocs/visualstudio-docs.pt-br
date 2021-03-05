---
description: Recupera uma referência ao símbolo para o compiland que contribuiu com os bytes do texto da imagem.
title: IDiaLineNumber::get_compiland | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLineNumber::get_compiland method
ms.assetid: c476d0b8-c473-47eb-96f5-c4e8f577b1c9
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2700ffb00c14a0f9f62f274157ffadecb0abee26
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102157591"
---
# <a name="idialinenumberget_compiland"></a>IDiaLineNumber::get_compiland
Recupera uma referência ao símbolo para o compiland que contribuiu com os bytes do texto da imagem.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_compiland ( 
   IDiaSymbol** pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 pRetVal

fora Retorna um objeto [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) para o compiland que contribuiu com os bytes do texto da imagem.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não há suporte para essa propriedade. Caso contrário, retornará um código de erro.

## <a name="see-also"></a>Confira também
- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)
