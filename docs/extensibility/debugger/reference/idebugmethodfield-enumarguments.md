---
description: Cria um enumerador para o tipo de cada argumento necessário para chamar o método.
title: 'IDebugMethodField:: EnumArguments | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumArguments
helpviewer_keywords:
- IDebugMethodField::EnumArguments method
ms.assetid: 3ab55488-2437-4ff6-a9ae-78ea6d7b23a8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3ba48eb4d98c1ab331ee898a219584b7a4b6cf1c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058411"
---
# <a name="idebugmethodfieldenumarguments"></a>IDebugMethodField::EnumArguments
Cria um enumerador para o tipo de cada argumento necessário para chamar o método.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT EnumArguments( 
   IEnumDebugFields** ppParams
);
```

```csharp
int EnumArguments(
   out IEnumDebugFields ppParams
);
```

## <a name="parameters"></a>Parâmetros
`ppParams`\
fora Retorna um objeto [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) que representa a lista de tipos de argumento. Retorna um valor nulo se não houver argumentos.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK ou retornará S_FALSE se não houver argumentos. Caso contrário, retornará um código de erro.

## <a name="remarks"></a>Comentários
 Cada elemento é um objeto [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) que representa os tipos de cada parâmetro. Chame o método [GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md) para recuperar informações sobre o tipo de cada parâmetro.

 Se o nome do parâmetro for necessário junto com o tipo, chame o método [EnumParameters](../../../extensibility/debugger/reference/idebugmethodfield-enumparameters.md) .

## <a name="see-also"></a>Confira também
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [EnumParameters](../../../extensibility/debugger/reference/idebugmethodfield-enumparameters.md)
