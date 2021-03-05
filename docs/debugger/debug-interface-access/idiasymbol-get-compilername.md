---
description: Retorna o nome do compilador usado para gerar o compiland).
title: IDiaSymbol::get_compilerName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_compilerName method
ms.assetid: 66eaaf72-68d4-40ee-b132-97bea9fe395c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 27f59110696a12423b9ada1001bcbce8c84d7b5d
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102162196"
---
# <a name="idiasymbolget_compilername"></a>IDiaSymbol::get_compilerName
Retorna o nome do compilador usado para gerar o [compiland](../../debugger/debug-interface-access/compiland.md).

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_compilerName (
   BSTR *pName
);
```

#### <a name="parameters"></a>Parâmetros
 `pName` Ponteiro para um BSTR que conterá o nome Unicode do compilador.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno de `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="remarks"></a>Comentários

## <a name="requirements"></a>Requisitos

|Requisito|Descrição|
|-----------------|-----------------|
|Cabeçalho:|dia2.h|
|Versão:|DIA SDK v 8.0|

## <a name="see-also"></a>Confira também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
