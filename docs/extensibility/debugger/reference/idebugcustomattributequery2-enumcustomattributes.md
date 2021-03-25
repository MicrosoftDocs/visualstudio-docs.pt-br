---
description: Obtém um enumerador para todos os atributos personalizados anexados a este campo.
title: 'IDebugCustomAttributeQuery2:: EnumCustomAttributes | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttributeQuery2::EnumCustomAttributes
helpviewer_keywords:
- IDebugCustomAttributeQuery2::EnumCustomAttributes
ms.assetid: 94bfce74-aa3d-45f0-8e04-5715faf85217
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5bcd11f3058de191a3b0a77f0316afb6140769fc
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077636"
---
# <a name="idebugcustomattributequery2enumcustomattributes"></a>IDebugCustomAttributeQuery2::EnumCustomAttributes
Obtém um enumerador para todos os atributos personalizados anexados a este campo.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT EnumCustomAttributes( 
   IEnumDebugCustomAttributes** ppEnum
);
```

```csharp
int EnumCustomAttributes(
   out IEnumDebugCustomAttributes ppEnum
);
```

## <a name="parameters"></a>Parâmetros
`ppEnum`\
fora Retorna um objeto [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md) que representa a lista de atributos personalizados; caso contrário, retornará um valor nulo se não houver nenhum atributo personalizado.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK ou S_FALSE se não houver nenhum atributo personalizado nesse campo. Caso contrário, retorna um código de erro;

## <a name="remarks"></a>Comentários
 Um campo pode ter vários atributos personalizados.

## <a name="see-also"></a>Confira também
- [IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)
- [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)
