---
description: Recupera uma matriz de todos os objetos System. Threading. Tasks. TaskScheduler que estão ativos no momento.
title: Método GetTaskSchedulersForDebugger | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- GetTaskSchedulersForDebugger method, TaskScheduler class [.NET Framework debug engines]
ms.assetid: 58aa236a-5ab8-4695-b303-89dffdbcd946
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7d024e44dee8e7513d862e3d299c2ed2b9e53cd5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054849"
---
# <a name="gettaskschedulersfordebugger-method"></a>Método GetTaskSchedulersForDebugger
Recupera uma matriz de todos os <xref:System.Threading.Tasks.TaskScheduler> objetos que estão ativos no momento.

 **Namespace:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **Assembly:** mscorlib (no *mscorlib.dll*)

 Como você não pode acessar esse membro interno do .NET Framework, a sintaxe a seguir é fornecida em Common Intermediate Language (CIL).

## <a name="syntax"></a>Sintaxe

```csharp
.method assembly hidebysig static class System.Threading.Tasks.TaskScheduler[] GetTaskSchedulersForDebugger() cil managed
```

## <a name="return-value"></a>Retornar valor
 Uma matriz de todos os <xref:System.Threading.Tasks.TaskScheduler> objetos que estão atualmente ativos neste <xref:System.AppDomain> .

## <a name="remarks"></a>Comentários
 Esse método não é thread-safe e você não deve usá-lo simultaneamente com outras instâncias do <xref:System.Threading.Tasks.TaskScheduler> . Chame esse método de um depurador somente quando o depurador tiver suspenso todos os outros threads.

## <a name="see-also"></a>Confira também
- [Classe TaskScheduler](../../extensibility/debugger/taskscheduler-class-internal-members.md)
