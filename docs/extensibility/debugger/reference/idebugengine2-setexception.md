---
description: Especifica como o mecanismo de depuração (DE) deve tratar uma determinada exceção.
title: 'IDebugEngine2:: SetException | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::SetException
helpviewer_keywords:
- IDebugEngine2::SetException
ms.assetid: e6f5ec48-09e8-4b9b-9dc9-55f8d883f1b7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3a327620ed9eddbba71f84c9950185f7987e8a79
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087906"
---
# <a name="idebugengine2setexception"></a>IDebugEngine2::SetException
Especifica como o mecanismo de depuração (DE) deve tratar uma determinada exceção.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT SetException( 
   EXCEPTION_INFO* pException
);
```

```csharp
int SetException( 
   EXCEPTION_INFO[] pException
);
```

## <a name="parameters"></a>Parâmetros
`pException`\
no Uma estrutura de [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md) que descreve a exceção e como depurá-la.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Um DE pode ser instruído a parar o programa que gera uma exceção na primeira chance, segunda chance ou não.

## <a name="see-also"></a>Confira também
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)
