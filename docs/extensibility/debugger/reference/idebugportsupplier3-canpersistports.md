---
description: Esse método determina se o fornecedor da porta pode persistir portas (gravando-as no disco) entre invocações do depurador.
title: 'IDebugPortSupplier3:: CanPersistPorts | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier3::CanPersistPorts
helpviewer_keywords:
- IDebugPortSupplier3::CanPersistPorts
ms.assetid: 4127760c-e602-4e86-9232-457e382a52c7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 570409a114acbf19697b0eb3ef3e5496fdfde93a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071968"
---
# <a name="idebugportsupplier3canpersistports"></a>IDebugPortSupplier3::CanPersistPorts
Esse método determina se o fornecedor da porta pode persistir portas (gravando-as no disco) entre invocações do depurador.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT CanPersistPorts();
```

```csharp
int CanPersistPorts();
```

## <a name="parameters"></a>Parâmetros
 Nenhum.

## <a name="return-value"></a>Valor Retornado
 `S_OK` Se as portas puderem ser persistidas ou `S_FALSE` para indicar que as portas não podem ser persistentes.

## <a name="remarks"></a>Comentários
 Se o fornecedor da porta persistir portas, ele deverá fazer isso quando for destruído e, em seguida, recarregá-las quando ela for instanciada novamente.

## <a name="see-also"></a>Confira também
- [IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md)
