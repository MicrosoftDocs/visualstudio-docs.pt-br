---
title: 'IDebugClassField:: EnumNestedEnums | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::EnumNestedEnums
helpviewer_keywords:
- IDebugClassField::EnumNestedEnums method
ms.assetid: 90fd0cef-9145-4de6-91d4-6c881df39d6e
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b9c283d4b07458368a4ea5f143dc83bf13453302
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99912005"
---
# <a name="idebugclassfieldenumnestedenums"></a>IDebugClassField::EnumNestedEnums
Cria um enumerador para os enumeradores aninhados dessa classe.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT EnumNestedEnums(
    IEnumDebugFields** ppEnum
);
```

```csharp
int EnumNestedEnums(
    out IEnumDebugFields ppEnum
);
```

## <a name="parameters"></a>Parâmetros
`ppEnum`\
fora Retorna um objeto [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) que representa a lista de enumerações aninhadas. Retorna um valor nulo se não houver nenhuma Enumeração aninhada.

## <a name="return-value"></a>Valor retornado
Se for bem-sucedido, retornará S_OK ou retornará S_FALSE se não houver enumeradores aninhados. Caso contrário, retornará um código de erro.

## <a name="remarks"></a>Comentários
Cada elemento da enumeração é um objeto [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md) que descreve uma enumeração aninhada.

Uma enumeração declarada dentro de uma classe é considerada uma enumeração aninhada. Por exemplo, considerando que:

```
class RootClass {
    enum NestedEnum { EnumValue = 0 }
};
```

O `EnumNestedEnums` método retornaria um objeto [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) que contém um objeto [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md) que representa a `NestedEnum` enumeração.

## <a name="see-also"></a>Consulte também
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)
