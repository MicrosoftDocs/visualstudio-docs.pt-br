---
title: IDebugComPlusSymbolProvider::GetAttributedClassesForLanguage | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetAttributedClassesForLanguage
- IDebugComPlusSymbolProvider::GetAttributedClassesForLanguage
ms.assetid: e5b1b8b6-52a6-4ade-9a36-644abfa9f4b2
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 10d25cb9e58ac3eb38282a3ef2a2f631b6ba0e66
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/22/2019
ms.locfileid: "56706230"
---
# <a name="idebugcomplussymbolprovidergetattributedclassesforlanguage"></a>IDebugComPlusSymbolProvider::GetAttributedClassesForLanguage
Recupera as classes com o atributo especificado que são implementadas na linguagem de programação especificada.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetAttributedClassesForLanguage (
    GUID               guidLanguage,
    LPOLESTR           pstrAttribute,
    IEnumDebugFields** ppEnum
);
```

```csharp
int GetAttributedClassesForLanguage (
    Guid                 guidLanguage,
    string               pstrAttribute,
    out IEnumDebugFields ppEnum
);
```

#### <a name="parameters"></a>Parâmetros
`guidLanguage`

 [in] Identificador exclusivo para o idioma.

`pstrAttribute`

 [in] A cadeia de caracteres do atributo.

`ppEnum`

 [out] Retorna uma enumeração das classes de atributos.

## <a name="return-value"></a>Valor de retorno
Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.

## <a name="example"></a>Exemplo
O exemplo a seguir mostra como implementar esse método para um **CDebugSymbolProvider** objeto que expõe a [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md) interface.

```cpp
HRESULT CDebugSymbolProvider::GetAttributedClassesForLanguage(
    GUID guidLanguage,
    __in_z LPOLESTR pstrAttribute,
    IEnumDebugFields** ppEnum
)
{
    HRESULT hr = S_OK;
    CFieldList listFields;
    CModIter ModIter;
    CModule* pModule; // the iterator owns the reference
    ULONG cClasses = 0;
    DWORD iTypeDef = 0;
    mdTypeDef* rgTypeDefs = NULL;
    IDebugField** rgFields = NULL;
    DWORD ctField = 0;
    CEnumDebugFields* pEnumFields = NULL;

    ASSERT(IsValidObjectPtr(this, CDebugSymbolProvider));
    ASSERT(IsValidWritePtr(ppEnum, IEnumDebugFields*));

    METHOD_ENTRY( CDebugSymbolProvider::GetAttributedClassesForLanguage );

    IfFalseGo( ppEnum, E_INVALIDARG );
    *ppEnum = NULL;

    // For Each Module - call EnumFields
    IfFailGo( GetModuleIter(&ModIter) );

    // Find the Max number of classes
    while (ModIter.GetNext(&pModule))
    {
        CComPtr<IMetaDataImport> pMetaData;
        HCORENUM hEnum = 0;
        ULONG cTypeDefs;
        ULONG cEnum;

        pModule->GetMetaData( &pMetaData );

        IfFailGo( pMetaData->EnumTypeDefs( &hEnum,
                                           NULL,
                                           0,
                                           &cTypeDefs ) );
        IfFailGo( pMetaData->CountEnum( hEnum, &cEnum ) );
        cClasses += cEnum;
    }

    IfNullGo( rgTypeDefs = new mdTypeDef[cClasses], E_OUTOFMEMORY );
    IfNullGo( rgFields = new IDebugField * [cClasses], E_OUTOFMEMORY );

    ModIter.Reset();

    // Create the classes
    while (ModIter.GetNext(&pModule))
    {
        CComPtr<IMetaDataImport> pMetaData;
        HCORENUM hEnum = 0;
        ULONG cTypeDefs;
        ULONG cEnum;
        const void* pUnused;
        ULONG cbUnused;

        pModule->GetMetaData( &pMetaData );

        IfFailGo( pMetaData->EnumTypeDefs( &hEnum,
                                           NULL,
                                           0,
                                           &cTypeDefs ) );
        IfFailGo( pMetaData->CountEnum( hEnum, &cEnum ) );
        IfFailGo( pMetaData->EnumTypeDefs( &hEnum,
                                           rgTypeDefs,
                                           cEnum,
                                           &cTypeDefs ) );

        pMetaData->CloseEnum(hEnum);
        hEnum = NULL;

        for ( iTypeDef = 0; iTypeDef < cTypeDefs; iTypeDef++)
        {

            if (pMetaData->GetCustomAttributeByName( rgTypeDefs[iTypeDef],
                    pstrAttribute,
                    &pUnused,
                    &cbUnused ) == S_OK)
            {
                // Only return classes implemeted in the correct language

                if (pModule->ClassImplementedInLanguage( rgTypeDefs[iTypeDef],
                        guidLanguage) )
                {
                    if (CreateClassType( pModule->GetID(),
                                         rgTypeDefs[iTypeDef],
                                         rgFields + ctField) == S_OK)
                    {
                        ctField++;
                    }
                    else
                    {
                        ASSERT(!"Failed to Create Attributed Class");
                    }
                }
            }
        }
    }

    IfNullGo( pEnumFields = new CEnumDebugFields, E_OUTOFMEMORY );
    IfFailGo( pEnumFields->Initialize(rgFields, ctField) );
    IfFailGo( pEnumFields->QueryInterface( __uuidof(IEnumDebugFields),
                                           (void**) ppEnum ) );

Error:

    METHOD_EXIT( CDebugSymbolProvider::GetAttributedClassesForLanguage, hr );

    DELETERG( rgTypeDefs );

    for ( iTypeDef = 0; iTypeDef < ctField; iTypeDef++)
    {
        RELEASE( rgFields[iTypeDef] );
    }

    DELETERG( rgFields );
    RELEASE( pEnumFields );

    return hr;
}
```

## <a name="see-also"></a>Consulte também
- [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)
