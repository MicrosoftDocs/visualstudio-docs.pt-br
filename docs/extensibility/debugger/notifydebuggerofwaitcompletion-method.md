---
title: Método NotifyDebuggerOfWaitCompletion | Microsoft Docs
description: Saiba mais sobre o método NotifyDebuggerOfWaitCompletion, que é um espaço reservado usado como um destino de ponto de interrupção pelo depurador.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- NotifyDebuggerOfWaitCompletion method, Task class [.NET Framework debug engines]
ms.assetid: 841c5908-4f3f-400b-a7b0-96a95f362817
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d58bb7a5e3a3395b534e5679ec303e5d93d5dc85
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054732"
---
# <a name="notifydebuggerofwaitcompletion-method"></a>Método NotifyDebuggerOfWaitCompletion
Método de espaço reservado usado como um destino de ponto de interrupção pelo depurador. Este método não deve ser embutido nem ser otimizado.

 **Namespace:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **Assembly:** mscorlib (no *mscorlib.dll*)

## <a name="syntax"></a>Sintaxe

```vb
private void NotifyDebuggerOfWaitCompletion()
```

## <a name="remarks"></a>Comentários
 Todas as operações de junção com uma tarefa devem chamar esse método se o bit de notificação do depurador for definido.

## <a name="requirements"></a>Requisitos

## <a name="see-also"></a>Confira também
- [Classe de tarefa](../../extensibility/debugger/task-class-internal-members.md)
