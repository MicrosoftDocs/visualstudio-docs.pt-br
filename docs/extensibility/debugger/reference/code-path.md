---
title: CODE_PATH | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- CODE_PATH
helpviewer_keywords:
- CODE_PATH structure
ms.assetid: 2d4b2890-4c9d-47e1-83c0-df9c6436427f
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3d8459fd900edd0aba4532a8ce3e082dc4f300eb
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54966213"
---
# <a name="codepath"></a>CODE_PATH
Descreve uma chamada de método ou função.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef struct tagCODE_PATH {   
   BSTR                bstrName;  
   IDebugCodeContext2* pCode;  
} CODE_PATH;  
```  
  
```csharp  
public struct CODE_PATH {  
   public string            bstrName;  
   public IDebugCodeContext pCode;  
}  
```  
  
## <a name="members"></a>Membros  
 bstrName  
 O nome do caminho do código.  
  
 pCode  
 O [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) objeto identifica onde no código para entrar em uma função.  
  
## <a name="remarks"></a>Comentários  
 Essa estrutura é usada para implementar a entrar em uma função. [EnumCodePaths](../../../extensibility/debugger/reference/idebugprogram2-enumcodepaths.md) retorna todas as chamadas do local atual no programa que está sendo depurado. Essa estrutura representa uma chamada.  
  
## <a name="requirements"></a>Requisitos  
 Header: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)   
 [EnumCodePaths](../../../extensibility/debugger/reference/idebugprogram2-enumcodepaths.md)