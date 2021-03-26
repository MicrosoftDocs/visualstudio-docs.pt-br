---
description: Recupera o nome do contexto de avaliação.
title: 'IDebugExpressionContext2:: GetName | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionContext2::GetName
helpviewer_keywords:
- IDebugExpressionContext2::GetName
ms.assetid: c2b70d22-17af-4986-a7e3-930910367216
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c3aa27ba70e0b407e72a42d2904467ee85fc027b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105092313"
---
# <a name="idebugexpressioncontext2getname"></a>IDebugExpressionContext2::GetName
Recupera o nome do contexto de avaliação.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetName( 
   BSTR* pbstrName
);
```

```csharp
int GetName( 
   out string pbstrName
);
```

## <a name="parameters"></a>Parâmetros
`pbstrName`\
fora Retorna o nome do contexto de avaliação.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 O nome é a descrição deste contexto de avaliação. Normalmente, é algo que pode ser analisado por um avaliador de expressão que se refere a esse contexto de avaliação exato. Por exemplo, em C++, o nome é o seguinte:

```
"{ function-name, source-file-name, module-file-name }"
```

## <a name="see-also"></a>Confira também
- [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)
