---
title: PROCESS_INFO_FLAGS | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- PROCESS_INFO_FLAGS
helpviewer_keywords:
- PROCESS_INFO_FLAGS enumeration
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 04bc34de6e7ecbc438cfc63ed08c684cf4224366
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49917018"
---
# <a name="processinfoflags"></a>PROCESS_INFO_FLAGS

Descreve ou especifica as propriedades de um processo.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_PROCESS_INFO_FLAGS { 
   PIFLAG_SYSTEM_PROCESS    = 0x00000001,
   PIFLAG_DEBUGGER_ATTACHED = 0x00000002,
   PIFLAG_PROCESS_STOPPED   = 0x00000004,
   PIFLAG_PROCESS_RUNNING   = 0x00000008,
};
typedef DWORD PROCESS_INFO_FLAGS;
```

```csharp
enum enum_PROCESS_INFO_FLAGS { 
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
Indica que o processo está sendo depurado por um depurador. Pode ser um [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] depurador, ou ele pode ser de alguns outro depurador, por exemplo, o WinDbg.

PIFLAG_PROCESS_STOPPED  
Indica que o processo é interrompido. Válido somente se `PIFLAG_DEBUGGER_ATTACHED` também for especificado. Disponível no Visual Studio 2005 e versões posteriores.

PIFLAG_PROCESS_RUNNING  
Indica que o processo está em execução. Válido somente se `PIFLAG_DEBUGGER_ATTACHED` também for especificado. Disponível no Visual Studio 2005 e versões posteriores.

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