---
title: IDebugProgramDestroyEventFlags2 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- IDebugProgramDestroyEventFlags2 interface
ms.assetid: d384ff71-dc71-40b9-a871-801f8b6a3418
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: f6b57206159ce00fbb79e9f9af1a6353588df76c
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31116328"
---
# <a name="idebugprogramdestroyeventflags2"></a>IDebugProgramDestroyEventFlags2
Permite que um mecanismo de depuração substituir o comportamento padrão da [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] interface do usuário quando você encerrar uma sessão de depuração.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugProgramDestroyEventFlags2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 Essa interface é implementada por mecanismos de depuração. É útil para hosts que podem criar e destruir vários programas durante o tempo de vida de um processo.  
  
## <a name="methods"></a>Métodos  
 A tabela a seguir mostra os métodos de `IDebugProgramDestroyEventFlags2`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetFlags](../../../extensibility/debugger/reference/idebugprogramdestroyeventflags2-getflags.md)|Recupera o programa destruir sinalizadores.|  
  
## <a name="remarks"></a>Comentários  
 O comportamento padrão da [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] interface do usuário é voltar ao modo de design depois que todos os programas enviou um programa destruir o evento. Essa interface permite que um mecanismo de depuração alterar esse comportamento.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: Msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll