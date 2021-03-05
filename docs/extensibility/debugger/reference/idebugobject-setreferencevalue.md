---
description: Define o valor de referência deste objeto.
title: 'IDebugObject:: setreferencevalue | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::SetReferenceValue
helpviewer_keywords:
- IDebugObject::SetReferenceValue method
ms.assetid: 08c78a4e-98eb-41cb-8b75-02a6a43d49f7
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bb376e4399157f9f9fe393086cca8fcf94c3b9de
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102161418"
---
# <a name="idebugobjectsetreferencevalue"></a>IDebugObject::SetReferenceValue
Define o valor de referência deste objeto.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT SetReferenceValue( 
   IDebugObject* pObject
);
```

```csharp
int SetReferenceValue(
   [In] IDebugObject pObject
);
```

## <a name="parameters"></a>Parâmetros
`pObject`\
no Um objeto [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) que representa o novo valor de referência.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Esse método torna esse objeto [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) uma referência ao valor do objeto fornecido no `pObject` parâmetro, descartando qualquer referência anterior. Observe que esse `IDebugObject` objeto já deve ser um tipo de referência.

## <a name="see-also"></a>Confira também
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)
