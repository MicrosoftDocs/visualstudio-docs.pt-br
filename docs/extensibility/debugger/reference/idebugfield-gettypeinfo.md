---
description: Esse método obtém informações independentes de tipo sobre o símbolo ou tipo.
title: 'IDebugField:: GetTypeInfo | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::GetTypeInfo
helpviewer_keywords:
- IDebugField::GetTypeInfo method
ms.assetid: bb5acfa3-04c3-4088-be84-9ff8926cd16f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9ea120cb58faa28bbb8168800ef6e35f707d879f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073697"
---
# <a name="idebugfieldgettypeinfo"></a>IDebugField::GetTypeInfo
Esse método obtém informações independentes de tipo sobre o símbolo ou tipo.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetTypeInfo( 
   TYPE_INFO* pTypeInfo
);
```

```csharp
int GetTypeInfo(
   TYPE_INFO[] pTypeInfo
);
```

## <a name="parameters"></a>Parâmetros
`pTypeInfo`\
fora Retorna informações de tipo na estrutura de [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md) fornecida.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 As informações independentes de tipo incluem, por exemplo, AppDomain, o módulo e a classe que contém o símbolo.

## <a name="see-also"></a>Confira também
- [GetType](../../../extensibility/debugger/reference/idebugfield-gettype.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)
