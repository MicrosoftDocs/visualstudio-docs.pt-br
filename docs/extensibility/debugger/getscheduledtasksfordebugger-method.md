---
description: Recupera uma matriz de todas as tarefas agendadas.
title: Método GetScheduledTasksForDebugger | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetScheduledTasksForDebugger method, TaskScheduler class [.NET Framework debug engines]
ms.assetid: 7c9b4cde-6e4a-4cef-929f-7d02b1da5762
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 51da481edb636450770d0cff569b9ef411e17cf6
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900948"
---
# <a name="getscheduledtasksfordebugger-method"></a>Método GetScheduledTasksForDebugger
Recupera uma matriz de todas as tarefas agendadas.

 **Namespace:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **Assembly:** mscorlib *(emmscorlib.dll*)

 Como você não pode acessar esse membro interno do .NET Framework, a sintaxe a seguir é fornecida Common Intermediate Language (CIL).

## <a name="syntax"></a>Sintaxe

```csharp
.method assembly hidebysig instance class System.Threading.Tasks.Task[] GetScheduledTasksForDebugger() cil managed
```

## <a name="return-value"></a>Valor retornado
 Uma matriz de todas as tarefas agendadas. Cada tarefa está em execução ou concluiu a execução.

## <a name="remarks"></a>Comentários
 Esse método não é thread-safe e você não deve usá-lo simultaneamente com outras instâncias do <xref:System.Threading.Tasks.TaskScheduler> . Chame esse método de um depurador somente quando o depurador tiver suspenso todos os outros threads.

## <a name="see-also"></a>Confira também
- [Classe TaskScheduler](../../extensibility/debugger/taskscheduler-class-internal-members.md)
