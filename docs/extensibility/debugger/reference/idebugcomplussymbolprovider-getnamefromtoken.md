---
title: 'IDebugComPlusSymbolProvider:: GetNameFromToken | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider::GetNameFromToken
- GetNameFromToken
ms.assetid: 6e8cf468-5fd1-4655-93ed-88828d6068b7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 544bb2ed8a5526c04c46c6609c6bca3b6bf57bdf
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "80733784"
---
# <a name="idebugcomplussymbolprovidergetnamefromtoken"></a>IDebugComPlusSymbolProvider::GetNameFromToken
Retorna o nome associado ao token especificado, dado seu objeto de metadados.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetNameFromToken (
    IUnknown* pMetadataImport,
    DWORD     dwToken,
    BSTR*     pbstrName
);
```

```csharp
int GetNameFromToken (
    object     pMetadataImport,
    uint       dwToken,
    out string pbstrName
);
```

## <a name="parameters"></a>Parâmetros
`pMetadataImport`\
no Objeto que contém as informações de metadados.

`dwToken`\
no Token a ser nomeado.

`pbstrName`\
fora Nome que corresponde ao token.

## <a name="return-value"></a>Valor Retornado
Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="example"></a>Exemplo
O exemplo a seguir mostra como implementar esse método para um objeto **CDebugSymbolProvider** que expõe a interface [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md) .

```cpp
HRESULT CDebugSymbolProvider::GetNameFromToken(
    IUnknown* pMetadataImport,
    DWORD dwToken,
    BSTR* pbstrName
)
{
    HRESULT hr = S_OK;
    CComPtr<IMetaDataImport> pMetaData;

    ASSERT(IsValidObjectPtr(this, CDebugSymbolProvider));
    ASSERT(IsValidInterfacePtr(pMetadataImport, IUnknown));

    METHOD_ENTRY(CDebugSymbolProvider::GetNameFromToken);

    IfFalseGo( pMetadataImport && pbstrName, E_INVALIDARG );

    *pbstrName = NULL;
    IfFailGo( pMetadataImport->QueryInterface( IID_IMetaDataImport,
              (void**) &pMetaData ) );

    switch ( TypeFromToken(dwToken) )
    {
        case mdtModule:
            IfFailGo( GetModuleName( pMetaData, dwToken, pbstrName) );
            break;

        case mdtTypeDef:
            IfFailGo( GetTypeName( pMetaData, dwToken, pbstrName) );
            break;

        case mdtFieldDef:
            IfFailGo( GetFieldName( pMetaData, dwToken, pbstrName) );
            break;

        case mdtMethodDef:
            IfFailGo( GetMethodName( pMetaData, dwToken, pbstrName) );
            break;

        case mdtEvent:
            IfFailGo( GetEventName( pMetaData, dwToken, pbstrName) );
            break;

        case mdtProperty:
            IfFailGo( GetPropertyName( pMetaData, dwToken, pbstrName) );
            break;

        case mdtAssembly:
            IfFailGo( GetAssemblyName( pMetaData, dwToken, pbstrName) );
            break;

        default:
            ASSERT(!"Unsupported token passed to GetNameFromToken");
            hr = E_FAIL;
            break;
    }

Error:

    METHOD_EXIT(CDebugSymbolProvider::GetNameFromToken, hr);
    return hr;
}
```

## <a name="see-also"></a>Confira também
- [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)
