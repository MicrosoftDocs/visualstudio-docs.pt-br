---
description: Um objeto que representa os dados que a ação usará.
title: m_stateObject campo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- m_stateObject field, Task class [.NET Framework debug engines]
ms.assetid: 68c54b22-3e1c-4031-b9c7-b972c519d8a0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: df510fafbfe3ed6e71e9b5290fb1df0b02ae1d39
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903951"
---
# <a name="m_stateobject-field"></a>m_stateObject campo
Um objeto que representa os dados que a ação usará.

 **Namespace:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **Assembly:** mscorlib *(emmscorlib.dll*)

 Como você não pode acessar esse membro interno do .NET Framework, a sintaxe a seguir é fornecida Common Intermediate Language (CIL).

## <a name="syntax"></a>Sintaxe

```
.field assembly object m_stateObject
```

## <a name="remarks"></a>Comentários
 Esse é `state` o parâmetro no <xref:System.Threading.Tasks.Task.%23ctor%2A> construtor. Também é o campo de backing para a <xref:System.Threading.Tasks.Task.AsyncState%2A?displayProperty=fullName> propriedade .

## <a name="see-also"></a>Confira também
- [Classe de tarefa](../../extensibility/debugger/task-class-internal-members.md)
