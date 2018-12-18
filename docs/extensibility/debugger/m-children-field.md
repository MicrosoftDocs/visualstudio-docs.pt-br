---
title: Campo m_children | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- m_children field, ContingentProperties class [.NET Framework debug engines]
ms.assetid: 0a3b5653-7bc0-4a7a-8963-9020bc52b9cb
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: e27704484e5cfb320c8b65432fb3efb283054019
ms.sourcegitcommit: 25a62c2db771f938e3baa658df8b1ae54a960e4f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2018
ms.locfileid: "39231142"
---
# <a name="mchildren-field"></a>campo m_children
A lista de tarefas filho que estão registrados com essa tarefa.  
  
 **Namespace:** <xref:System.Threading.Tasks?displayProperty=fullName>  
  
 **Assembly:** mscorlib (em *mscorlib. dll*)  
  
 Porque você não pode acessar esse membro interno do .NET Framework, a sintaxe a seguir é fornecida em comum Intermediate Language (CIL).  
  
## <a name="syntax"></a>Sintaxe  
  
```csharp 
.field public class System.Collections.Generic.List`1<class System.Threading.Tasks.Task> m_children  
```  
  
## <a name="remarks"></a>Comentários  
 Enquanto a tarefa está em execução, somente o thread que executa a tarefa deve acessar essa matriz.  
  
 Se a tarefa for concluída, outros threads podem acessar este campo desde que eles não adiciona nada a ele ou remover nada dela.  
  
## <a name="see-also"></a>Consulte também  
 [Classe ContingentProperties](../../extensibility/debugger/contingentproperties-class-internal-members.md)