---
title: IDiaEnumSymbols | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSymbols interface
ms.assetid: 649f7bfd-86ac-49a5-8533-aff77e1bc62e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 44be5f88542d867d8baf25fbc3cdd3c060231d7d
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 02/21/2019
ms.locfileid: "56635326"
---
# <a name="idiaenumsymbols"></a>IDiaEnumSymbols
Enumera os vários símbolos contidos na fonte de dados.

## <a name="syntax"></a>Sintaxe

```
IDiaEnumSymbols : IUnknown
```

## <a name="methods-in-vtable-order"></a>Métodos na ordem de Vtable
A tabela a seguir mostra os métodos de `IDiaEnumSymbols`.

|Método|Descrição|
|------------|-----------------|
|[IDiaEnumSymbols::get__NewEnum](../../debugger/debug-interface-access/idiaenumsymbols-get-newenum.md)|Recupera o `IEnumVARIANT Interface` versão este enumerador.|
|[IDiaEnumSymbols::get_Count](../../debugger/debug-interface-access/idiaenumsymbols-get-count.md)|Recupera o número de símbolos.|
|[IDiaEnumSymbols::Item](../../debugger/debug-interface-access/idiaenumsymbols-item.md)|Recupera um símbolo por meio de um índice.|
|[IDiaEnumSymbols::Next](../../debugger/debug-interface-access/idiaenumsymbols-next.md)|Recupera um número especificado de símbolos na sequência de enumeração.|
|[IDiaEnumSymbols::Skip](../../debugger/debug-interface-access/idiaenumsymbols-skip.md)|Ignora um número especificado de símbolos em uma sequência de enumeração.|
|[IDiaEnumSymbols::Reset](../../debugger/debug-interface-access/idiaenumsymbols-reset.md)|Redefine uma sequência de enumeração para o início.|
|[IDiaEnumSymbols::Clone](../../debugger/debug-interface-access/idiaenumsymbols-clone.md)|Cria um enumerador que contém o mesmo estado de enumeração que o enumerador atual.|

## <a name="remarks"></a>Comentários
Essa interface fornece símbolos agrupados por um tipo específico de símbolo, por exemplo, `SymTagUDT` (tipos definidos pelo usuário) ou `SymTagBaseClass`. Para trabalhar com símbolos agrupados por endereço, use o [IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md) interface.

## <a name="notes-for-callers"></a>Observações para chamadores
Obtenha essa interface chamando os métodos a seguir:

- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)

- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)

- [IDiaSourceFile::get_compilands](../../debugger/debug-interface-access/idiasourcefile-get-compilands.md)

## <a name="example"></a>Exemplo
Este exemplo mostra como obter o `IDiaEnumSymbols` de interface e, em seguida, usar essa enumeração para tipos de lista definidos pelo usuário (UDTs).

> [!NOTE]
> `CDiaBSTR` é uma classe que encapsula um `BSTR` e manipula automaticamente a liberar a cadeia de caracteres quando a instanciação sai do escopo.

```C++
void ShowUDTs(IDiaSymbol *pGlobals)
{
    CComPtr<IDiaEnumSymbols> pEnum;
    CComPtr<IDiaSymbol> pSymbol;
    HRESULT hr;

    hr = pGlobals->findChildren(SymTagUDT,
                                NULL,
                                nsfCaseInsensitive | nsfUndecoratedName,
                                &pEnum);
    if (hr == S_OK)
    {
        while ( SUCCEEDED( hr = pEnum->Next( 1, &pSymbol, &celt ) ) &&
                celt == 1 )
        {
            CDiaBSTR name;
            if ( pSymbol->get_name( &name ) != S_OK )
                Fatal( "get_name" );
            printf( "Found UDT: %ws\n", name );
            pSymbol = 0;
        }
    }
}
```

## <a name="requirements"></a>Requisitos
Cabeçalho: Dia2.h

Biblioteca: diaguids.lib

DLL: msdia80.dll

## <a name="see-also"></a>Consulte também
- [Interfaces (SDK de Acesso à Interface de Depuração)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)
- [IDiaSourceFile::get_compilands](../../debugger/debug-interface-access/idiasourcefile-get-compilands.md)
- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)
