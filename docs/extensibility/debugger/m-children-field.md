---
description: A lista de tarefas filho que são registradas com esta tarefa.
title: Campo de m_children | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- m_children field, ContingentProperties class [.NET Framework debug engines]
ms.assetid: 0a3b5653-7bc0-4a7a-8963-9020bc52b9cb
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5aaf29d76a7bbd81a416c86360f315bc5c09b76c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102158863"
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
