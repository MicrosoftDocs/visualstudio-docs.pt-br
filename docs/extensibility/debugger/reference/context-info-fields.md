---
title: CONTEXT_INFO_FIELDS | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- CONTEXT_INFO_FIELDS
helpviewer_keywords:
- CONTEXT_INFO_FIELDS enumeration
ms.assetid: ef436bd3-738e-47e8-828c-8febce752439
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: a6833e93e7947ee5013a8879c6a5fc949de9fb20
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49929459"
---
# <a name="contextinfofields"></a>CONTEXT_INFO_FIELDS
Especifica quais informações devem ser recuperadas sobre um contexto de memória.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
enum enum_CONTEXT_INFO_FIELDS {   
   CIF_MODULEURL =       0x00000001,  
   CIF_FUNCTION =        0x00000002,  
   CIF_FUNCTIONOFFSET =  0x00000004,  
   CIF_ADDRESS =         0x00000008,  
   CIF_ADDRESSOFFSET =   0x00000010,  
   CIF_ADDRESSABSOLUTE = 0x00000020,  
   CIF_ALLFIELDS =       0x0000003f  
};  
typedef DWORD CONTEXT_INFO_FIELDS;  
```  
  
```csharp  
public enum enum_CONTEXT_INFO_FIELDS {  
   CIF_MODULEURL =       0x00000001,  
   CIF_FUNCTION =        0x00000002,  
   CIF_FUNCTIONOFFSET =  0x00000004,  
   CIF_ADDRESS =         0x00000008,  
   CIF_ADDRESSOFFSET =   0x00000010,  
   CIF_ADDRESSABSOLUTE = 0x00000020,  
   CIF_ALLFIELDS =       0x0000003f  
};  
```  
  
## <a name="members"></a>Membros  
 CIF_MODULEURL  
 Inicialização/usar o `bstrModuleUrl` campo do [CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md) estrutura.  
  
 CIF_FUNCTION  
 Inicialização/usar o `bstrFunction` campo do `CONTEXT_INFO` estrutura.  
  
 CIF_FUNCTIONOFFSET  
 Inicialização/usar o `posFunctionOffset` campo do `CONTEXT_INFO` estrutura.  
  
 CIF_ADDRESS  
 Inicialização/usar o `bstrAddress` campo do `CONTEXT_INFO` estrutura.  
  
 CIF_ADDRESSOFFSET  
 Inicialização/usar o `bstrAddressOffset` campo do `CONTEXT_INFO` estrutura.  
  
 CIF_ALLFIELDS  
 Inicialização/usar todos os campos do `CONTEXT_INFO` estrutura.  
  
## <a name="remarks"></a>Comentários  
 Esses valores são passados a um parâmetro para o [GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md) método para indicar quais campos da [CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md) são de estrutura a ser inicializado.  
  
 Esses sinalizadores também são usados para indicar quais campos do `CONTEXT_INFO` estrutura são usados e válidos quando a estrutura é retornada.  
  
 Esses valores podem ser combinados com um OR bit a bit.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md)   
 [GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)