---
description: Obtém os bytes de memória que compõem o valor de uma propriedade.
title: 'IDebugProperty2:: GetMemoryBytes | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetMemoryBytes
helpviewer_keywords:
- IDebugProperty2::GetMemoryBytes
ms.assetid: b32042ed-7a06-4b4a-99ef-fe03b0aa61cc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 86a290ed3fc79c666099323516b8461d62f46b68
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064976"
---
# <a name="idebugproperty2getmemorybytes"></a>IDebugProperty2::GetMemoryBytes
Obtém os bytes de memória que compõem o valor de uma propriedade.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetMemoryBytes ( 
   IDebugMemoryBytes2** ppMemoryBytes
);
```

```csharp
int GetMemoryBytes ( 
   out IDebugMemoryBytes2 ppMemoryBytes
);
```

## <a name="parameters"></a>Parâmetros
`ppMemoryBytes`\
fora Retorna um objeto [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md) que pode ser usado para recuperar a memória que contém o valor da propriedade.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna o código de erro. Retorna `S_GETMEMORYBYTES_NO_MEMORY_BYTES` se não houver nenhum byte de memória para recuperar.

## <a name="see-also"></a>Confira também
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)
