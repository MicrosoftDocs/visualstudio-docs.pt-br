---
description: 'IDebugProgramNode2:: getprogramname Obtém o nome do programa.'
title: 'IDebugProgramNode2:: getprogramaname | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::GetProgramName
helpviewer_keywords:
- IDebugProgramNode2::GetProgramName
ms.assetid: 510c7f5d-48ff-4d9f-ad79-fbad9f15239d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 88a4bc58f5d91cdb52482f4dc862446cfc9e7eb1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102161379"
---
# <a name="idebugprogramnode2getprogramname"></a>IDebugProgramNode2::GetProgramName
Obtém o nome do programa.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetProgramName (
    BSTR* pbstrProgramName
);
```

```csharp
int GetProgramName (
    out string pbstrProgramName
);
```

## <a name="parameters"></a>Parâmetros
`pbstrProgramName`\
fora Retorna o nome do programa.

## <a name="return-value"></a>Valor Retornado
Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
O nome de um programa não é a mesma coisa que o caminho para o programa, embora o nome do programa possa fazer parte desse caminho.

## <a name="example"></a>Exemplo
O exemplo a seguir mostra como implementar esse método para um `CProgram` objeto simples que implementa a interface [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) . A `MakeBstr` função aloca uma cópia da cadeia de caracteres especificada como um BSTR.

```cpp
HRESULT CProgram::GetProgramName(BSTR* pbstrProgramName) {
    if (!pbstrProgramName)
        return E_INVALIDARG;

    // Assign the member program name to the passed program name.
    *pbstrProgramName = MakeBstr(m_pszProgramName);
    return NOERROR;
}
```

## <a name="see-also"></a>Confira também
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
