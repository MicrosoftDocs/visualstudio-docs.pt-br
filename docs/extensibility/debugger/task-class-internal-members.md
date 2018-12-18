---
title: Classe Task - membros internos | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debug engines, Task class [.NET Framework]
- Task class [.NET Framework debug engines]
ms.assetid: 28e47c3b-9323-424a-80ac-6cc3bf19e09b
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: d9e9bbf6bbf42b8008850b540a59fa2b5d75b199
ms.sourcegitcommit: 8d38d5d2f2b75fc1563952c0d6de0fe43af12766
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/26/2018
ms.locfileid: "39276758"
---
# <a name="task-class---internal-members"></a>Classe Task - membros internos
Este artigo descreve os membros internos do <xref:System.Threading.Tasks.Task?displayProperty=fullName> classe que ajudam você a implementar um depurador personalizado. Para obter informações gerais sobre essa classe, consulte o <xref:System.Threading.Tasks.Task> artigo de referência.  
  
 **Namespace:** <xref:System.Threading.Tasks?displayProperty=fullName>  
  
 **Assembly:** mscorlib (em *mscorlib. dll*)  
  
 Porque você não pode acessar esses membros internos do .NET Framework, a sintaxe a seguir é fornecida em comum Intermediate Language (CIL).  
  
## <a name="syntax"></a>Sintaxe  
  
```csharp  
.class public auto ansi System.Threading.Tasks.Task  
       extends System.Object  
       implements System.Threading.IThreadPoolWorkItem,  
                  System.IAsyncResult,  
                  System.IDisposable,  
                  System.Threading.ICancelableOperation  
```  
  
## <a name="members"></a>Membros  
  
### <a name="methods"></a>Métodos  
  
|Nome|Descrição|  
|----------|-----------------|  
|[Método SetNotificationForWaitCompletion](../../extensibility/debugger/setnotificationforwaitcompletion-method.md)|Define ou limpa o bit de estado TASK_STATE_WAIT_COMPLETION_NOTIFICATION.|  
|[Método NotifyDebuggerOfWaitCompletion](../../extensibility/debugger/notifydebuggerofwaitcompletion-method.md)|Método de espaço reservado usado como um destino de ponto de interrupção pelo depurador.|  
  
### <a name="fields"></a>Campos  
  
|Nome|Descrição|  
|----------|-----------------|  
|[m_action](../../extensibility/debugger/m-action-field.md)|O delegado que representa o código seja executado no <xref:System.Threading.Tasks.Task> objeto.|  
|[m_contingentProperties](../../extensibility/debugger/m-contingentproperties-field.md)|Armazena propriedades adicionais do <xref:System.Threading.Tasks.Task> objeto.|  
|[m_Parent](../../extensibility/debugger/m-parent-field.md)|O campo de suporte para o <xref:System.Threading.Tasks.Task?displayProperty=fullName> propriedade pai.|  
|[m_stateFlags](../../extensibility/debugger/m-stateflags-field.md)|Armazena informações sobre o estado atual do <xref:System.Threading.Tasks.Task> objeto.|  
|[m_stateObject](../../extensibility/debugger/m-stateobject-field.md)|Um objeto que representa os dados que serão usados pela ação.|  
|[m_taskId](../../extensibility/debugger/m-taskid-field.md)|O campo de suporte para o <xref:System.Threading.Tasks.Task.Id%2A?displayProperty=fullName> propriedade.|  
|[s_taskIdCounter](../../extensibility/debugger/s-taskidcounter-field.md)|O próximo identificador disponível para um <xref:System.Threading.Tasks.Task> objeto.|  
|[TASK_STATE_CANCELED](../../extensibility/debugger/task-state-canceled-field.md)|Indica que a tarefa cancelada antes que este atingisse o estado de execução, ou que a tarefa confirmou o cancelamento e concluída sem exceção.|  
|[TASK_STATE_EXECUTED](../../extensibility/debugger/task-state-executed-field.md)|Indica que a tarefa está em execução.|  
|[TASK_STATE_FAULTED](../../extensibility/debugger/task-state-faulted-field.md)|Indica que a tarefa foi concluída devido a uma exceção sem tratamento.|  
|[TASK_STATE_RAN_TO_COMPLETION](../../extensibility/debugger/task-state-ran-to-completion-field.md)|Indica que a tarefa concluída com êxito a execução.|  
|[TASK_STATE_WAITING_ON_CHILDREN](../../extensibility/debugger/task-state-waiting-on-children-field.md)|Indica que a tarefa terminou a execução de seu delegado e está aguardando implicitamente a conclusão das tarefas filho anexadas.|  
  
## <a name="remarks"></a>Comentários  
 Os seguintes métodos internos são úteis para um mecanismo de depuração porque eles marcam da entrada <xref:System.Threading.Tasks.Task> a execução de código:  
  
-   `Execute`  
  
-   `ExecuteEntry`  
  
-   `ExecuteWithThreadLocal`  
  
-   `Finish`  
  
-   `InnerInvoke`  
  
-   `InternalWait`  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Threading.Tasks.Task?displayProperty=fullName>   
 [Elementos internos de extensões paralelas para o .NET Framework](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)