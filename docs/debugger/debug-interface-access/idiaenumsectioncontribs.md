---
title: IDiaEnumSectionContribs | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSectionContribs interface
ms.assetid: 0d6c0632-310f-4a99-8921-58149a1817e3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ebc0fe8391c6390d62cffbb591c4cef1ea52976f
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85468068"
---
# <a name="idiaenumsectioncontribs"></a>IDiaEnumSectionContribs
Enumera as várias contribuições de seção contidas na fonte de dados.

## <a name="syntax"></a>Syntax

```
IDiaEnumSectionContribs : IUnknown
```

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
A tabela a seguir mostra os métodos de `IDiaEnumSectionContribs` .

|Método|Descrição|
|------------|-----------------|
|[IDiaEnumSectionContribs::get__NewEnum](../../debugger/debug-interface-access/idiaenumsectioncontribs-get-newenum.md)|Recupera a versão da [interface IEnumVARIANT](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-ienumvariant) deste enumerador.|
|[IDiaEnumSectionContribs::get_Count](../../debugger/debug-interface-access/idiaenumsectioncontribs-get-count.md)|Recupera o número de contribuições de seção.|
|[IDiaEnumSectionContribs::Item](../../debugger/debug-interface-access/idiaenumsectioncontribs-item.md)|Recupera contribuições de seção por meio de um índice.|
|[IDiaEnumSectionContribs::Next](../../debugger/debug-interface-access/idiaenumsectioncontribs-next.md)|Recupera um número especificado de contribuições de seção na sequência de enumeração.|
|[IDiaEnumSectionContribs::Skip](../../debugger/debug-interface-access/idiaenumsectioncontribs-skip.md)|Ignora um número especificado de contribuições de seção em uma sequência de enumeração.|
|[IDiaEnumSectionContribs::Reset](../../debugger/debug-interface-access/idiaenumsectioncontribs-reset.md)|Redefine uma sequência de enumeração para o início.|
|[IDiaEnumSectionContribs::Clone](../../debugger/debug-interface-access/idiaenumsectioncontribs-clone.md)|Cria um enumerador que contém o mesmo estado de enumeração que o enumerador atual.|

## <a name="remarks"></a>Comentários

## <a name="note-for-callers"></a>Observação para chamadores
Obtenha essa interface do método [IDiaSession:: getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md) . Consulte o exemplo para obter detalhes.

## <a name="example"></a>Exemplo
Este exemplo mostra como obter (a `GetEnumSectionContribs` função) e usar (a `ShowSectionContribs` função) a `IDiaEnumSectionContribs` interface. Para obter um exemplo mais completo de como usar as contribuições de seção, consulte a interface [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md) .

```C++

IDiaEnumSectionContribs* GetEnumSectionContribs(IDiaSession *pSession)
{
    IDiaEnumSectionContribs* pUnknown    = NULL;
    REFIID                   iid         = __uuidof(IDiaEnumSectionContribs);
    IDiaEnumTables*          pEnumTables = NULL;
    IDiaTable*               pTable      = NULL;
    ULONG                    celt        = 0;

    if (pSession->getEnumTables(&pEnumTables) != S_OK)
    {
        wprintf(L"ERROR - GetTable() getEnumTables\n");
        return NULL;
    }
    while (pEnumTables->Next(1, &pTable, &celt) == S_OK && celt == 1)
    {
        // There is only one table that matches the given iid
        HRESULT hr = pTable->QueryInterface(iid, (void**)&pUnknown);
        pTable->Release();
        if (hr == S_OK)
        {
            break;
        }
    }
    pEnumTables->Release();
    return pUnknown;
}

void ShowSectionContribs(IDiaSession *pSession)
{
    IDiaEnumSectionContribs* pEnumSectionContribs;

    pEnumSectionContribs = GetEnumSectionContribs(pSession);
    if (pSectionContrib != NULL)
    {
        IDiaSectionContrib* pSectionContrib;
        ULONG celt = 0;

        while(pEnumSectionContribs->Next(1, &pSectionContrib, &celt) == S_OK &&
              celt == 1)
        {
            PrintSectionContrib(pSectionContrib, pSession);
            pSectionContrib->Release();
        }
        pSectionContrib->Release();
    }
}
```

## <a name="requirements"></a>Requisitos
Cabeçalho: dia2. h

Biblioteca: diaguids. lib

DLL: msdia80.dll

## <a name="see-also"></a>Veja também
- [Interfaces (SDK de Acesso à Interface de Depuração)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaSession::getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md)
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
