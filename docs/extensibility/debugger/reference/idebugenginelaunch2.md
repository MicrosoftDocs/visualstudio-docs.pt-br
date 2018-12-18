---
title: IDebugEngineLaunch2 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugEngineLaunch2
helpviewer_keywords:
- IDebugEngineLaunch2 interface
ms.assetid: 5eaf2ad8-3fbf-446e-b48b-5327ad3f5255
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 1abff9f393b34bbf5950c9e56b6f489f332840db
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31113241"
---
# <a name="idebugenginelaunch2"></a>IDebugEngineLaunch2
Usado por um mecanismo de depuração (DE) para iniciar e encerrar programas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugEngineLaunch2 : IDebugEngine2  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 Essa interface é implementada por um DE personalizada se ele tem requisitos especiais para iniciar um processo que não pode ser manipulado inteiramente por uma porta personalizada. Isso normalmente é o caso quando o DE faz parte de um intérprete e o processo que está sendo depurado é um script: o interpretador deve ser iniciado pela primeira vez e, em seguida, o script é carregado e iniciado. Uma porta pode iniciar o interpretador, mas o script pode exigir tratamento especial (que é onde o DE tem uma função). Essa interface é implementada somente se houver requisitos específicos para iniciar um programa que não é possível manipular uma porta personalizada.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Essa interface é chamada, o Gerenciador de sessão de depuração (SDM) se o SDM pode obter essa interface do [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) interface (usando QueryInterface). Se essa interface pode ser obtida, o SDM sabe que o DE tem requisitos especiais e chama essa interface para iniciar o programa em vez de ter a porta iniciá-lo.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
 A tabela a seguir mostra os métodos de `IDebugEngineLaunch2`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)|Inicia um processo por meio DE.|  
|[ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)|Reinicia a processo de execução.|  
|[CanTerminateProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-canterminateprocess.md)|Determina se um processo pode ser encerrado.|  
|[TerminateProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-terminateprocess.md)|Finaliza um processo.|  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: Msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)