---
description: Cria um enumerador para as interfaces implementadas por essa classe.
title: 'IDebugClassField:: EnumInterfacesImplemented | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::EnumInterfacesImplemented
helpviewer_keywords:
- IDebugClassField::EnumInterfacesImplemented method
ms.assetid: e5523e45-d350-491e-a92c-fe0ca97d2052
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1763cbcd0a1c61150a054752c94a42f10127251a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088608"
---
# <a name="idebugclassfieldenuminterfacesimplemented"></a>IDebugClassField::EnumInterfacesImplemented
Cria um enumerador para as interfaces implementadas por essa classe.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT EnumInterfacesImplemented( 
   IEnumDebugFields** ppEnum
);
```

```csharp
int EnumInterfacesImplemented(
   out IEnumDebugFields ppEnum
);
```

## <a name="parameters"></a>Parâmetros
`ppEnum`\
fora Retorna um objeto [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) que representa a lista de interfaces implementadas. Retorna um valor nulo se não houver nenhuma interface.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK ou retornará S_FALSE se não houver interfaces implementadas nessa classe. Caso contrário, retornará um código de erro.

## <a name="remarks"></a>Comentários
 Cada elemento da enumeração é um objeto [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) que descreve uma interface. Observe que [!INCLUDE[vcprvc](../../../code-quality/includes/vcprvc_md.md)] o código não gerenciado não usa interfaces como uma entidade discreta, portanto, esse método sempre retorna um valor nulo para código não gerenciado [!INCLUDE[vcprvc](../../../code-quality/includes/vcprvc_md.md)] .

## <a name="see-also"></a>Confira também
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
