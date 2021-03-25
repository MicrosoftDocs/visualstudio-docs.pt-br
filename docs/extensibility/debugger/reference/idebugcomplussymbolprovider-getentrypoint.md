---
description: Recupera o ponto de entrada do aplicativo.
title: 'IDebugComPlusSymbolProvider:: getentrypoint | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider::GetEntryPoint
- GetEntryPoint
ms.assetid: 9640e121-1da1-41f9-8e66-76efca36baf2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 60c05683bae7845c852b954ed330b26557504fd6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058840"
---
# <a name="idebugcomplussymbolprovidergetentrypoint"></a>IDebugComPlusSymbolProvider::GetEntryPoint
Recupera o ponto de entrada do aplicativo.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetEntryPoint(
    ULONG32         ulAppDomainID,
    GUID            guidModule,
    IDebugAddress** ppAddress
);
```

```csharp
int GetEntryPoint(
    uint              ulAppDomainID,
    Guid              guidModule,
    out IDebugAddress ppAddress
);
```

## <a name="parameters"></a>Parâmetros
`ulAppDomainID`\
no Identificador para o domínio do aplicativo.

`guidModule`\
no Identificador exclusivo do módulo.

`ppAddress`\
fora Retorna o ponto de entrada representado por uma interface [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) .

## <a name="return-value"></a>Valor Retornado
Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="example"></a>Exemplo
O exemplo a seguir mostra como implementar esse método para um objeto **CDebugSymbolProvider** que expõe a interface [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md) .

```cpp
HRESULT CDebugSymbolProvider::GetEntryPoint(
    ULONG32 ulAppDomainID,
    GUID guidModule,
    IDebugAddress **ppAddress
)
{
    HRESULT hr = S_OK;
    CComPtr<CModule> pModule;
    Module_ID idModule(ulAppDomainID, guidModule);

    ASSERT(IsValidObjectPtr(this, CDebugSymbolProvider));
    ASSERT(IsValidWritePtr(ppAddress, IDebugAddress *));

    METHOD_ENTRY( CDebugSymbolProvider::GetEntryPoint );

    IfFalseGo( ppAddress, E_INVALIDARG );

    *ppAddress = NULL;

    IfFailGo( GetModule( idModule, &pModule) );

    IfFailGo( pModule->GetEntryPoint( ppAddress ) );

Error:

    METHOD_EXIT( CDebugSymbolProvider::GetEntryPoint, hr );

    return hr;
}
```

## <a name="see-also"></a>Confira também
- [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)
