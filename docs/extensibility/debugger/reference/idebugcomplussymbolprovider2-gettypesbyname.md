---
description: Recupera um tipo dado seu nome.
title: 'IDebugComPlusSymbolProvider2:: GetTypesByName | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetTypesByName
- IDebugComPlusSymbolProvider2::GetTypesByName
ms.assetid: ef76b1a8-6910-48fe-b4af-d9045eefd23f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 18d94daf830b852d8a3d13cbda7f9eb494889ff3
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102163389"
---
# <a name="idebugcomplussymbolprovider2gettypesbyname"></a>IDebugComPlusSymbolProvider2::GetTypesByName
Recupera um tipo dado seu nome.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetTypesByName(
    LPCOLESTR          pszClassName,
    NAME_MATCH         nameMatch,
    IEnumDebugFields** ppEnum
);
```

```csharp
int GetTypesByName(
    string               pszClassName,
    enum_ NAME_MATCH     nameMatch,
    out IEnumDebugFields ppEnum
);
```

## <a name="parameters"></a>Parâmetros
`pszClassName`\
no Nome do tipo.

`nameMatch`\
no Seleciona o tipo de correspondência, por exemplo, diferencia maiúsculas de minúsculas. Um valor da enumeração de [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md) .

`ppEnum`\
fora Um enumerador que contém o tipo ou os tipos com o nome fornecido.

## <a name="return-value"></a>Valor Retornado
Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
Para tipos genéricos, o nome a ser pesquisado para ' List \<int> ' ou ' List \<int,int> ' seria ' list '. Se os tipos de mesmo nome aparecerem em vários módulos, o parâmetro conterá `ppEnum` todas as cópias. Você precisa usar [GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md) e distinguir com base no `guidModule` parâmetro.

## <a name="example"></a>Exemplo
O exemplo a seguir mostra como implementar esse método para um objeto **CDebugSymbolProvider** que expõe a interface [IDebugComPlusSymbolProvider2](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2.md) .

```cpp
HRESULT CDebugSymbolProvider::GetTypesByName(
    LPCOLESTR pszClassName,
    NAME_MATCH nameMatch,
    IEnumDebugFields** ppEnum
)
{
    HRESULT hr = S_OK;
    CModIter ModIter;
    CModule* pmodule; // the iterator owns the reference
    CFieldList listField;

    ASSERT(IsValidWideStringPtr(pszClassName));
    ASSERT(IsValidWritePtr(ppEnum, IEnumDebugFields*));

    METHOD_ENTRY( CDebugSymbolProvider::GetTypesByName );

    IfFalseGo( pszClassName && ppEnum, E_INVALIDARG );
    *ppEnum = NULL;

    IfFailGo( GetModuleIter(&ModIter) );

    hr = S_FALSE;

    if ( nameMatch == nmCaseInsensitive)
    {
        while (ModIter.GetNext(&pmodule))
        {
            if (pmodule->FindTypesByNameCaseInsensitive( pszClassName,
                    &listField,
                    this ) )
            {
                hr = S_OK;
            }
        }
    }
    else
    {
        while (ModIter.GetNext(&pmodule))
        {
            if (pmodule->FindTypesByName( pszClassName,
                                          &listField,
                                          this) )
            {
                hr = S_OK;
            }
        }
    }

    // If the list is empty then no type
    IfFalseGo( listField.GetCount(), E_FAIL );

    // Create enumerator
    IfFailGo( CreateEnumerator( ppEnum, &listField ) );

Error:

    METHOD_EXIT( CDebugSymbolProvider::GetTypesByName, hr );

    return hr;
}
```

## <a name="see-also"></a>Confira também
- [IDebugComPlusSymbolProvider2](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2.md)
