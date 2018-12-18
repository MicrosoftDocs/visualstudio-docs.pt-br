---
title: Campo m_stateObject | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- m_stateObject field, Task class [.NET Framework debug engines]
ms.assetid: 68c54b22-3e1c-4031-b9c7-b972c519d8a0
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 3231f63d91e8393e5fa1417d97202d1b46cdd571
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51732358"
---
# <a name="mstateobject-field"></a>Campo m_stateObject
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Um objeto que representa os dados que usará a ação.  
  
 **Namespace:** <xref:System.Threading.Tasks?displayProperty=fullName>  
  
 **Assembly:** mscorlib (em mscorlib. dll)  
  
 Porque você não pode acessar esse membro interno do .NET Framework, a sintaxe a seguir é fornecida em comum Intermediate Language (CIL).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
.field assembly object m_stateObject  
```  
  
## <a name="remarks"></a>Comentários  
 Esse é o `state` parâmetro no <xref:System.Threading.Tasks.Task.%23ctor%2A> construtor. Também é o campo de suporte para o <xref:System.Threading.Tasks.Task.AsyncState%2A?displayProperty=fullName> propriedade.  
  
## <a name="see-also"></a>Consulte também  
 [Classe de tarefa](../../extensibility/debugger/task-class-internal-members.md)

