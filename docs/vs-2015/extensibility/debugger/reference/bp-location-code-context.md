---
title: BP_LOCATION_CODE_CONTEXT | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BP_LOCATION_CODE_CONTEXT
helpviewer_keywords:
- BP_LOCATION_CODE_CONTEXT structure
ms.assetid: 37412896-021a-4f73-9bb7-4125502c2e18
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1d703a35c0b4e065bcf3515fe063c7620382666f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153487"
---
# <a name="bp_location_code_context"></a>BP_LOCATION_CODE_CONTEXT
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Descreve o local de um ponto de interrupção que está associado diretamente a um endereço no programa que está sendo depurado.  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
typedef struct _BP_LOCATION_CODE_CONTEXT {   
   IDebugCodeContext2* pCodeContext;  
} BP_LOCATION_CODE_CONTEXT;  
```  
  
## <a name="members"></a>Membros  
 pCodeContext  
 O objeto [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) que identifica a posição do ponto de interrupção no código.  
  
## <a name="remarks"></a>Comentários  
 Essa estrutura é um membro da estrutura de [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) como parte de uma União.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg. h  
  
 Namespace: Microsoft. VisualStudio. Debugger. Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte Também  
 [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)   
 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
