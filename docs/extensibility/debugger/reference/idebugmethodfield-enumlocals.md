---
title: 'IDebugMethodField:: EnumLocals | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumLocals
helpviewer_keywords:
- IDebugMethodField::EnumLocals method
ms.assetid: b0456a6d-2b96-49e2-a871-516571b4f6a5
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 98d6d7c4d9f1df0c7c4346792d841de574859619
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99861147"
---
# <a name="idebugmethodfieldenumlocals"></a>IDebugMethodField::EnumLocals
Cria um enumerador para as variáveis locais selecionadas do método.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT EnumLocals(
    IDebugAddress*     pAddress,
    IEnumDebugFields** ppLocals
);
```

```csharp
int EnumLocals(
    IDebugAddress        pAddress,
    out IEnumDebugFields ppLocals
);
```

## <a name="parameters"></a>Parâmetros
`pAddress`\
no Um objeto [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) que representa o endereço de depuração que seleciona o contexto ou o escopo do qual obter os locais.

`ppLocals`\
fora Retorna um objeto [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) que representa uma lista de locais; caso contrário, retornará um valor nulo se não houver nenhum local.

## <a name="return-value"></a>Valor retornado
Se for bem-sucedido, retornará S_OK ou retornará S_FALSE se não houver nenhum local. Caso contrário, retornará um código de erro.

## <a name="remarks"></a>Comentários
Somente as variáveis definidas no bloco que contém o endereço de depuração fornecido são enumeradas. Se todos os locais, incluindo qualquer local gerado pelo compilador, forem necessários, chame o método [EnumAllLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumalllocals.md) .

Um método pode conter vários blocos ou contextos de escopo. Por exemplo, o seguinte método forçado contém três escopos, os dois blocos internos e o próprio corpo do método.

```csharp
public void func(int index)
{
    // Method body scope
    int a = 0;
    if (index == 1)
    {
        // Inner scope 1
        int temp1 = a;
    }
    else
    {
        // Inner scope 2
        int temp2 = a;
    }
}
```

O objeto [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md) representa o `func` próprio método. Chamar o `EnumLocals` método com um [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) definido como o `Inner Scope 1` endereço retorna uma enumeração que contém a `temp1` variável, por exemplo.

## <a name="see-also"></a>Consulte também
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [EnumAllLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumalllocals.md)
