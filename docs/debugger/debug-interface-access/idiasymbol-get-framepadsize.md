---
description: Recupera o tamanho de PAD extra adicionado a cada função.
title: 'IDiaSymbol:: get_framePadSize | Microsoft Docs'
ms.date: 04/27/2021
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_framePadSize method
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d361ec3e144730e49345d3560f815ee5fe0be469
ms.sourcegitcommit: 30c404655fb83ea28f96ab1edb1c09b4d8d7eec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/29/2021
ms.locfileid: "108217217"
---
# <a name="idiasymbolget_framepadsize"></a>IDiaSymbol:: get_framePadSize

Recupera o tamanho de PAD extra adicionado a cada função.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_framePadSize ( 
   DWORD* pPadSize
);
```

#### <a name="parameters"></a>Parâmetros

 `pPadSize`

fora Retorna o tamanho de PAD extra adicionado a cada função.

## <a name="return-value"></a>Valor Retornado

 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou código de erro.

> [!NOTE]
> Um valor de retorno de `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="remarks"></a>Comentários

O tamanho do PAD extra normalmente é usado por editar e continuar.

Esse método tem suporte a partir do Visual Studio 2019 versão 16,10 Preview 2.

## <a name="requirements"></a>Requisitos

|Requisito|Descrição|
|-----------------|-----------------|
|Cabeçalho:|dia2.h|
|Versão:|DIA SDK v 7.0|

## <a name="see-also"></a>Confira também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
