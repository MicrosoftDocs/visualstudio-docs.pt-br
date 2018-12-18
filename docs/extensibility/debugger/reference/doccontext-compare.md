---
title: DOCCONTEXT_COMPARE | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- DOCCONTEXT_COMPARE
helpviewer_keywords:
- DOCCONTEXT_COMPARE enumeration
ms.assetid: ed947c34-b07e-4b69-8381-b6e7cb842862
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 8f092666833b80dd59ed4b7b3345c379078ce2bf
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49862951"
---
# <a name="doccontextcompare"></a>DOCCONTEXT_COMPARE
Especifica os critérios para comparar dois contextos de documento.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
enum enum_DOCCONTEXT_COMPARE {   
   DOCCONTEXT_EQUAL         = 0x0001,  
   DOCCONTEXT_LESS_THAN     = 0x0002,  
   DOCCONTEXT_GREATER_THAN  = 0x0003,  
   DOCCONTEXT_SAME_DOCUMENT = 0x0004  
};  
typedef DWORD DOCCONTEXT_COMPARE;  
```  
  
```csharp  
enum enum_DOCCONTEXT_COMPARE {   
   DOCCONTEXT_EQUAL         = 0x0001,  
   DOCCONTEXT_LESS_THAN     = 0x0002,  
   DOCCONTEXT_GREATER_THAN  = 0x0003,  
   DOCCONTEXT_SAME_DOCUMENT = 0x0004  
};  
```  
  
## <a name="members"></a>Membros  
 DOCCONTEXT_EQUAL  
 Localize o contexto do documento primeiro na lista que é igual para o contexto do documento de destino.  
  
 DOCCONTEXT_LESS_THAN  
 Localize o contexto do documento primeiro na lista que é menor que o contexto do documento de destino.  
  
 DOCCONTEXT_GREATER_THAN  
 Localize o contexto do documento primeiro na lista que é maior que o contexto do documento de destino.  
  
 DOCCONTEXT_SAME_DOCUMENT  
 Localize o contexto do documento primeiro na lista que está no mesmo documento que o contexto do documento de destino.  
  
## <a name="remarks"></a>Comentários  
 Passado como um argumento para o [comparar](../../../extensibility/debugger/reference/idebugdocumentcontext2-compare.md) método.  
  
 Esses valores são usados para especificar um critério de comparação para localizar o contexto do documento primeiro em uma lista. Um contexto de documento é dada uma lista de contextos de documento para comparar a próprio em relação a por meio de `IDebugDocumentContext2::Compare` método. O contexto do documento primeiro na lista para o qual o operador de comparação é `true` , em seguida, será retornado.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [Compare](../../../extensibility/debugger/reference/idebugdocumentcontext2-compare.md)