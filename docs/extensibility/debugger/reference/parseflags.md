---
title: PARSEFLAGS | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- PARSEFLAGS
helpviewer_keywords:
- PARSEFLAGS enumeration
ms.assetid: 47943f0a-54cb-4493-a62e-5dba97bd4c35
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 7192483b4f2ce88235fc5e8d48f1d51ef71b442f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49913001"
---
# <a name="parseflags"></a>PARSEFLAGS
Especifica como analisar uma expressão.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
enum enum_PARSEFLAGS {   
   PARSE_EXPRESSION            = 0x0001,  
   PARSE_FUNCTION_AS_ADDRESS   = 0x0002,  
   PARSE_DESIGN_TIME_EXPR_EVAL = 0x1000  
};  
typedef DWORD PARSEFLAGS;  
```  
  
```csharp  
public enum enum_PARSEFLAGS {   
   PARSE_EXPRESSION            = 0x0001,  
   PARSE_FUNCTION_AS_ADDRESS   = 0x0002,  
   PARSE_DESIGN_TIME_EXPR_EVAL = 0x1000  
};  
```  
  
## <a name="members"></a>Membros  
 PARSE_EXPRESSION  
 Indica que a expressão não é uma instrução.  
  
 PARSE_FUNCTION_AS_ADDRESS  
 Indica que a expressão deve ser analisado (e avaliado mais tarde) como um endereço.  
  
 PARSE_DESIGN_TIME_EXPR_EVAL  
 Indica que a expressão está sendo analisada durante o tempo de design (ou seja, quando um designer estiver aberto).  
  
## <a name="remarks"></a>Comentários  
 Passado como um parâmetro para o [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) e [analisar](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) métodos.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)   
 [Analisar](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)