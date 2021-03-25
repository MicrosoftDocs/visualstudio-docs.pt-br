---
description: Recupera o endereço dentro de uma função que representa o deslocamento de linha fornecido.
title: 'IDebugComPlusSymbolProvider:: GetFunctionLineOffset | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider::GetFunctionLineOffset
- GetFunctionLineOffset
ms.assetid: 51460f5a-4e98-427a-8315-27246e24fb61
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ae212e00e6d49b54b0536147194317584fad2830
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058762"
---
# <a name="idebugcomplussymbolprovidergetfunctionlineoffset"></a>IDebugComPlusSymbolProvider::GetFunctionLineOffset
Recupera o endereço dentro de uma função que representa o deslocamento de linha fornecido.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetFunctionLineOffset(
    IDebugAddress*  pAddress,
    DWORD           dwLine,
    IDebugAddress** ppNewAddress
);
```

```csharp
int GetFunctionLineOffset(
    IDebugAddress     pAddress,
    uint              dwLine,
    out IDebugAddress ppNewAddress
);
```

## <a name="parameters"></a>Parâmetros
`pAddress`\
no Endereço que representa a função.

`dwLine`\
no Deslocamento de linha do início da função.

`ppNewAddress`\
fora Novo endereço que representa o deslocamento de linha do início da função.

## <a name="return-value"></a>Valor Retornado
Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="example"></a>Exemplo
O exemplo a seguir mostra como implementar esse método para um objeto **CDebugSymbolProvider** que expõe a interface [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md) .

```cpp
HRESULT CDebugSymbolProvider::GetFunctionLineOffset(
    IDebugAddress *pAddress,
    DWORD dwLine,
    IDebugAddress **ppNewAddress
)
{
    HRESULT hr = S_OK;
    CDEBUG_ADDRESS address;
    CComPtr<CModule> pModule;
    DWORD dwOffset;
    CDebugAddress* paddr = NULL;

    METHOD_ENTRY(CDebugSymbolProvider::GetFunctionLineOffset);

    IfFalseGo( pAddress, S_FALSE );
    IfFailGo( pAddress->GetAddress( &address ) );

    ASSERT(address.addr.dwKind == ADDRESS_KIND_METADATA_METHOD);
    IfFalseGo( address.addr.dwKind == ADDRESS_KIND_METADATA_METHOD, S_FALSE );

    IfFailGo( GetModule( address.GetModule(), &pModule) );

    // Find the first offset for dwLine in the function

    IfFailGo( pModule->GetFunctionLineOffset( address.addr.addr.addrMethod.tokMethod,
              address.addr.addr.addrMethod.dwVersion,
              dwLine,
              &dwOffset ) );

    // Create the new Address

    address.addr.addr.addrMethod.dwOffset = dwOffset;
    IfNullGo( paddr = new CDebugAddress(address), E_OUTOFMEMORY );
    IfFailGo( paddr->QueryInterface( __uuidof(IDebugAddress),
                                     (void**) ppNewAddress ) );

Error:

    METHOD_EXIT(CDebugSymbolProvider::GetFunctionLineOffset, hr);
    RELEASE( paddr );
    return hr;
}
```

## <a name="see-also"></a>Confira também
- [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)
