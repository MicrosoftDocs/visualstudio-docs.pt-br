---
title: BP_LOCATION_CODE_FILE_LINE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION_CODE_FILE_LINE
helpviewer_keywords:
- BP_LOCATION_CODE_FILE_LINE structure
ms.assetid: 3ff32032-d412-44d3-91bf-870cc354a09e
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 611a3103c2747040ae9d72c53a905ee3f23c180a
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/22/2019
ms.locfileid: "56688284"
---
# <a name="bplocationcodefileline"></a>BP_LOCATION_CODE_FILE_LINE
Contém os dados para o local de um ponto de interrupção em uma linha específica em um arquivo de origem do código.

## <a name="syntax"></a>Sintaxe

```cpp
typedef struct _BP_LOCATION_CODE_FILE_LINE {
    BSTR                     bstrContext;
    IDebugDocumentPosition2* pDocPos;
} BP_LOCATION_CODE_FILE_LINE;
```

## <a name="members"></a>Membros
`bstrContext` O contexto do ponto de interrupção, normalmente um nome de método ou função, como visto em uma pilha de chamadas.

`pDocPos` O [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md) objeto que representa a posição do documento do ponto de interrupção.

## <a name="remarks"></a>Comentários
Essa estrutura é um membro do [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) estrutura como parte de uma união.

## <a name="requirements"></a>Requisitos
Header: msdbg.h

Namespace: Microsoft.VisualStudio.Debugger.Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Consulte também
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)
