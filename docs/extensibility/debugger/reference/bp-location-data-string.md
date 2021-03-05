---
description: Usado para definir pontos de interrupção de dados baseados em uma cadeia de caracteres que o usuário pode inserir do ambiente de desenvolvimento integrado (IDE).
title: BP_LOCATION_DATA_STRING | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION_DATA_STRING
helpviewer_keywords:
- BP_LOCATION_DATA_STRING structure
ms.assetid: 445d6f3f-95b0-47ac-85e2-51b778240687
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
ms.openlocfilehash: 1e4a250843ebbb6ab7680040e3aa296699e184ee
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102144345"
---
# <a name="bp_location_data_string"></a>BP_LOCATION_DATA_STRING
Usado para definir pontos de interrupção de dados baseados em uma cadeia de caracteres que o usuário pode inserir do ambiente de desenvolvimento integrado (IDE).

## <a name="syntax"></a>Sintaxe

```cpp
typedef struct _BP_LOCATION_DATA_STRING {
    IDebugThread2* pThread;
    BSTR           bstrContext;
    BSTR           bstrDataExpr;
    DWORD          dwNumElements;
} BP_LOCATION_DATA_STRING;
```

## <a name="members"></a>Membros
`pThread`\
O objeto [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) que representa o thread no qual o ponto de interrupção ocorre.

`bstrContext`\
O contexto do ponto de interrupção dentro do código, normalmente um nome de método ou função como visto em uma pilha de chamadas.

`bstrDataExpr`\
A cadeia de dados que o usuário insere para definir o ponto de interrupção.

`dwNumElements`\
O número de elementos na cadeia de caracteres de dados em que ocorre o ponto de interrupção.

## <a name="remarks"></a>Comentários
Essa estrutura é um membro da estrutura de [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) como parte de uma União.

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
