---
title: IDiaSession::findSymbolByRVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findSymbolByRVA method
ms.assetid: 14fb2903-b771-44d6-b0a8-44e0097c58ce
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a3af468a08d938fbdc19509fc93d48cd7d619a07
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85465562"
---
# <a name="idiasessionfindsymbolbyrva"></a>IDiaSession::findSymbolByRVA
Recupera um tipo de símbolo especificado que contém ou está mais próximo de um endereço virtual relativo (RVA) específico.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT findSymbolByRVA ( 
   DWORD        rva,
   SymTagEnum   symtag,
   IDiaSymbol** ppSymbol
);
```

#### <a name="parameters"></a>Parâmetros
 `rva`

no Especifica o RVA.

 `symtag`

no Tipo de símbolo a ser encontrado. Os valores são obtidos da enumeração de [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md) .

 `ppSymbol`

fora Retorna um objeto [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) que representa o símbolo recuperado.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="example"></a>Exemplo

```C++
IDiaSymbol* pFunc;
pSession->findSymbolByRVA( rva, SymTagFunction, &pFunc );
```

## <a name="see-also"></a>Confira também
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md)