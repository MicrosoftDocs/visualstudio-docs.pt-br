---
title: IDebugCodeContext2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugCodeContext2
helpviewer_keywords:
- IDebugCodeContext2 interface
ms.assetid: 3670439e-2171-405d-9d77-dedb0f1cba93
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2e06fd709b2d076b6fa8de7f104e907eb1b35a42
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68190949"
---
# <a name="idebugcodecontext2"></a>IDebugCodeContext2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Essa interface representa a posição inicial de uma instrução de código. Para a maioria das arquiteturas de tempo de execução atualmente, um contexto de código pode ser pensado como um endereço no fluxo de execução de um programa.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugCodeContext2 : IDebugMemoryContext2  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 O mecanismo de depuração implementa essa interface para relacionar a posição de uma instrução de código para uma posição do documento.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Métodos em várias interfaces retornam essa interface, em geral, [GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md). Ele também é usado extensivamente com o [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md) interface, bem como informações de resolução de ponto de interrupção.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem de Vtable  
 Além dos métodos na [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) interface, essa interface implementa os seguintes métodos:  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md)|Obtém o contexto do documento que corresponde ao contexto de código ativo.|  
|[GetLanguageInfo](../../../extensibility/debugger/reference/idebugcodecontext2-getlanguageinfo.md)|Obtém as informações de idioma para este contexto de código.|  
  
## <a name="remarks"></a>Comentários  
 A principal diferença entre um `IDebugCodeContext2` interface e uma [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) interface é que um `IDebugCodeContext2` sempre é alinhado à instrução. Isso significa que um `IDebugCodeContext2` sempre está apontando para o início de uma instrução, enquanto um `IDebugMemoryContext2` podem apontar para qualquer byte de memória na arquitetura de tempo de execução. `IDebugCodeContext2` é incrementado por instruções em vez do tamanho de armazenamento básico (normalmente bytes).  
  
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
