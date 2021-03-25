---
description: Cria um enumerador para todas as variáveis locais do método, incluindo aquelas geradas internamente por um compilador.
title: 'IDebugMethodField:: EnumAllLocals | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumAllLocals
helpviewer_keywords:
- IDebugMethodField::EnumAllLocals method
ms.assetid: 0bc7cc13-2628-4bd8-8c06-4d2aa6755ea8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 021dd54157a46e35c0acbb7dd7315fe155304b6d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076687"
---
# <a name="idebugmethodfieldenumalllocals"></a>IDebugMethodField::EnumAllLocals
Cria um enumerador para todas as variáveis locais do método, incluindo aquelas geradas internamente por um compilador.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT EnumAllLocals( 
   IDebugAddress*     pAddress,
   IEnumDebugFields** ppLocals
);
```

```csharp
int EnumAllLocals(
   IDebugAddress        pAddress,
   out IEnumDebugFields ppLocals
);
```

## <a name="parameters"></a>Parâmetros
`pAddress`\
no Um objeto [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) que representa um endereço de depuração dentro do método, apontando para um escopo ou contexto específico.

`ppLocals`\
fora Retorna um objeto [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) que representa a lista de todos os locais no escopo especificado; caso contrário, retorna um valor nulo que indica nenhum local.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK ou retornará S_FALSE se não houver nenhum local. Caso contrário, retornará um código de erro.

## <a name="remarks"></a>Comentários
 Somente as variáveis definidas no bloco que contém o endereço de depuração fornecido são enumeradas. Esse método inclui qualquer local gerado pelo compilador. Se tudo o que for necessário são os locais explicitamente definidos na origem, chame o método [EnumLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md) .

 Um método pode conter vários blocos ou contextos de escopo.

## <a name="see-also"></a>Confira também
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [EnumLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)
