---
description: Recupera a cadeia de caracteres associada a essa propriedade e a armazena em um buffer fornecido pelo usuário.
title: 'IDebugProperty3:: GetStringChars | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3::GetStringChars
helpviewer_keywords:
- IDebugProperty3::GetStringChars
ms.assetid: 832c37f3-85cb-4227-8ab2-f27a80eafe90
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d3b220fa02809015d1fa699c5e9eb5edac8cf2f3
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102166678"
---
# <a name="idebugproperty3getstringchars"></a>IDebugProperty3::GetStringChars
Recupera a cadeia de caracteres associada a essa propriedade e a armazena em um buffer fornecido pelo usuário.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetStringChars(
    ULONG  buflen,
    WCHAR* rgString,
    ULONG* pceltFetched
);
```

```csharp
int GetStringChars(
    uint       buflen,
    out string rgString,
    out uint   pceltFetched
);
```

## <a name="parameters"></a>Parâmetros
`buflen`\
no Número máximo de caracteres que o buffer fornecido pelo usuário pode conter.

`rgString`\
fora Retorna a cadeia de caracteres.

 [C++ Only], `rgString` é um ponteiro para um buffer que recebe os caracteres Unicode da cadeia de caracteres. Esse buffer deve ter pelo menos `buflen` caracteres (não bytes) de tamanho.

`pceltFetched`\
fora Em que o número de caracteres realmente armazenados no buffer é retornado. (Pode estar `NULL` em C++.)

## <a name="return-value"></a>Valor Retornado
Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
Em C++, deve-se ter cuidado para garantir que o buffer tenha pelo menos `buflen` caracteres Unicode de comprimento. Observe que um caractere Unicode tem 2 bytes de comprimento.

> [!NOTE]
> Em C++, a cadeia de caracteres retornada não inclui um caractere nulo de terminação. Se for especificado, `pceltFetched` especificará o número de caracteres na cadeia de caracteres.

## <a name="example"></a>Exemplo

```cpp
CStringW RetrievePropertyString(IDebugProperty2 *pPropInfo)
{
    CStringW returnString = L"";
    CComQIPtr<IDebugProperty3> pProp3 = pPropInfo->pProperty;
    If (pProp3 != NULL) {
        ULONG dwStrLen = 0;
        HRESULT hr;
        hr = pProp3->GetStringCharLength(&dwStrLen);
        if (SUCCEEDED(hr) && dwStrLen > 0) {
            ULONG dwRead;
            CStrBufW buf(returnString,dwStrLen,CStrBuf::SET_LENGTH);
            hr = pProp3->GetStringChars(dwStrLen,
                                        reinterpret_cast<WCHAR*>(static_cast<CStringW::PXSTR>(buf)),
                                        &dwRead);
        }
    }
    return(returnString);
}
```

## <a name="see-also"></a>Confira também
- [GetStringCharLength](../../../extensibility/debugger/reference/idebugproperty3-getstringcharlength.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
