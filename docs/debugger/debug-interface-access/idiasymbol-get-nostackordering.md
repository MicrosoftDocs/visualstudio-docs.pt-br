---
title: IDiaSymbol::get_noStackOrdering | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_noStackOrdering method
ms.assetid: a1753917-705b-4165-9880-d05e91e6dcb4
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c82b8c4836d97f02fa84aec500d961911f993df3
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85462787"
---
# <a name="idiasymbolget_nostackordering"></a>IDiaSymbol::get_noStackOrdering
Essa função recupera um sinalizador que indica se nenhuma ordem de pilha pode ser feita como parte da verificação do buffer de pilha (opção[de compilador/GS (verificação de segurança de buffer)](/cpp/build/reference/gs-buffer-security-check) ).

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_noStackOrdering(
   BOOL *pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna `TRUE` se nenhuma ordem de pilha pode ser feita como parte da verificação do buffer de pilha; caso contrário, retorna `FALSE` .

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="requirements"></a>Requisitos

|Requisito|Descrição|
|-----------------|-----------------|
|Cabeçalho:|dia2.h|
|Versão:|DIA SDK v 8.0|

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [/GS (verificação de segurança do buffer)](/cpp/build/reference/gs-buffer-security-check)