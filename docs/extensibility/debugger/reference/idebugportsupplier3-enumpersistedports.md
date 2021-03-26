---
description: Esse método recupera um objeto que permite a enumeração da lista de portas persistentes.
title: 'IDebugPortSupplier3:: EnumPersistedPorts | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier3::EnumPersistedPorts
helpviewer_keywords:
- IDebugPortSupplier3::EnumPersistedPorts
ms.assetid: 1c3dead3-5d6c-4067-8418-4015f0b0dd07
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b4fe55898f6dbc7713db6e013868b1c7f22a5faf
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071955"
---
# <a name="idebugportsupplier3enumpersistedports"></a>IDebugPortSupplier3::EnumPersistedPorts
Esse método recupera um objeto que permite a enumeração da lista de portas persistentes.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT EnumPersistedPorts(
   BSTR_ARRAY         PortNames,
   IEnumDebugPorts2** ppEnum
);
```

```csharp
int EnumPersistedPorts(
   BSTR_ARRAY           PortNames,
   out IEnumDebugPorts2 ppEnum
);
```

## <a name="parameters"></a>Parâmetros
`PortNames`\
no Uma estrutura de [BSTR_ARRAY](../../../extensibility/debugger/reference/bstr-array.md) que contém uma lista de nomes de porta para localizar e retornar entre as portas persistentes. Somente as portas persistentes com esses nomes serão retornadas.

`ppEnum`\
fora Um objeto que implementa a interface [IEnumDebugPorts2](../../../extensibility/debugger/reference/ienumdebugports2.md) .

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 As portas persistentes são carregadas quando um fornecedor de porta é instanciado e salvo quando o fornecedor da porta é destruído.

## <a name="see-also"></a>Confira também
- [IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md)
- [IEnumDebugPorts2](../../../extensibility/debugger/reference/ienumdebugports2.md)
- [BSTR_ARRAY](../../../extensibility/debugger/reference/bstr-array.md)
