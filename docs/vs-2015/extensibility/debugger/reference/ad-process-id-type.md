---
title: AD_PROCESS_ID_TYPE | Microsoft Docs
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
- AD_PROCESS_ID_TYPE
helpviewer_keywords:
- AD_PROCESS_ID_TYPE enumeration
ms.assetid: 0aab80e9-285a-4697-94ac-c864d42a6aaa
caps.latest.revision: 7
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 7819439f618dfbf2b33bef08d6ebf8aa2290cc25
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51810072"
---
# <a name="adprocessidtype"></a>AD_PROCESS_ID_TYPE
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Especifica como interpretar uma ID de processo na [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) estrutura.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
enum enum_AD_PROCESS_ID {  
   AD_PROCESS_ID_SYSTEM = 0,  
   AD_PROCESS_ID_GUID   = 1  
};  
typedef DWORD AD_PROCESS_ID_TYPE;  
```  
  
```csharp  
public enum enum_AD_PROCESS_ID {  
   AD_PROCESS_ID_SYSTEM = 0,  
   AD_PROCESS_ID_GUID   = 1  
};  
```  
  
## <a name="members"></a>Membros  
 AD_PROCESS_ID_SYSTEM  
 ID do processo é um identificador de sistema. Use o `ProcessId.dwProcessId` campo do [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) estrutura.  
  
 AD_PROCESS_ID_GUID  
 ID do processo é um GUID. Use o `ProcessId.guidProcessId` campo do `AD_PROCESS_ID` estrutura.  
  
## <a name="remarks"></a>Comentários  
 Usado para o `ProcessIdType` membro do [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) estrutura para identificar o tipo de ID do processo que está contido na estrutura. Determina como interpretar o `ProcessId` union na estrutura.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)

