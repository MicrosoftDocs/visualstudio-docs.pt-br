---
description: Obtém a propriedade Parent de uma propriedade.
title: 'IDebugProperty2:: GetParent | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetParent
helpviewer_keywords:
- IDebugProperty2::GetParent
ms.assetid: 58780469-fe25-4d84-9187-67940ca0767f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ef12171d338802b585818954858f5af4d723a34c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064833"
---
# <a name="idebugproperty2getparent"></a>IDebugProperty2::GetParent
Obtém a propriedade Parent de uma propriedade.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetParent ( 
   IDebugProperty2** ppParent
);
```

```csharp
int GetParent ( 
   out IDebugProperty2 ppParent
);
```

## <a name="parameters"></a>Parâmetros
`ppParent`\
fora Retorna um objeto [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) que representa o pai da propriedade.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna o código de erro. Retornará `S_GETPARENT_NO_PARENT` se não houver nenhum pai.

## <a name="see-also"></a>Confira também
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
