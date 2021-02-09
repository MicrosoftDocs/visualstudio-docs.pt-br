---
title: 'IDebugMethodField:: EnumAllLocals | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumAllLocals
helpviewer_keywords:
- IDebugMethodField::EnumAllLocals method
ms.assetid: 0bc7cc13-2628-4bd8-8c06-4d2aa6755ea8
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c10de4db63a7706326ff6f387366c75f860408bf
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99928153"
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

## <a name="return-value"></a>Valor retornado
 Se for bem-sucedido, retornará S_OK ou retornará S_FALSE se não houver nenhum local. Caso contrário, retornará um código de erro.

## <a name="remarks"></a>Comentários
 Somente as variáveis definidas no bloco que contém o endereço de depuração fornecido são enumeradas. Esse método inclui qualquer local gerado pelo compilador. Se tudo o que for necessário são os locais explicitamente definidos na origem, chame o método [EnumLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md) .

 Um método pode conter vários blocos ou contextos de escopo.

## <a name="see-also"></a>Confira também
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [EnumLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)
