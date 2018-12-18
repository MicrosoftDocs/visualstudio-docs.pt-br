---
title: Campo m_stateObject | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- m_stateObject field, Task class [.NET Framework debug engines]
ms.assetid: 68c54b22-3e1c-4031-b9c7-b972c519d8a0
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 4d33879ca8aaaba08288f9e16d54ab462d92f67b
ms.sourcegitcommit: 25a62c2db771f938e3baa658df8b1ae54a960e4f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2018
ms.locfileid: "39231311"
---
# <a name="mstateobject-field"></a>campo m_stateObject
Um objeto que representa os dados que usará a ação.  
  
 **Namespace:** <xref:System.Threading.Tasks?displayProperty=fullName>  
  
 **Assembly:** mscorlib (em *mscorlib. dll*)  
  
 Porque você não pode acessar esse membro interno do .NET Framework, a sintaxe a seguir é fornecida em comum Intermediate Language (CIL).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
.field assembly object m_stateObject  
```  
  
## <a name="remarks"></a>Comentários  
 Esse é o `state` parâmetro no <xref:System.Threading.Tasks.Task.%23ctor%2A> construtor. Também é o campo de suporte para o <xref:System.Threading.Tasks.Task.AsyncState%2A?displayProperty=fullName> propriedade.  
  
## <a name="see-also"></a>Consulte também  
 [Classe de tarefa](../../extensibility/debugger/task-class-internal-members.md)