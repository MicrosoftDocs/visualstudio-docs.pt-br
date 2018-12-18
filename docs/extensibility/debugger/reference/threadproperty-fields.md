---
title: THREADPROPERTY_FIELDS | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- THREADPROPERTY_FIELDS
helpviewer_keywords:
- THREADPROPERTY_FIELDS enumeration
ms.assetid: 5b88acb9-03ea-4c29-a788-f0087dccbe23
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 44692c4715db3db8f65a85bd66a129b4d17e5138
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49855541"
---
# <a name="threadpropertyfields"></a>THREADPROPERTY_FIELDS
Especifica quais informações sobre um thread deve ser recuperado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
enum enum_THREADPROPERTY_FIELDS {   
   TPF_ID           = 0x0001,  
   TPF_SUSPENDCOUNT = 0x0002,  
   TPF_STATE        = 0x0004,  
   TPF_PRIORITY     = 0x0008,  
   TPF_NAME         = 0x0010,  
   TPF_LOCATION     = 0x0020,  
   TPF_ALLFIELDS    = 0xffffffff  
};  
typedef DWORD THREADPROPERTY_FIELDS;  
```  
  
```csharp  
public enum enum_THREADPROPERTY_FIELDS {   
   TPF_ID           = 0x0001,  
   TPF_SUSPENDCOUNT = 0x0002,  
   TPF_STATE        = 0x0004,  
   TPF_PRIORITY     = 0x0008,  
   TPF_NAME         = 0x0010,  
   TPF_LOCATION     = 0x0020,  
   TPF_ALLFIELDS    = 0xffffffff  
};  
```  
  
## <a name="members"></a>Membros  
 TPF_ID  
 Inicialização/usar o `dwThreadId` campo do [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md) estrutura.  
  
 TPF_SUSPENDCOUNT  
 Inicialização/usar o `dwSuspendCount` campo do `THREADPROPERTIE`estrutura.  
  
 TPF_STATE  
 Inicialização/usar o `dwThreadState` campo do `THREADPROPERTIE`estrutura.  
  
 TPF_PRIORITY  
 Inicialização/usar o `bstrPriority` campo do `THREADPROPERTIE`estrutura.  
  
 TPF_NAME  
 Inicialização/usar o `bstrName` campo do `THREADPROPERTIE`estrutura.  
  
 TPF_LOCATION  
 Inicialização/usar o `bstrLocation` campo do `THREADPROPERTIE`estrutura.  
  
 TPF_ALLFIELDS  
 Especifica todos os campos.  
  
## <a name="remarks"></a>Comentários  
 Esses valores são passados como um argumento para o [GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md) método para indicar quais campos da [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md) são de estrutura a ser inicializado.  
  
 Esses valores também são usados no `dwFields` membro o `THREADPROPERTIES` estrutura para indicar quais campos são usados e válido.  
  
 Esses sinalizadores podem ser combinados com um bit a bit `OR`.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)   
 [GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)