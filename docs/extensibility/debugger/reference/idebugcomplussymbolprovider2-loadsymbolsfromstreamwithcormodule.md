---
title: IDebugComPlusSymbolProvider2::LoadSymbolsFromStreamWithCorModule
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider2::LoadSymbolsFromStreamWithCorModule
- LoadSymbolsFromStreamWithCorModule
ms.assetid: f79b894f-52c4-43c2-9a68-c71536451f6c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fa1d03b2f91cea03403f4893e61ec15bf5b82952
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80733392"
---
# <a name="idebugcomplussymbolprovider2loadsymbolsfromstreamwithcormodule"></a>IDebugComPlusSymbolProvider2::LoadSymbolsFromStreamWithCorModule
Carregar símbolos de depuração de um fluxo de dados dado o objeto **ICorDebugModule.**

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT LoadSymbolsFromStreamWithCorModule(
    ULONG32   ulAppDomainID,
    GUID      guidModule,
    ULONGLONG baseAddress,
    IUnknown* pUnkMetadataImport,
    IUnknown* pUnkCorDebugModule,
    IStream*  pStream
);
```

```csharp
int LoadSymbolsFromStreamWithCorModule(
    uint    ulAppDomainID,
    Guid    guidModule,
    ulong   baseAddress,
    object  pUnkMetadataImport,
    object  pUnkCorDebugModule,
    IStream pStream
);
```

## <a name="parameters"></a>parâmetros
`ulAppDomainID`\
[em] Identificador do domínio do aplicativo.

`guidModule`\
[em] Identificador único do módulo.

`baseAddress`\
[em] Endereço de memória base.

`pUnkMetadataImport`\
[em] Objeto que contém os metadados do símbolo.

`pUnkCorDebugModule`\
[em] Objeto que implementa a [interface ICorDebugModule](/dotnet/framework/unmanaged-api/debugging/icordebugmodule-interface).

`pStream`\
[em] Fluxo de dados que contém os símbolos de depuração a serem carregados.

## <a name="return-value"></a>Valor retornado
Se for `S_OK`bem sucedido, retorna; caso contrário, retorna um código de erro.

## <a name="example"></a>Exemplo
O exemplo a seguir mostra como implementar esse método para um objeto **CDebugSymbolProvider** que expõe a interface [IDebugComPlusSymbolProvider2.](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2.md)

```cpp
HRESULT CDebugSymbolProvider::LoadSymbolsFromStreamWithCorModule(
    ULONG32 ulAppDomainID,
    GUID guidModule,
    ULONGLONG baseOffset,
    IUnknown* pUnkMetadataImport,
    IUnknown* pUnkCorDebugModule,
    IStream* pStream
)
{
    CAutoLock Lock(this);

    HRESULT hr = S_OK;
    CComPtr<IMetaDataImport> pMetadata;
    CComPtr<ICorDebugModule> pCorModule;

    CModule* pmodule = NULL;
    CModule* pmoduleNew = NULL;
    bool fAlreadyLoaded = false;
    Module_ID idModule(ulAppDomainID, guidModule);
    DWORD dwCurrentState = 0;

    ASSERT(IsValidObjectPtr(this, CDebugSymbolProvider));
    ASSERT(IsValidInterfacePtr(pUnkMetadataImport, IUnknown));

    METHOD_ENTRY( CDebugSymbolProvider::LoadSymbolsFromStream );

    IfFalseGo( pUnkMetadataImport, E_INVALIDARG );
    IfFalseGo( pUnkCorDebugModule, E_INVALIDARG );

    IfFailGo( pUnkMetadataImport->QueryInterface( IID_IMetaDataImport,
              (void**)&pMetadata) );

    IfFailGo( pUnkCorDebugModule->QueryInterface( IID_ICorDebugModule,
              (void**)&pCorModule) );

    ASSERT(guidModule != GUID_NULL);

    fAlreadyLoaded = GetModule( idModule, &pmodule ) == S_OK;

    IfNullGo( pmoduleNew = new CModule, E_OUTOFMEMORY );

    dwCurrentState = m_pSymProvGroup ? m_pSymProvGroup->GetCurrentState() : 0;

    IfFailGo( pmoduleNew->Create( idModule,
                                  dwCurrentState,
                                  pMetadata,
                                  pCorModule,
                                  pStream,
                                  baseOffset ) );

    if (fAlreadyLoaded)
    {
        IfFailGo(pmoduleNew->AddEquivalentModulesFrom(pmodule));
        RemoveModule(pmodule);
    }

    IfFailGo( AddModule( pmoduleNew ) );

Error:

    RELEASE (pmodule);
    RELEASE (pmoduleNew);

    METHOD_EXIT( CDebugSymbolProvider::LoadSymbolsFromStream, hr );

    return hr;
}
```

## <a name="see-also"></a>Confira também
- [IDebugComPlusSymbolProvider2](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2.md)
