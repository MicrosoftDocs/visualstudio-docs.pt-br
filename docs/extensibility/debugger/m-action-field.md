---
description: O delegado que representa o código a ser executado no objeto System. Threading. Tasks. Task.
title: Campo de m_action | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- m_action field, Task class [.NET Framework debug engines]
ms.assetid: 201838c2-260d-4071-b6c3-f526874e19c9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: be180bf50c61869aab889c731e40d8d43ffb7300
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094647"
---
# <a name="m_action-field"></a>campo de m_action
O delegado que representa o código a ser executado no <xref:System.Threading.Tasks.Task> objeto.

 **Namespace:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **Assembly:** mscorlib (no *mscorlib.dll*)

 Como você não pode acessar esse membro interno do .NET Framework, a sintaxe a seguir é fornecida em Common Intermediate Language (CIL).

## <a name="syntax"></a>Sintaxe

```csharp
.field assembly object m_action
```

## <a name="remarks"></a>Comentários
 Esse é o `action` parâmetro no <xref:System.Threading.Tasks.Task.%23ctor%2A> Construtor.

## <a name="see-also"></a>Confira também
- [Classe de tarefa](../../extensibility/debugger/task-class-internal-members.md)
