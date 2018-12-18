---
title: IDebugProcessEx2 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugProcessEx2
helpviewer_keywords:
- IDebugProcessEx2 interface
ms.assetid: 44e309ba-1d6f-499b-aa7e-9b34858a6d57
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 7fa10fb5ebe2f9a78d44997c29ae51bc02e2c842
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49934932"
---
# <a name="idebugprocessex2"></a>IDebugProcessEx2
Essa interface permite que a sessão de Gerenciador de depuração (SDM) notificar um processo que está anexando a ou desanexar do processo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugProcessEx2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 Um fornecedor de porta personalizada implementa essa interface no mesmo objeto como o [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) de interface para:  
  
- Suporte ao acompanhamento de sessões conectadas a um processo  
  
- Suporte a anexação automática entre vários mecanismos de depuração  
  
  O fornecedor de porta personalizada pode implementar essa interface se optar por.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
  
-   As chamadas SDM [QueryInterface](/cpp/atl/queryinterface) em um `IDebugProcess2` interface para obter essa interface.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem de Vtable  
 A tabela a seguir mostra os métodos de `IDebugProcessEx2`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[Anexar](../../../extensibility/debugger/reference/idebugprocessex2-attach.md)|Informa o processo que uma sessão agora está depurando o processo.|  
|[Desanexar](../../../extensibility/debugger/reference/idebugprocessex2-detach.md)|Informa o processo que uma sessão não está depurando o processo.|  
|[AddImplicitProgramNodes](../../../extensibility/debugger/reference/idebugprocessex2-addimplicitprogramnodes.md)|Adiciona nós de programa para obter uma lista de mecanismos de depuração.|  
  
## <a name="remarks"></a>Comentários  
 Essa interface é privada entre o SDM e o processo.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: Portpriv.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Principais Interfaces](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)