---
description: Define o valor de uma referência de outra referência.
title: 'IDebugReference2:: SetValueAsReference | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::SetValueAsReference
helpviewer_keywords:
- IDebugReference2::SetValueAsReference
ms.assetid: 94a545d2-16b9-45e9-b2e7-4e49ff90aad0
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 84117f4a9eb925b442be86a73736479a05818ca1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102165937"
---
# <a name="idebugreference2setvalueasreference"></a>IDebugReference2::SetValueAsReference
Define o valor de uma referência de outra referência. Reservado para uso futuro.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT SetValueAsReference ( 
   IDebugReference2** rgpArgs,
   DWORD              dwArgCount,
   IDebugReference2*  pValue,
   DWORD              dwTimeout
);
```

```cpp
int SetValueAsReference ( 
   IDebugReference2[] rgpArgs,
   uint               dwArgCount,
   IDebugReference2   pValue,
   uint               dwTimeout
);
```

## <a name="parameters"></a>Parâmetros
`rgpArgs`\
no Uma matriz de objetos [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) usada para determinar como definir o valor de referência.

`dwArgCount`\
no O número de referências na matriz.

`pValue`\
no Um objeto [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) do qual definir o valor da propriedade.

`dwTimeout`\
no Tempo máximo, em milissegundos, a aguardar antes de retornar deste método. Use `INFINITE` para aguardar indefinidamente.

## <a name="return-value"></a>Valor Retornado
 Sempre retorna `E_NOTIMPL`.

## <a name="see-also"></a>Confira também
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
