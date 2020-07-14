---
title: IDiaSectionContrib | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib interface
ms.assetid: 371d40f6-ca0e-4d7e-9210-64d3768996c6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 82d1a52616273a1cfe1d54580c91ec4ba6e1c09e
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85466066"
---
# <a name="idiasectioncontrib"></a>IDiaSectionContrib
Recupera dados que descrevem uma contribuição de seção, ou seja, um bloco contíguo de memória contribuído para a imagem por um compiland.

## <a name="syntax"></a>Syntax

```
IDiaSectionContrib : IUnknown
```

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
A tabela a seguir mostra os métodos de `IDiaSectionContrib` .

|Método|Descrição|
|------------|-----------------|
|[IDiaSectionContrib::get_compiland](../../debugger/debug-interface-access/idiasectioncontrib-get-compiland.md)|Recupera uma referência ao símbolo compiland que contribuiu para esta seção.|
|[IDiaSectionContrib::get_addressSection](../../debugger/debug-interface-access/idiasectioncontrib-get-addresssection.md)|Recupera a parte da seção do endereço da contribuição.|
|[IDiaSectionContrib::get_addressOffset](../../debugger/debug-interface-access/idiasectioncontrib-get-addressoffset.md)|Recupera a parte offset do endereço da contribuição.|
|[IDiaSectionContrib::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiasectioncontrib-get-relativevirtualaddress.md)|Recupera o endereço virtual relativo da imagem (RVA) da contribuição.|
|[IDiaSectionContrib::get_virtualAddress](../../debugger/debug-interface-access/idiasectioncontrib-get-virtualaddress.md)|Recupera o endereço virtual (VA) da contribuição.|
|[IDiaSectionContrib::get_length](../../debugger/debug-interface-access/idiasectioncontrib-get-length.md)|Recupera o número de bytes em uma seção.|
|[IDiaSectionContrib::get_notPaged](../../debugger/debug-interface-access/idiasectioncontrib-get-notpaged.md)|Recupera um sinalizador que indica se a seção não pode ser paginada da memória.|
|[IDiaSectionContrib::get_nopad](../../debugger/debug-interface-access/idiasectioncontrib-get-nopad.md)|Recupera um sinalizador que indica se a seção não deve ser preenchida para o próximo limite de memória.|
|[IDiaSectionContrib::get_code](../../debugger/debug-interface-access/idiasectioncontrib-get-code.md)|Recupera um sinalizador que indica se a seção contém código executável.|
|[IDiaSectionContrib::get_code16bit](../../debugger/debug-interface-access/idiasectioncontrib-get-code16bit.md)|Recupera um sinalizador que indica se a seção contém código de 16 bits.|
|[IDiaSectionContrib::get_initializedData](../../debugger/debug-interface-access/idiasectioncontrib-get-initializeddata.md)|Recupera um sinalizador que indica se a seção contém dados inicializados.|
|[IDiaSectionContrib::get_uninitializedData](../../debugger/debug-interface-access/idiasectioncontrib-get-uninitializeddata.md)|Recupera um sinalizador que indica se a seção contém dados não inicializados.|
|[IDiaSectionContrib::get_informational](../../debugger/debug-interface-access/idiasectioncontrib-get-informational.md)|Recupera um sinalizador que indica se uma seção contém comentários ou informações semelhantes.|
|[IDiaSectionContrib::get_remove](../../debugger/debug-interface-access/idiasectioncontrib-get-remove.md)|Recupera um sinalizador que indica se a seção é removida antes de ser feita como parte da imagem na memória.|
|[IDiaSectionContrib::get_comdat](../../debugger/debug-interface-access/idiasectioncontrib-get-comdat.md)|Recupera um sinalizador que indica se a seção é um registro COMDAT.|
|[IDiaSectionContrib::get_discardable](../../debugger/debug-interface-access/idiasectioncontrib-get-discardable.md)|Recupera um sinalizador que indica se a seção pode ser descartada.|
|[IDiaSectionContrib::get_notCached](../../debugger/debug-interface-access/idiasectioncontrib-get-notcached.md)|Recupera um sinalizador que indica se a seção não pode ser armazenada em cache.|
|[IDiaSectionContrib::get_share](../../debugger/debug-interface-access/idiasectioncontrib-get-share.md)|Recupera um sinalizador que indica se a seção pode ser compartilhada na memória.|
|[IDiaSectionContrib::get_execute](../../debugger/debug-interface-access/idiasectioncontrib-get-execute.md)|Recupera um sinalizador que indica se a seção é executável como código.|
|[IDiaSectionContrib::get_read](../../debugger/debug-interface-access/idiasectioncontrib-get-read.md)|Recupera um sinalizador que indica se a seção pode ser lida.|
|[IDiaSectionContrib::get_write](../../debugger/debug-interface-access/idiasectioncontrib-get-write.md)|Recupera um sinalizador que indica se a seção pode ser gravada.|
|[IDiaSectionContrib::get_dataCrc](../../debugger/debug-interface-access/idiasectioncontrib-get-datacrc.md)|Recupera a CRC (verificação de redundância cíclica) dos dados na seção.|
|[IDiaSectionContrib::get_relocationsCrc](../../debugger/debug-interface-access/idiasectioncontrib-get-relocationscrc.md)|Recupera o CRC das informações de realocação da seção.|
|[IDiaLineNumber::get_compilandId](../../debugger/debug-interface-access/idialinenumber-get-compilandid.md)|Recupera o identificador de compiland para a seção.|

## <a name="remarks"></a>Comentários

## <a name="notes-for-callers"></a>Observações para chamadores
Essa interface é obtida chamando os métodos [IDiaEnumSectionContribs:: item](../../debugger/debug-interface-access/idiaenumsectioncontribs-item.md) e [IDiaEnumSectionContribs:: Next](../../debugger/debug-interface-access/idiaenumsectioncontribs-next.md) . Consulte a interface [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md) para obter um exemplo de como obter a `IDiaSectionContrib` interface.

## <a name="example"></a>Exemplo
Essa função mostra o endereço de cada seção junto com quaisquer símbolos associados. Consulte a interface [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md) para ver como a `IDiaSectionContrib` interface é obtida.

```C++
void PrintSectionContrib(IDiaSectionContrib* pSecContrib, IDiaSession* pSession)
{
    if (pSecContrib != NULL && pSession != NULL)
    {
        DWORD rva;
        if ( pSecContrib->get_relativeVirtualAddress( &rva ) == S_OK )
        {
            printf( "\taddr: 0x%.8X", rva );
            pSecContrib = NULL;
            CComPtr<IDiaSymbol> pSym;
            if ( psession->findSymbolByRVA( rva, SymTagNull, &pSym ) == S_OK )
            {
                CDiaBSTR name;
                DWORD    tag;
                pSym->get_symTag( &tag );
                pSym->get_name( &name );
                printf( "     symbol: %ws (%ws)\n",
                        name != NULL ? name : L"",
                        szTags[ tag ] );
            }
            else
            {
                printf( "<no symbol found?>\n" );
            }
        }
        else
        {
            DWORD isect;
            DWORD offset;
            pSecContrib->get_addressSection( &isect );
            pSecContrib->get_addressOffset( &offset );
            printf( "\taddr: 0x%.4X:0x%.8X", isect, offset );
            pSecContrib = NULL;
            CComPtr<IDiaSymbol> pSym;
            if ( SUCCEEDED( psession->findSymbolByAddr(
                                              isect,
                                              offset,
                                              SymTagNull,
                                              &pSym )
                          )
               )
            {
                CDiaBSTR name;
                DWORD    tag;
                pSym->get_symTag( &tag );
                pSym->get_name( &name );
                printf( "     symbol: %ws (%ws)\n",
                    name != NULL ? name : L"",
                    szTags[ tag ] );
            }
            else
            {
                printf( "<no symbol found?>\n" );
            }
        }
    }
}
```

## <a name="requirements"></a>Requisitos
Cabeçalho: dia2. h

Biblioteca: diaguids. lib

DLL: msdia80.dll

## <a name="see-also"></a>Veja também
- [Interfaces (SDK de Acesso à Interface de Depuração)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)
- [IDiaEnumSectionContribs::Item](../../debugger/debug-interface-access/idiaenumsectioncontribs-item.md)
- [IDiaEnumSectionContribs::Next](../../debugger/debug-interface-access/idiaenumsectioncontribs-next.md)
