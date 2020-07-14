---
title: IDiaSymbol::get_symbolsFileName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_symbolsFileName method
ms.assetid: c1aa39ee-d645-431e-bf5f-0640c0998934
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d83747d3db9336c00d8c770db415093de693f1c7
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85461924"
---
# <a name="idiasymbolget_symbolsfilename"></a>IDiaSymbol::get_symbolsFileName
Recupera o nome do arquivo do qual os símbolos foram carregados.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_symbolsFileName ( 
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna o nome do arquivo do qual os símbolos foram carregados.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno de `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="remarks"></a>Comentários
 Essa propriedade só é válida para símbolos com um valor de [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md) `SymTagExe` que também tenha escopo global.

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md)