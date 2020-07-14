---
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3ea4a05bfccddeedb29110ea6ee44f34f85534a8
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85466843"
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

## <a name="see-also"></a>Veja também
- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)