---
title: IDebugComPlusSymbolProvider::UpdateSymbols | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- UpdateSymbols
- IDebugComPlusSymbolProvider::UpdateSymbols
ms.assetid: d530f6f1-4af2-454b-bab0-02478a8fe81e
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c6c3c396dbea0e005012162080590a0b84ec9f5b
ms.sourcegitcommit: 7153e2fc717d32e0e9c8a9b8c406dc4053c9fd53
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/19/2019
ms.locfileid: "56413287"
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

#### <a name="parameters"></a>Parâmetros
`ulAppDomainID`  
[in] Identificador do domínio do aplicativo.

`guidModule`  
[in] Identificador exclusivo do módulo.

`pUpdateStream`  
[in] Fluxo de dados que contém os símbolos de depuração atualizado.

## <a name="example"></a>Exemplo
O exemplo a seguir mostra como implementar esse método para um **CDebugSymbolProvider** objeto que expõe a [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md) interface.

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

## <a name="return-value"></a>Valor de retorno
Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Consulte também
[IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)
