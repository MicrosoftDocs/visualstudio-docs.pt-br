---
title: BP_REQUEST_INFO2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_REQUEST_INFO2
helpviewer_keywords:
- BP_REQUEST_INFO2 structure
ms.assetid: 008c87f7-a76e-43d3-8904-11b225d6a9a5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 04d1db2ca8176678d8a72a84ede2bddcbfa2f152
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737884"
---
# <a name="bp_request_info2"></a>BP_REQUEST_INFO2
Contém as informações necessárias para implementar um ponto de ruptura, incluindo GUID, restrição e tracepoint do fornecedor.

## <a name="syntax"></a>Sintaxe

```cpp
typedef struct _BP_REQUEST_INFO2 {
    BPREQI_FIELDS   dwFields;
    GUID            guidLanguage;
    BP_LOCATION     bpLocation;
    IDebugProgram2* pProgram;
    BSTR            bstrProgramName;
    IDebugThread2*  pThread;
    BSTR            bstrThreadName;
    BP_CONDITION    bpCondition;
    BP_PASSCOUNT    bpPassCount;
    BP_FLAGS        dwFlags;
    GUID            guidVendor;
    BSTR            bstrConstraint;
    BSTR            bstrTracepoint;
} BP_REQUEST_INFO2;
```

```csharp
public struct BP_REQUEST_INFO2 {
    public uint           dwFields;
    public Guid           guidLanguage;
    public BP_LOCATION    bpLocation;
    public IDebugProgram2 pProgram;
    public string         bstrProgramName;
    public IDebugThread2  pThread;
    public string         bstrThreadName;
    public BP_CONDITION   bpCondition;
    public BP_PASSCOUNT   bpPassCount;
    public uint           dwFlags;
    public Guid           guidVendor;
    public string         bstrConstraint;
    public string         bstrTracepoint;
};
```

## <a name="members"></a>Membros
`dwFields`\
Uma combinação de bandeiras da enumeração [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md) que especifica quais campos são preenchidos.

`guidLanguage`\
O GUID do idioma.

`bpLocation`\
A estrutura [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) que especifica o tipo de local do ponto de ruptura.

`pProgram`\
O objeto [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) que representa o aplicativo no qual ocorre o ponto de ruptura.

`bstrProgramName`\
O nome do aplicativo no qual ocorre o ponto de ruptura.

`pThread`\
O objeto [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) que representa o segmento no qual ocorre o ponto de ruptura.

`bstrThreadName`\
O nome do segmento no qual ocorre o ponto de ruptura.

`bpCondition`\
A [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md) estrutura que descreve as condições sob as quais o ponto de ruptura será acionado.

`bpPassCount`\
A [estrutura BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md) que contém as informações de contagem de passes do ponto de ruptura.

`dwFlags`\
Uma combinação de bandeiras da enumeração [BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md) que especifica as bandeiras para o ponto de ruptura solicitado.

`guidVendor`\
GUID de fornecedor. Pode ser um valor nulo.

`bstrConstraint`\
Nome da restrição de ponto de ruptura. Pode ser um valor nulo.

`bstrTracepoint`\
Nome do ponto de rastreamento. Pode ser um valor nulo.

## <a name="remarks"></a>Comentários
Essa estrutura é devolvida pelo método [GetRequestInfo2.](../../../extensibility/debugger/reference/idebugbreakpointrequest3-getrequestinfo2.md)

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg.h

Namespace: Microsoft.VisualStudio.Debugger.Interop

Montagem: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetRequestInfo2](../../../extensibility/debugger/reference/idebugbreakpointrequest3-getrequestinfo2.md)
- [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)
- [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)
- [BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md)
