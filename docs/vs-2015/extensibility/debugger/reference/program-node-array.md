---
title: PROGRAM_NODE_ARRAY | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- PROGRAM_NODE_ARRAY
helpviewer_keywords:
- PROGRAM_NODE_ARRAY structure
ms.assetid: 8eeea600-eda5-4b7c-868a-0b86d177b0a5
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: e325e7b543e8b1a86687dd33edcc34b3ae88d6b3
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49817659"
---
# <a name="programnodearray"></a>PROGRAM_NODE_ARRAY
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Contém uma matriz de objetos que descrevem os programas de interesse.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef struct tagPROGRAM_NODE_ARRAY {  
   DWORD                dwCount;  
   IDebugProgramNode2** Members;  
} PROGRAM_NODE_ARRAY;  
```  
  
```csharp  
public struct tagPROGRAM_NODE_ARRAY {  
   public uint                 dwCount;  
   public IDebugProgramNode2[] Members;  
}  
```  
  
## <a name="members"></a>Membros  
 dwCount  
 Número de objetos no `Members` matriz.  
  
 Membros  
 Uma matriz de [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) objetos que descrevem os programas solicitados.  
  
## <a name="remarks"></a>Comentários  
 Essa estrutura é parte do [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md) estrutura que por sua vez é preenchida por uma chamada para o [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md) método.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)   
 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)   
 [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)

