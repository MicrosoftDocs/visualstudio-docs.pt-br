---
title: EXCEPTION_INFO | Microsoft Docs
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
- EXCEPTION_INFO
helpviewer_keywords:
- EXCEPTION_INFO structure
ms.assetid: d046957a-b97d-420b-b46b-c67cbaef709e
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 8a6feebb3be6f6f6f50a7d1a2ed3ff8525dacf6c
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51786876"
---
# <a name="exceptioninfo"></a>EXCEPTION_INFO
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Descreve uma exceção ou erro de tempo de execução gerado pelo programa que está sendo depurado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
typedef struct tagEXCEPTION_INFO {   
   IDebugProgram2* pProgram;  
   BSTR            bstrProgramName;  
   BSTR            bstrExceptionName;  
   DWORD           dwCode;  
   EXCEPTION_STATE dwState;  
   GUID            guidType;  
} EXCEPTION_INFO;  
```  
  
```csharp  
public struct EXCEPTION_INFO {   
   public IDebugProgram2 pProgram;  
   public string         bstrProgramName;  
   public string         bstrExceptionName;  
   public uint           dwCode;  
   public uint           dwState;  
   public Guid           guidType;  
};  
```  
  
## <a name="members"></a>Membros  
 pProgram  
 O [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) objeto que representa o programa no qual a exceção ocorreu.  
  
 bstrProgramName  
 O nome do programa no qual a exceção ocorreu.  
  
 bstrExceptionName  
 O nome da exceção.  
  
 dwCode  
 O código de identificação para o erro de exceção ou tempo de execução.  
  
 dwState  
 Um valor a partir de [EXCEPTION_STATE](../../../extensibility/debugger/reference/exception-state.md) enumeração que define o estado da exceção.  
  
 guidType  
 O identificador de idioma GUID, seja `guidLang` ou `guidEng`.  
  
## <a name="remarks"></a>Comentários  
 Essa estrutura é passada como um parâmetro para o [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md) e o [RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md) métodos. Essa estrutura também é passada para o [GetException](../../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md) método a ser preenchido.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [EXCEPTION_STATE](../../../extensibility/debugger/reference/exception-state.md)   
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)   
 [RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md)   
 [GetException](../../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md)

