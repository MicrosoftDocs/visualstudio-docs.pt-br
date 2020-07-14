---
title: IDiaSymbol::findChildrenEx | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::findChildrenEx
ms.assetid: 6e045045-da8c-4338-9423-81a1ca20c405
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 191991ffb842657b7a7c4f439ca04a05670bca7d
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85464579"
---
# <a name="idiasymbolfindchildrenex"></a>IDiaSymbol::findChildrenEx
Recupera os filhos do símbolo. Os símbolos locais que são retornados incluem informações de intervalo ao vivo, se o programa for compilado com otimização ativada.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT findChildrenEx ( 
   enum SymTagEnum   symtag,
   LPCOLESTR         name,
   DWORD             compareFlags,
   IDiaEnumSymbols** ppResult
);
```

#### <a name="parameters"></a>Parâmetros
 `symtag`

no Especifica as marcas de símbolo dos filhos a serem recuperados, conforme definido na [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md). Defina como `SymTagNull` para todos os filhos a serem recuperados.

 `name`

no Especifica o nome dos filhos a serem recuperados. Defina como `NULL` para todos os filhos a serem recuperados.

 `compareFlags`

no Especifica as opções de comparação a serem aplicadas à correspondência de nomes. Os valores da enumeração de [Enumeração NameSearchOptions](../../debugger/debug-interface-access/namesearchoptions.md) podem ser usados sozinhos ou em combinação.

 `ppResult`

fora Retorna um objeto [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md) que contém uma lista dos símbolos filho recuperados.

## <a name="return-value"></a>Valor Retornado
 Retorna `S_OK` se pelo menos um filho do símbolo foi encontrado ou retorna `S_FALSE` se nenhum filho foi encontrado; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Este método é a versão estendida de [IDiaSymbol:: findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md).

## <a name="requirements"></a>Requisitos
 Cabeçalho: dia2. h

 Biblioteca: diaguids. lib

 DLL: msdia100.dll

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)
- [Enumeração NameSearchOptions](../../debugger/debug-interface-access/namesearchoptions.md)