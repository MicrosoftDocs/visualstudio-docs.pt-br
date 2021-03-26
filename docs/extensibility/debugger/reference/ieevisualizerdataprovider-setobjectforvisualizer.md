---
description: Esse método altera o objeto que o visualizador representa.
title: 'IEEVisualizerDataProvider:: SetObjectForVisualizer | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerDataProvider::SetObjectForVisualizer
helpviewer_keywords:
- IEEVisualizerDataProvider::SetObjectForVisualizer method
ms.assetid: 40dad2be-57ff-4f74-9d82-c48039c125c4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2e0a59c10293d5d8cc13d46b625a7b43136cb71b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091793"
---
# <a name="ieevisualizerdataprovidersetobjectforvisualizer"></a>IEEVisualizerDataProvider::SetObjectForVisualizer
Esse método altera o objeto que o visualizador representa.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT SetObjectForVisualizer(
   IDebugObject*  pNewObject,
   BSTR*          error,
   IDebugObject** pException
);
```

```csharp
int SetObjectForVisualizer(
   IDebugObject     pNewObject,
   out string       error,
   out IDebugObject pException
);
```

## <a name="parameters"></a>Parâmetros
`pNewObject`\
no O objeto a ser definido.

`error`\
fora Se houvesse um erro ao definir o objeto, essa cadeia de caracteres conterá a mensagem de erro.

`pException`\
fora Se houver um erro, esse objeto conterá as informações de exceção.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Cabe ao implementador determinar como as informações de erro são retornadas. No entanto, é possível que alguns chamadores só procurem ver se um objeto de exceção foi retornado para saber que houve um erro, portanto, esse método sempre deve retornar um objeto de exceção se houvesse um erro. A cadeia de caracteres de erro também deve ser fornecida caso o chamador queira usá-la.

## <a name="see-also"></a>Confira também
- [IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
