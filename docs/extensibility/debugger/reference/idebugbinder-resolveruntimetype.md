---
description: Esse método determina o tipo de tempo de execução de um objeto.
title: 'IDebugBinder:: ResolveRuntimeType | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder::ResolveRuntimeType
helpviewer_keywords:
- IDebugBinder::ResolveRuntimeType method
ms.assetid: 6456ab3e-1c03-4f3c-91f9-16797ab7f5e7
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 19e7285dd25009e7fe4aeb92974c70ce4109502c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102143630"
---
# <a name="idebugbinderresolveruntimetype"></a>IDebugBinder::ResolveRuntimeType
Esse método determina o tipo de tempo de execução de um objeto.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT ResolveRuntimeType( 
   IDebugObject* pObject,
   IDebugField** ppResolved
);
```

```csharp
int ResolveRuntimeType(
   IDebugObject     pObject,
   out IDebugField  ppResolved
);
```

## <a name="parameters"></a>Parâmetros
`pObject`\
no O [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) a ser resolvido.

`ppResolved`\
fora Retorna o tipo do objeto como um [IDebugField](../../../extensibility/debugger/reference/idebugfield.md).

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 O tipo de tempo de execução de um objeto nem sempre é conhecido no momento da compilação. Por exemplo, usando polimorfismo, um argumento pode ser passado para uma função como sua classe base, como uma classe de botão. O argumento real pode ser uma classe derivada, como uma classe de botão de opção.

## <a name="see-also"></a>Confira também
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
