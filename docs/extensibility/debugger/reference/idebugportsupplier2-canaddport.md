---
description: Verifica se um fornecedor de porta pode adicionar novas portas.
title: 'IDebugPortSupplier2:: CanAddPort | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2::CanAddPort
helpviewer_keywords:
- IDebugPortSupplier2::CanAddPort
ms.assetid: 41f69e0a-e82c-473d-8b7a-0c40fc5730fc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ad704eda53807d344b23736d2d9b55e172c36468
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072202"
---
# <a name="idebugportsupplier2canaddport"></a>IDebugPortSupplier2::CanAddPort
Verifica se um fornecedor de porta pode adicionar novas portas.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT CanAddPort( 
   void 
);
```

```csharp
int CanAddPort();
```

## <a name="return-value"></a>Valor retornado
 Se a porta puder ser adicionada, retornará `S_OK` ; caso contrário, retornará `S_FALSE` para indicar que nenhuma porta pode ser adicionada a esse fornecedor de porta.

## <a name="remarks"></a>Comentários
 Chame esse método antes de chamar o método [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md) , pois o último método cria a porta, além de adicioná-la, que pode ser uma operação demorada.

## <a name="see-also"></a>Confira também
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)
