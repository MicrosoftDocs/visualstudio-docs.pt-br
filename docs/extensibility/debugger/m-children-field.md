---
description: A lista de tarefas filho que são registradas com esta tarefa.
title: Campo de m_children | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- m_children field, ContingentProperties class [.NET Framework debug engines]
ms.assetid: 0a3b5653-7bc0-4a7a-8963-9020bc52b9cb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 311ab164551e46fbe1c30b5a6045a7993a900a67
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901364"
---
# <a name="m_children-field"></a>campo de m_children
A lista de tarefas filho que são registradas com esta tarefa.

 **Namespace:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **Assembly:** mscorlib (no *mscorlib.dll*)

 Como você não pode acessar esse membro interno do .NET Framework, a sintaxe a seguir é fornecida em Common Intermediate Language (CIL).

## <a name="syntax"></a>Sintaxe

```csharp
.field public class System.Collections.Generic.List`1<class System.Threading.Tasks.Task> m_children
```

## <a name="remarks"></a>Comentários
 Enquanto a tarefa está em execução, somente o thread que executa a tarefa deve acessar essa matriz.

 Se a tarefa for concluída, outros threads poderão acessar esse campo contanto que eles não adicionem nada a ele nem removam nada dele.

## <a name="see-also"></a>Confira também
- [Classe contingentproperties](../../extensibility/debugger/contingentproperties-class-internal-members.md)
