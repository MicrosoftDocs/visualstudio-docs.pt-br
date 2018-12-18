---
title: IDebugCodeContext2 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugCodeContext2
helpviewer_keywords:
- IDebugCodeContext2 interface
ms.assetid: 3670439e-2171-405d-9d77-dedb0f1cba93
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 5b46ec36a93ac91647a3f17aac28187519ca2447
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31103871"
---
# <a name="idebugcodecontext2"></a>IDebugCodeContext2
Essa interface representa a posição inicial de uma instrução de código. Para a maioria das arquiteturas de tempo de execução atualmente, um contexto de código pode ser pensado como um endereço no fluxo de execução do programa.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugCodeContext2 : IDebugMemoryContext2  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 O mecanismo de depuração implementa essa interface para relacionar a posição de uma instrução de código para uma posição de documento.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Métodos em interfaces muitos retornam esta interface, geralmente, [GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md). Ele também é usado extensivamente com o [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md) interface, bem como informações de resolução do ponto de interrupção.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
 Além dos métodos de [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) interface, essa interface implementa os métodos a seguir:  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md)|Obtém o contexto de documento que corresponde ao contexto de código ativo.|  
|[GetLanguageInfo](../../../extensibility/debugger/reference/idebugcodecontext2-getlanguageinfo.md)|Obtém as informações de idioma para este contexto de código.|  
  
## <a name="remarks"></a>Comentários  
 A principal diferença entre um `IDebugCodeContext2` interface e um [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) interface é que um `IDebugCodeContext2` sempre é alinhado à instrução. Isso significa que um `IDebugCodeContext2` sempre está apontando para o início de uma instrução, enquanto um `IDebugMemoryContext2` pode apontar para qualquer bytes de memória na arquitetura de tempo de execução. `IDebugCodeContext2` é incrementado por instruções em vez do tamanho de armazenamento básico (normalmente bytes).  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)   
 [CanSetNextStatement](../../../extensibility/debugger/reference/idebugthread2-cansetnextstatement.md)   
 [SetNextStatement](../../../extensibility/debugger/reference/idebugthread2-setnextstatement.md)   
 [GetCodeContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getcodecontext.md)   
 [GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)   
 [Avançar](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-next.md)   
 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)