---
title: IDiaSession::findSymbolByRVAEx | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findSymbolByRVAEx method
ms.assetid: 61344966-fed4-4c02-9e27-20356ec2ef7c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 807025265de5c088f1af24ec76402cdbf3a516a7
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85465548"
---
# <a name="idiasessionfindsymbolbyrvaex"></a>IDiaSession::findSymbolByRVAEx
Recupera um tipo de símbolo especificado que contém ou está mais próximo de um endereço virtual relativo (RVA) e deslocamento específico.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT findSymbolByRVAEx ( 
   DWORD        rva,
   SymTagEnum   symtag,
   IDiaSymbol** ppSymbol,
   LONG*        displacement
);
```

#### <a name="parameters"></a>Parâmetros
 `rva`

no Especifica o RVA.

 `symtag`

no Tipo de símbolo a ser encontrado. Os valores são obtidos da enumeração de [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md) .

 `ppSymbol`

fora Retorna um objeto [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) que representa o símbolo recuperado.

 `displacement`

fora Retorna um valor que especifica um deslocamento do endereço virtual relativo especificado em `rva` .

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="example"></a>Exemplo

```C++
IDiaSymbol* pFunc;
LONG disp = 0;
pSession->findSymbolByRVAEx( rva, SymTagFunction, &pFunc, &disp );
```

## <a name="see-also"></a>Confira também
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md)