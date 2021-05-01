---
description: Recupera um valor que informa se a função foi compilada com verificação de erro de tempo de execução de quadro de pilha. Esse é o sinalizador/RTCs.
title: 'IDiaSymbol:: get_isRTCs | Microsoft Docs'
ms.date: 04/27/2021
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isRTCs method
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9a297abe6326af6f04058e6095f59f880f526adb
ms.sourcegitcommit: 30c404655fb83ea28f96ab1edb1c09b4d8d7eec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/29/2021
ms.locfileid: "108217218"
---
# <a name="idiasymbolget_isrtcs"></a>IDiaSymbol:: get_isRTCs

Retorna um valor que informa se a função foi compilada com verificação de erro de tempo de execução de quadro de pilha. Esse é o sinalizador/RTCs.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_isRTCs ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros

 `pRetVal`

fora Um ponteiro para um BOOL que especifica se a função foi compilada com verificação de erro de tempo de execução de quadro de pilha.

## <a name="return-value"></a>Valor Retornado

 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou código de erro.

> [!NOTE]
> Um valor de retorno de `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="remarks"></a>Comentários

Esse método tem suporte a partir do Visual Studio 2019 versão 16,10 Preview 2.

## <a name="requirements"></a>Requisitos

|Requisito|Descrição|
|-----------------|-----------------|
|Cabeçalho:|dia2.h|
|Versão:|DIA SDK v 7.0|

## <a name="see-also"></a>Confira também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
