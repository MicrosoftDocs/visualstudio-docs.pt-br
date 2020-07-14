---
title: IDiaTable | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaTable interface
ms.assetid: c99a2c44-7b72-4e3c-b963-25fe3df3a555
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 984b9d5d9bfd5c3800ec816e1f57489e0348f53c
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85461283"
---
# <a name="idiatable"></a>IDiaTable
Enumera uma tabela de fonte de dados de DIA.

## <a name="syntax"></a>Syntax

```
IDiaTable : IEnumUnknown
```

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
A tabela a seguir mostra os métodos de `IDiaTable` .

|Método|Descrição|
|------------|-----------------|
|[IDiaTable::get__NewEnum](../../debugger/debug-interface-access/idiatable-get-newenum.md)|Recupera a versão da [interface IEnumVARIANT](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-ienumvariant) deste enumerador.|
|[IDiaTable::get_name](../../debugger/debug-interface-access/idiatable-get-name.md)|Recupera o nome da tabela.|
|[IDiaTable::get_Count](../../debugger/debug-interface-access/idiatable-get-count.md)|Recupera o número de itens na tabela.|
|[IDiaTable::Item](../../debugger/debug-interface-access/idiatable-item.md)|Recupera uma referência a um índice de entrada específico.|

## <a name="remarks"></a>Comentários
Essa interface implementa os `IEnumUnknown` métodos de enumeração no namespace Microsoft. VisualStudio. OLE. Interop. A `IEnumUnknown` interface de enumeração é muito mais eficiente para iterar sobre o conteúdo da tabela do que os métodos [IDiaTable:: Get_Count](../../debugger/debug-interface-access/idiatable-get-count.md) e [IDiaTable:: item](../../debugger/debug-interface-access/idiatable-item.md) .

A interpretação da `IUnknown` interface retornada do `IDiaTable::Item` método ou do `Next` método (no namespace Microsoft. VisualStudio. OLE. Interop) depende do tipo de tabela. Por exemplo, se a `IDiaTable` interface representa uma lista de fontes injetadas, a `IUnknown` interface deve ser consultada para a interface [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md) .

## <a name="notes-for-callers"></a>Observações para chamadores
Obtenha essa interface chamando os métodos [IDiaEnumTables:: item](../../debugger/debug-interface-access/idiaenumtables-item.md) ou [IDiaEnumTables:: Next](../../debugger/debug-interface-access/idiaenumtables-next.md) .

As seguintes interfaces são implementadas com a `IDiaTable` interface (ou seja, você pode consultar a `IDiaTable` interface para uma das seguintes interfaces):

- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)

- [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)

- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)

- [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)

- [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)

- [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)

- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)

## <a name="example"></a>Exemplo
A primeira função, `ShowTableNames` , exibe os nomes de todas as tabelas na sessão. A segunda função, `GetTable` , pesquisa todas as tabelas de uma tabela que implementa uma interface especificada. A terceira função, `UseTable` , mostra como usar a `GetTable` função.

> [!NOTE]
> `CDiaBSTR`é uma classe que encapsula um `BSTR` e automaticamente trata a liberação da cadeia de caracteres quando a instanciação sai do escopo.

```C++
void ShowTableNames(IDiaSession *pSession)
{
    CComPtr<IDiaEnumTables> pTables;
    if ( FAILED( psession->getEnumTables( &pTables ) ) )
    {
        Fatal( "getEnumTables" );
    }
    CComPtr< IDiaTable > pTable;
    while ( SUCCEEDED( hr = pTables->Next( 1, &pTable, &celt ) )
            && celt == 1 )
    {
        CDiaBSTR bstrTableName;
        if ( pTable->get_name( &bstrTableName ) != 0 )
        {
            Fatal( "get_name" );
        }
        printf( "Found table: %ws\n", bstrTableName );
    }

// Searches the list of all tables for a table that supports
// the specified interface.  Use this function to obtain an
// enumeration interface.
HRESULT GetTable(IDiaSession* pSession,
                 REFIID       iid,
                 void**       ppUnk)
{
    CComPtr<IDiaEnumTables> pEnumTables;
    HRESULT hResult;

    if (FAILED(pSession->getEnumTables(&pEnumTables)))
        Fatal("getEnumTables");

    CComPtr<IDiaTable> pTable;
    ULONG celt = 0;
    while (SUCCEEDED(hResult = pEnumTables->Next(1, &pTable, &celt)) &&
           celt == 1)
    {
        if (pTable->QueryInterface(iid, (void**)ppUnk) == S_OK)
        {
            return S_OK;
        }
        pTable = NULL;
    }

    if (FAILED(hResult))
        Fatal("EnumTables->Next");

    return E_FAIL;
}

// This function shows how to use the GetTable function.
void UseTable(IDiaSession *pSession)
{
    CComPtr<IDiaEnumSegments> pEnumSegments;
    if (SUCCEEDED(GetTable(pSession, __uuidof(IDiaEnumSegments), &pEnumSegments)))
    {
        // Do something with pEnumSegments.
    }
}
```

## <a name="requirements"></a>Requisitos
Cabeçalho: dia2. h

Biblioteca: diaguids. lib

DLL: msdia80.dll

## <a name="see-also"></a>Veja também
- [Interfaces (SDK de Acesso à Interface de Depuração)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)
- [IDiaEnumTables::Item](../../debugger/debug-interface-access/idiaenumtables-item.md)
- [IDiaEnumTables::Next](../../debugger/debug-interface-access/idiaenumtables-next.md)
