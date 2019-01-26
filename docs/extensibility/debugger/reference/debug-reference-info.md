---
title: DEBUG_REFERENCE_INFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- DEBUG_REFERENCE_INFO
helpviewer_keywords:
- DEBUG_REFERENCE_INFO structure
ms.assetid: 24b83d00-d756-42a1-8083-730f998761dc
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: eb3b9f0c89d350fece18d49eee34d14d01d03352
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55007666"
---
# <a name="debugreferenceinfo"></a>DEBUG_REFERENCE_INFO
Descreve uma referência.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef struct tagDEBUG_REFERENCE_INFO {   
   DEBUGREF_INFO_FLAGS dwFields;  
   BSTR                bstrName;  
   BSTR                bstrType;  
   BSTR                bstrValue;  
   DBG_ATTRIB_FLAGS    dwAttrib;  
   REFERENCE_TYPE.     dwRefType;  
   IDebugReference2*   m_pReference;  
} DEBUG_REFERENCE_INFO;  
```  
  
```csharp  
public struct DEBUG_REFERENCE_INFO {   
   public uint             dwFields;  
   public string           bstrName;  
   public string           bstrType;  
   public string           bstrValue;  
   public ulong            dwAttrib;  
   public uint.            dwRefType;  
   public IDebugReference2 m_pReference;  
};  
```  
  
## <a name="members"></a>Membros  
 dwFields  
 Uma combinação de sinalizadores do [DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md) enumeração que especifica quais campos são preenchidos.  
  
 bstrName  
 O nome especificado pelo usuário da [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) objeto.  
  
 bstrType  
 O tipo de referência como uma cadeia de caracteres formatada.  
  
 bstrValue  
 O valor de referência como uma cadeia de caracteres formatada  
  
 dwAttrib  
 Uma combinação de sinalizadores do [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md) enumeração que especifica os sinalizadores para os atributos de propriedade de depuração.  
  
 dwRefType  
 Um valor a partir de [REFERENCE_TYPE](../../../extensibility/debugger/reference/reference-type.md) enumeração que especifica se o tipo de referência é forte ou fraca.  
  
 m_pReference  
 Uma [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) objeto que especifica as informações de referência.  
  
## <a name="remarks"></a>Comentários  
 Essa estrutura é passada para uma chamada para o [GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md) método a ser preenchido. Essa estrutura também é retornada como parte de uma lista a partir de [IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md) interface que, por sua vez, é retornado de uma chamada para o [EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md) método.  
  
## <a name="requirements"></a>Requisitos  
 Header: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)   
 [DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md)   
 [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)   
 [REFERENCE_TYPE](../../../extensibility/debugger/reference/reference-type.md)   
 [GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)   
 [EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)   
 [IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)