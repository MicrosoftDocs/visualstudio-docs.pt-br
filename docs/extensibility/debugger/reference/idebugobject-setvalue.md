---
description: Define o valor do objeto a partir de uma série de bytes consecutivos.
title: 'IDebugObject:: SetValue | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::SetValue
helpviewer_keywords:
- IDebugObject::SetValue method
ms.assetid: d652e09c-cdc1-4519-8116-d7c743f5679b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 972281335b964679f38693182e42c4e64074dffa
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102167146"
---
# <a name="idebugobjectsetvalue"></a>IDebugObject::SetValue
Define o valor do objeto a partir de uma série de bytes consecutivos.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT SetValue( 
   BYTE* pValue,
   UINT  nSize
);
```

```csharp
int SetValue(
   byte[] pValue,
   uint   nSize
);
```

## <a name="parameters"></a>Parâmetros
`pValue`\
no Uma matriz de bytes que representa o novo valor.

`nSize`\
no O tamanho do valor em bytes.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Os valores na matriz são copiados para esse objeto [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) , substituindo qualquer valor existente. O tamanho do novo valor pode ser maior ou menor do que o valor existente. Essa `IDebugObject` não pode ser uma referência nula.

## <a name="see-also"></a>Confira também
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)
