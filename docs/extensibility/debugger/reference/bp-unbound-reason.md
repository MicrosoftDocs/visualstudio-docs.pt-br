---
title: BP_UNBOUND_REASON | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- BP_UNBOUND_REASON
helpviewer_keywords:
- BP_UNBOUND_REASON enumeration
ms.assetid: 939b6f9c-113b-471d-9f30-b03871af6285
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4d8dfc8e032eecc854a0572c8a7bd14b0c551df7
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55028615"
---
# <a name="bpunboundreason"></a>BP_UNBOUND_REASON
Fornece o motivo pelo qual que um ponto de interrupção foi desassociado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
enum enum_BP_UNBOUND_REASON {   
   BPUR_UNKNOWN           = 0x0000,  
   BPUR_CODE_UNLOADED     = 0x0002,  
   BPUR_BREAKPOINT_REBIND = 0x0003,  
   BPUR_BREAKPOINT_ERROR  = 0x0004  
};  
typedef DWORD BP_UNBOUND_REASON;  
```  
  
```csharp  
public enum enum_BP_UNBOUND_REASON {   
   BPUR_UNKNOWN           = 0x0000,  
   BPUR_CODE_UNLOADED     = 0x0002,  
   BPUR_BREAKPOINT_REBIND = 0x0003,  
   BPUR_BREAKPOINT_ERROR  = 0x0004  
};  
```  
  
## <a name="members"></a>Membros  
 BPUR_UNKNOWN  
 O motivo é desconhecido.  
  
 BPUR_CODE_UNLOADED  
 O código que contém o ponto de interrupção foi descarregado.  
  
 BPUR_BREAKPOINT_REBIND  
 O ponto de interrupção foram religado para um local diferente. Isso pode acontecer após editar e continuar as operações quando move o ponto de interrupção ou quando o ponto de interrupção é associado a um arquivo com um caminho que não é mais válido.  
  
 BPUR_ BREAKPOINT_ERROR  
 O ponto de interrupção é determinado em erro depois que ele está associado. Isso acontece com os pontos de interrupção gerenciados cujas condições não são mais válidas.  
  
## <a name="remarks"></a>Comentários  
 Retornado pela [GetReason](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getreason.md) método.  
  
## <a name="requirements"></a>Requisitos  
 Header: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [GetReason](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getreason.md)