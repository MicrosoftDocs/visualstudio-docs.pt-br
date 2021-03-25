---
description: Cria um enumerador para os parâmetros do método.
title: 'IDebugMethodField:: EnumParameters | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumParameters
helpviewer_keywords:
- IDebugMethodField::EnumParameters method
ms.assetid: d77b1197-deb6-4144-8d1b-8b09949ccfac
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0f2085b6a2aff6b41456f47a01c446b1c646f353
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058385"
---
# <a name="idebugmethodfieldenumparameters"></a>IDebugMethodField::EnumParameters
Cria um enumerador para os parâmetros do método.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT EnumParameters( 
   IEnumDebugFields** ppParams
);
```

```csharp
int EnumParameters(
   out IEnumDebugFields ppParams
);
```

## <a name="parameters"></a>Parâmetros
`ppParams`\
fora Retorna um objeto [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) que representa a lista de parâmetros para o método; caso contrário, retornará um valor nulo se não houver parâmetros.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK ou retornará S_FALSE se não houver parâmetros. Caso contrário, retornará um código de erro.

## <a name="remarks"></a>Comentários
 Cada elemento é um objeto [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) que representa diferentes tipos de parâmetros. Chame o método [getkind](../../../extensibility/debugger/reference/idebugfield-getkind.md) em cada objeto para determinar exatamente que tipo de parâmetro o objeto representa.

 Um parâmetro inclui o seu nome de variável e seu tipo. O primeiro parâmetro para um método de classe normalmente é o ponteiro "This".

 Se apenas os tipos dos parâmetros forem necessários, chame o método [EnumArguments](../../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md) .

## <a name="see-also"></a>Confira também
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [EnumArguments](../../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)
