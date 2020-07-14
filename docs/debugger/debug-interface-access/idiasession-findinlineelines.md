---
title: IDiaSession::findInlineeLines | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: b6822d8b-70d5-470b-8278-3aec4680326c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a03eb23929d3a882b397a8a95f2d9c4c17abf0df
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85465807"
---
# <a name="idiasessionfindinlineelines"></a>IDiaSession::findInlineeLines
Recupera uma enumeração que permite que um cliente itere pelas informações de número de linha de todas as funções que são embutidas, direta ou indiretamente, pelo símbolo pai especificado.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT findInlineeLines ( 
   IDiaSymbol*       parent,
   IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>Parâmetros
 `parent`

no Um `IDiaSymbol` objeto que representa o pai.

 `ppResult`

fora Mantém um `IDiaEnumLineNumbers` objeto que contém a lista de números de linha recuperados.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Veja também
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)