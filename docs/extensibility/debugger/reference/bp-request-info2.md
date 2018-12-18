---
title: BP_REQUEST_INFO2 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- BP_REQUEST_INFO2
helpviewer_keywords:
- BP_REQUEST_INFO2 structure
ms.assetid: 008c87f7-a76e-43d3-8904-11b225d6a9a5
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 68bdf873cdd108428ec05bda6429de70a80e71a8
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49888782"
---
# <a name="bprequestinfo2"></a>BP_REQUEST_INFO2
Contém as informações necessárias para implementar um ponto de interrupção, incluindo o GUID do fornecedor, restrição e tracepoint.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef struct _BP_REQUEST_INFO2 {  
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
} BP_REQUEST_INFO2;  
```  
  
```csharp  
public struct BP_REQUEST_INFO2 {  
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
 `dwFields`  
 Uma combinação de sinalizadores do [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md) enumeração que especifica quais campos são preenchidos.  
  
 `guidLanguage`  
 O GUID do idioma.  
  
 `bpLocation`  
 O [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) estrutura que especifica o tipo do local de ponto de interrupção.  
  
 `pProgram`  
 O [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) objeto que representa o aplicativo no qual o ponto de interrupção ocorre.  
  
 `bstrProgramName`  
 O nome do aplicativo no qual o ponto de interrupção ocorre.  
  
 `pThread`  
 O [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) objeto que representa o thread no qual o ponto de interrupção ocorre.  
  
 `bstrThreadName`  
 O nome do thread no qual o ponto de interrupção ocorre.  
  
 `bpCondition`  
 O [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md) estrutura que descreve as condições sob as quais o ponto de interrupção será acionado.  
  
 `bpPassCount`  
 O [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md) estrutura que contém as informações de contagem de passagem do ponto de interrupção.  
  
 `dwFlags`  
 Uma combinação de sinalizadores do [BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md) enumeração que especifica os sinalizadores para o ponto de interrupção solicitado.  
  
 `guidVendor`  
 GUID do fornecedor. Pode ser um valor nulo.  
  
 `bstrConstraint`  
 Nome da restrição de ponto de interrupção. Pode ser um valor nulo.  
  
 `bstrTracepoint`  
 Nome do ponto de rastreamento. Pode ser um valor nulo.  
  
## <a name="remarks"></a>Comentários  
 Essa estrutura é retornada pelo [GetRequestInfo2](../../../extensibility/debugger/reference/idebugbreakpointrequest3-getrequestinfo2.md) método.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [GetRequestInfo2](../../../extensibility/debugger/reference/idebugbreakpointrequest3-getrequestinfo2.md)   
 [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)   
 [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)   
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)   
 [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)   
 [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)   
 [BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md)