---
description: Recupera o deslocamento do painel de pilha do registro do ponteiro do quadro.
title: 'IDiaSymbol:: get_framePadOffset | Microsoft Docs'
ms.date: 04/27/2021
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_framePadOffset method
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 455e617188a58090f3bd6229ab008847912b1f19
ms.sourcegitcommit: 30c404655fb83ea28f96ab1edb1c09b4d8d7eec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/29/2021
ms.locfileid: "108217219"
---
# <a name="idiasymbolget_framepadoffset"></a>IDiaSymbol:: get_framePadOffset

Recupera o deslocamento do painel de pilha do registro do ponteiro do quadro.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_framePadOffset ( 
   DWORD* pPadOffset
);
```

#### <a name="parameters"></a>Parâmetros

 `pPadOffset`

fora Retorna o deslocamento do painel de pilha.

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
