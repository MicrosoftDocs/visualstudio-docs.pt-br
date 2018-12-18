---
title: BP_ERROR_TYPE | Microsoft Docs
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
- BP_ERROR_TYPE
helpviewer_keywords:
- BP_ERROR_TYPE enumeration
ms.assetid: c483eaab-db29-46de-bfdb-5c2a9a9cfb68
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 61ec31973d1de69b9b276456465b31c429d77469
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51725842"
---
# <a name="bperrortype"></a>BP_ERROR_TYPE
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Especifica o tipo de erro de um ponto de interrupção.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
enum enum_BP_ERROR_TYPE {   
   BPET_NONE            = 0x00000000,  
   BPET_TYPE_WARNING    = 0x00000001,  
   BPET_TYPE_ERROR      = 0x00000002,  
   BPET_SEV_HIGH        = 0x0F000000,  
   BPET_SEV_GENERAL     = 0x07000000,  
   BPET_SEV_LOW         = 0x01000000,  
   BPET_TYPE_MASK       = 0x0000ffff,  
   BPET_SEV_MASK        = 0xffff0000,  
   BPET_GENERAL_WARNING = BPET_SEV_GENERAL | BPET_TYPE_WARNING,  
   BPET_GENERAL_ERROR   = BPET_SEV_GENERAL | BPET_TYPE_ERROR,  
   BPET_ALL             = 0xffffffff  
};  
typedef DWORD BP_ERROR_TYPE;  
```  
  
```csharp  
public enum enum_BP_ERROR_TYPE {   
   BPET_NONE            = 0x00000000,  
   BPET_TYPE_WARNING    = 0x00000001,  
   BPET_TYPE_ERROR      = 0x00000002,  
   BPET_SEV_HIGH        = 0x0F000000,  
   BPET_SEV_GENERAL     = 0x07000000,  
   BPET_SEV_LOW         = 0x01000000,  
   BPET_TYPE_MASK       = 0x0000ffff,  
   BPET_SEV_MASK        = 0xffff0000,  
   BPET_GENERAL_WARNING = BPET_SEV_GENERAL | BPET_TYPE_WARNING,  
   BPET_GENERAL_ERROR   = BPET_SEV_GENERAL | BPET_TYPE_ERROR,  
   BPET_ALL             = 0xffffffff  
};  
```  
  
## <a name="members"></a>Membros  
 BPET_NONE  
 Não especifica que nenhum erro de ponto de interrupção.  
  
 BPET_TYPE_WARNING  
 Especifica um erro de ponto de interrupção de estilo de aviso.  
  
 BPET_TYPE_ERROR  
 Especifica um erro de ponto de interrupção de estilo de erro.  
  
 BPET_SEV_HIGH  
 Especifica um erro de ponto de interrupção de alta gravidade.  
  
 BPET_SEV_GENERAL  
 Especifica um erro de ponto de interrupção de severidade média.  
  
 BPET_SEV_LOW  
 Especifica um erro de ponto de interrupção de baixa severidade.  
  
 BPET_TYPE_MASK  
 Especifica um erro de ponto de interrupção de estilo de máscara.  
  
 BPET_SEV_MASK  
 Especifica um erro de ponto de interrupção de gravidade de máscara de estilo.  
  
 BPET_GENERAL_WARNING  
 Especifica um erro de ponto de interrupção de estilo de aviso geral.  
  
 BPET_GENERAL_ERROR  
 Especifica um erro de ponto de interrupção de estilo de erro geral.  
  
 BPET_ALL  
 Especifica todos os tipos de erros de ponto de interrupção.  
  
## <a name="remarks"></a>Comentários  
 Esses valores podem ser combinados com um bit a bit `OR` e é usado para o `dwType` membro a [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md) estrutura. Passado como um parâmetro para o [EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md) método.  
  
 Um tipo de erro de ponto de interrupção é composto de um tipo e severidade. Isso significa que um tipo de erro de ponto de interrupção nunca é apenas um tipo (por exemplo, `BPET_TYPE_ERROR`,) ou uma severidade (por exemplo, `BPET_SEV_GENERAL`) por si só. `BPET_GENERAL_WARNING` e `BPET_GENERAL_ERROR` fornecem valores predefinidos para pontos de interrupção de aviso e erro geral.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)   
 [EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)

