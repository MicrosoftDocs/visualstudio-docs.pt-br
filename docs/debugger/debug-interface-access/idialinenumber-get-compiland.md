---
title: IDiaLineNumber::get_compiland | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaLineNumber::get_compiland method
ms.assetid: c476d0b8-c473-47eb-96f5-c4e8f577b1c9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 25d990ab019c01daf1f977464211fb72838275a1
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 02/21/2019
ms.locfileid: "56618660"
---
# <a name="idialinenumbergetcompiland"></a>IDiaLineNumber::get_compiland
Recupera uma referência ao símbolo para compiland que contribuíram os bytes do texto da imagem.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_compiland ( 
   IDiaSymbol** pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 pRetVal

[out] Retorna um [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) objeto para compiland que contribuíram os bytes do texto da imagem.

## <a name="return-value"></a>Valor de retorno
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não há suporte para essa propriedade. Caso contrário, retornará um código de erro.

## <a name="see-also"></a>Consulte também
- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)