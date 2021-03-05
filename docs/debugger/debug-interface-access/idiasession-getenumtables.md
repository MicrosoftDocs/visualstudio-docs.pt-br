---
description: Recupera um enumerador para todas as tabelas contidas no repositório de símbolos.
title: IDiaSession::getEnumTables | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::getEnumTables method
ms.assetid: 66e0fba2-ca63-4e24-a46a-c99c7fb61dd1
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d75ac2a4bca7051c6fe80f80b7a8063ef7ec6c86
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102157017"
---
# <a name="idiasessiongetenumtables"></a>IDiaSession::getEnumTables
Recupera um enumerador para todas as tabelas contidas no repositório de símbolos.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT getEnumTables (
    IDiaEnumTables** ppEnumTables
);
```

#### <a name="parameters"></a>Parâmetros
`ppEnumTables`

fora Retorna um objeto [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md) . Use essa interface para enumerar as tabelas no repositório de símbolos.

## <a name="return-value"></a>Valor Retornado
Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="example"></a>Exemplo
Este exemplo apresenta uma função geral que usa o `getEnumTables` método para obter um objeto enumerador específico. Se o enumerador for encontrado, a função retornará um ponteiro que pode ser convertido na interface desejada; caso contrário, a função retornará `NULL` .

```C++
IUnknown *GetTable(IDiaSession *pSession, REFIID iid)
{
    IUnknown *pUnknown = NULL;
    if (pSession != NULL)
    {
        CComPtr<IDiaEnumTables> pEnumTables;
        if (pSession->getEnumTables(&pEnumTables) == S_OK)
        {
            CComPtr<IDiaTable> pTable;
            DWORD celt = 0;
            while(pEnumTables->Next(1,&pTable,&celt) == S_OK &&
                  celt == 1)
            {
                if (pTable->QueryInterface(iid, (void **)pUnknown) == S_OK)
                {
                    break;
                }
                pTable = NULL;
            }
        }
    }
    return(pUnknown);
}
```

## <a name="see-also"></a>Confira também
- [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
