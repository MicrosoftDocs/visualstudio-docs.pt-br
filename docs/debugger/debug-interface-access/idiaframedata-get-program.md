---
description: Recupera a cadeia de caracteres do programa que é usada para calcular o conjunto de registros antes da chamada para a função atual.
title: IDiaFrameData::get_program | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_program method
ms.assetid: 9201409e-b4b1-4e2e-a9f8-d17678ac538b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d3e16503d025771b3af34c7f4eee185c2f6aacab
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102148489"
---
# <a name="idiaframedataget_program"></a>IDiaFrameData::get_program
Recupera a cadeia de caracteres do programa que é usada para calcular o conjunto de registros antes da chamada para a função atual.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_program ( 
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna a cadeia de caracteres do programa.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não há suporte para essa propriedade. Caso contrário, retornará um código de erro.

## <a name="remarks"></a>Comentários
 A cadeia de caracteres do programa é uma sequência de macros que é interpretada para estabelecer o prólogo. Por exemplo, um quadro de pilha típico pode usar a cadeia de caracteres do programa `"$T0 $ebp = $eip $T0 4 + ^ = $ebp $T0 ^ = $esp $T0 8 + ="` . O formato é notação de polonês reverso, em que os operadores seguem os operandos. `T0` representa uma variável temporária na pilha. Este exemplo executa as seguintes etapas:

1. Mover o conteúdo do registro `ebp` para `T0` .

2. Adicione `4` ao valor em `T0` para produzir um endereço, obtenha o valor desse endereço e armazene o valor no registro `eip` .

3. Obtenha o valor do endereço armazenado em `T0` e armazene esse valor no registro `ebp` .

4. Adicione `8` ao valor em `T0` e armazene esse valor no registro `esp` .

   Observe que a cadeia de caracteres do programa é específica para a CPU e para a Convenção de chamada configurada para a função representada pelo quadro de pilhas atual.

## <a name="see-also"></a>Confira também
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
