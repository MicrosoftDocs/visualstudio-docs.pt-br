---
description: Recupera um sinalizador que indica que essas informações de linha descrevem o início de uma instrução, em vez de uma expressão, na origem do programa.
title: IDiaLineNumber::get_statement | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLineNumber::get_statement method
ms.assetid: 22b8ee29-79ef-427f-bd05-00d255ab836b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e6c36852f5aa48bcd5146419415dd06ec9d0a847
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102157437"
---
# <a name="idialinenumberget_statement"></a>IDiaLineNumber::get_statement
Recupera um sinalizador que indica que essas informações de linha descrevem o início de uma instrução, em vez de uma expressão, na origem do programa.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_statement ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna `TRUE` se as informações da linha descrevem o início de uma instrução na origem do programa.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não há suporte para essa propriedade. Caso contrário, retornará um código de erro.

## <a name="remarks"></a>Comentários
 As instruções podem abranger várias linhas. Esse método indica se o número de linha associado marca o início de uma instrução de várias linhas.

## <a name="see-also"></a>Confira também
- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)
