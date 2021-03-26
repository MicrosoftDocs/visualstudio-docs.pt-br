---
description: Obtém o campo ao qual o atributo personalizado está anexado.
title: 'IDebugCustomAttribute:: getparentfield | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttribute::GetParentField
helpviewer_keywords:
- IDebugCustomAttribute::GetParentField
ms.assetid: bcdfdf37-bfcf-4988-a7b8-4c731d0af1b0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7aaa3ea38e5ed0691b8e335a3d39a8a82b7576ef
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088049"
---
# <a name="idebugcustomattributegetparentfield"></a>IDebugCustomAttribute::GetParentField
Obtém o campo ao qual o atributo personalizado está anexado.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetParentField( 
   IDebugField** ppField
);
```

```csharp
int GetParentField(
   out IDebugField ppField
);
```

## <a name="parameters"></a>Parâmetros
`ppField`\
fora Retorna o objeto [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) que representa o campo ao qual o atributo personalizado está anexado.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Chame o método [getkind](../../../extensibility/debugger/reference/idebugfield-getkind.md) no objeto [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) retornado para determinar que tipo de campo o pai é.

## <a name="see-also"></a>Confira também
- [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
