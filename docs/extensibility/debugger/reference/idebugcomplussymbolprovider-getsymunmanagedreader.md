---
title: 'IDebugComPlusSymbolProvider:: GetSymUnmanagedReader | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider::GetSymUnmanagedReader
- GetSymUnmanagedReader
ms.assetid: 8f1c1627-217f-4405-8141-7a2eb80310a5
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4463085b021f2de5f9237817b6d8ffade88612a5
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99936152"
---
# <a name="idebugcomplussymbolprovidergetsymunmanagedreader"></a>IDebugComPlusSymbolProvider::GetSymUnmanagedReader
Recupera o leitor de símbolos a ser usado pelo código não gerenciado.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetSymUnmanagedReader(
    ULONG32    ulAppDomainID,
    GUID       guidModule,
    IUnknown** ppSymUnmanagedReader
);
```

```csharp
int GetSymUnmanagedReader(
    uint       ulAppDomainID,
    Guid       guidModule,
    out object ppSymUnmanagedReader
);
```

## <a name="parameters"></a>Parâmetros
`ulAppDomainID`\
no Identificador do domínio do aplicativo.

`guidModule`\
no Identificador exclusivo do módulo.

`ppSymUnmanagedReader`\
fora Retorna o objeto que representa o leitor de símbolo.

## <a name="return-value"></a>Valor retornado
Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="example"></a>Exemplo
O exemplo a seguir mostra como implementar esse método para um objeto **CDebugSymbolProvider** que expõe a interface [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md) .

```cpp
HRESULT CDebugSymbolProvider::GetSymUnmanagedReader(
    ULONG32 ulAppDomainID,
    GUID guidModule,
    IUnknown ** ppSymUnmanagedReader
)
{
    HRESULT hr = S_OK;
    CComPtr<CModule> pModule;
    Module_ID idModule(ulAppDomainID, guidModule);

    METHOD_ENTRY( CDebugSymbolProvider::GetSymUnmanagedReader );

    IfFailGo( GetModule( idModule, &pModule ) );
    IfFailGo( pModule->GetSymReader((ISymUnmanagedReader**) ppSymUnmanagedReader) );

Error:

    METHOD_EXIT( CDebugSymbolProvider::GetSymUnmanagedReader, hr );
    return hr;
}
```

## <a name="see-also"></a>Confira também
- [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)
