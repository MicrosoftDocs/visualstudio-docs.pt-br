---
title: PROCESS_INFO_FLAGS | Microsoft Docs
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
- PROCESS_INFO_FLAGS
helpviewer_keywords:
- PROCESS_INFO_FLAGS enumeration
ms.assetid: 696951ce-701a-40c2-ac8c-b897f3aae6e2
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 453c976ec4dd1c0c0b1c1e67592f840c17a9ac9e
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51726795"
---
# <a name="processinfoflags"></a>PROCESS_INFO_FLAGS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Descreve ou especifica as propriedades de um processo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
enum enum_PROCESS_INFO_FLAGS {   
   PIFLAG_SYSTEM_PROCESS    = 0x00000001,  
   PIFLAG_DEBUGGER_ATTACHED = 0x00000002,  
   PIFLAG_PROCESS_STOPPED   = 0x00000004,  
   PIFLAG_PROCESS_RUNNING   = 0x00000008,  
};  
typedef DWORD PROCESS_INFO_FLAGS;  
```  
  
```csharp  
enum enum_PROCESS_INFO_FLAGS {   
   PIFLAG_SYSTEM_PROCESS    = 0x00000001,  
   PIFLAG_DEBUGGER_ATTACHED = 0x00000002,  
   PIFLAG_PROCESS_STOPPED   = 0x00000004,  
   PIFLAG_PROCESS_RUNNING   = 0x00000008,  
};  
```  
  
## <a name="members"></a>Membros  
 PIFLAG_SYSTEM_PROCESS  
 Indica que o processo é um processo do sistema.  
  
 PIFLAG_DEBUGGER_ATTACHED  
 Indica que o processo está sendo depurado por um depurador. Pode ser um [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] depurador, ou ele pode ser de alguns outro depurador, por exemplo, o WinDbg.  
  
 PIFLAG_PROCESS_STOPPED  
 Indica que o processo é interrompido. Válido somente se `PIFLAG_DEBUGGER_ATTACHED` também for especificado. Disponível em [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)] e versões posteriores.  
  
 PIFLAG_PROCESS_RUNNING  
 Indica que o processo está em execução. Válido somente se `PIFLAG_DEBUGGER_ATTACHED` também for especificado. Disponível em [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)] e versões posteriores.  
  
## <a name="remarks"></a>Comentários  
 Usado para o `Flags` membro a [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md) estrutura.  
  
 Esses sinalizadores podem ser combinados com um bit a bit `OR`.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)

