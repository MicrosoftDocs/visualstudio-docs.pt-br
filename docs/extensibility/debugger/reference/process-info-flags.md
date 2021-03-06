---
description: Descreve ou especifica as propriedades de um processo.
title: PROCESS_INFO_FLAGS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROCESS_INFO_FLAGS
helpviewer_keywords:
- PROCESS_INFO_FLAGS enumeration
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e192a51c2c371754778ecbe697d280d1b254f224
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102225325"
---
# <a name="process_info_flags"></a>PROCESS_INFO_FLAGS

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

## <a name="fields"></a>Campos

`PIFLAG_SYSTEM_PROCESS`\
Indica que o processo é um processo do sistema.

`PIFLAG_DEBUGGER_ATTACHED`\
Indica que o processo está sendo depurado por um depurador. Pode ser um [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] depurador ou pode ser outro depurador, por exemplo, WinDbg.

`PIFLAG_PROCESS_STOPPED`\
Indica que o processo foi interrompido. Válido somente se `PIFLAG_DEBUGGER_ATTACHED` também for especificado. Disponível no Visual Studio 2005 e posterior.

`PIFLAG_PROCESS_RUNNING`\
Indica que o processo está em execução. Válido somente se `PIFLAG_DEBUGGER_ATTACHED` também for especificado. Disponível no Visual Studio 2005 e posterior.

## <a name="remarks"></a>Comentários

Usado para o `Flags` membro da estrutura de [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md) .

Esses sinalizadores podem ser combinados com uma operadora de bits `OR` .

## <a name="requirements"></a>Requisitos

Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também

- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)
