---
title: IDebugProcessQueryProperties | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- IDebugProcessQueryProperties
ms.assetid: ce29a248-81a0-42c0-99a7-1606e8c548ec
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: ac071afd9f9ce7d45a05408aeec32117776832f2
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31116185"
---
# <a name="idebugprocessqueryproperties"></a>IDebugProcessQueryProperties
Esta interface é uma interface de extensão implementada por [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) implementadores. Ele permite que o implementador obter informações sobre o ambiente do processo de depuração.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugProcessQueryProperties: IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 Implemente essa interface para obter informações sobre o ambiente de execução de um processo de depuração.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
 A tabela a seguir mostra os métodos de `IDebugProcessQueryProperties`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[QueryProperty](../../../extensibility/debugger/reference/idebugprocessqueryproperties-queryproperty.md)|Consultas para um valor de propriedade.|  
|[QueryProperties](../../../extensibility/debugger/reference/idebugprocessqueryproperties-queryproperties.md)|Consultas de valores de propriedade.|  
  
## <a name="remarks"></a>Comentários  
 Essa interface é implementada raramente.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: Portpriv.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de núcleo](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)