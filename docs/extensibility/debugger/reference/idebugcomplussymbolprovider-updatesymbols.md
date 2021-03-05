---
description: Atualiza os símbolos de depuração na memória com aqueles do fluxo de dados especificado.
title: 'IDebugComPlusSymbolProvider:: UpdateSymbols | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- UpdateSymbols
- IDebugComPlusSymbolProvider::UpdateSymbols
ms.assetid: d530f6f1-4af2-454b-bab0-02478a8fe81e
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2d849ec9359055e6ff469ef49a50cf6c724eb4ca
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102163506"
---
# <a name="idebugcomplussymbolproviderupdatesymbols"></a>IDebugComPlusSymbolProvider::UpdateSymbols
Atualiza os símbolos de depuração na memória com aqueles do fluxo de dados especificado.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT UpdateSymbols (
    ULONG32  ulAppDomainID,
    GUID     guidModule,
    IStream* pUpdateStream
);
```

```csharp
int UpdateSymbols (
    uint    ulAppDomainID,
    Guid    guidModule,
    IStream pUpdateStream
);
```

## <a name="parameters"></a>Parâmetros
`ulAppDomainID`\
no Identificador do domínio do aplicativo.

`guidModule`\
no Identificador exclusivo do módulo.

`pUpdateStream`\
no Fluxo de dados que contém os símbolos de depuração atualizados.

## <a name="example"></a>Exemplo
O exemplo a seguir mostra como implementar esse método para um objeto **CDebugSymbolProvider** que expõe a interface [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md) .

```cpp
HRESULT CDebugSymbolProvider::UpdateSymbols(
    ULONG32 ulAppDomainID,
    GUID guidModule,
    IStream* pUpdateStream
)
{
    ASSERT(!"Use UpdateSymbols2 on IDebugENCSymbolProvider2");
    return E_NOTIMPL;
}

HRESULT CDebugSymbolProvider::UpdateSymbols2(
    ULONG32 ulAppDomainID,
    GUID guidModule,
    IStream* pUpdateStream,
    LINEDELTA* pDeltaLines,
    ULONG cDeltaLines
)
{
    HRESULT hr = S_OK;
    CComPtr<CModule> pModule;
    Module_ID idModule(ulAppDomainID, guidModule);

    METHOD_ENTRY( CDebugSymbolProvider::UpdateSymbols );

    IfFailGo( GetModule( idModule, &pModule ) );
    IfFailGo( pModule->UpdateSymbols( pUpdateStream, pDeltaLines, cDeltaLines ) );

Error:

    METHOD_EXIT( CDebugSymbolProvider::UpdateSymbols, hr );

    return hr;
}
```

## <a name="return-value"></a>Valor Retornado
Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)
