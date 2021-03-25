---
description: Especificou o tipo de informações a serem recuperadas para um processo.
title: PROCESS_INFO_FIELDS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROCESS_INFO_FIELDS
helpviewer_keywords:
- PROCESS_INFO_FIELDS enumeration
ms.assetid: 0d9cc345-3d3a-44d8-ae15-a67acb97a828
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d1f779352ce6b1217cd8af1e87988cb165b2dddc
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079625"
---
# <a name="process_info_fields"></a>PROCESS_INFO_FIELDS
Especificou o tipo de informações a serem recuperadas para um processo.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_PROCESS_INFO_FIELDS { 
   PIF_FILE_NAME             = 0x00000001,
   PIF_BASE_NAME             = 0x00000002,
   PIF_TITLE                 = 0x00000004,
   PIF_PROCESS_ID            = 0x00000008,
   PIF_SESSION_ID            = 0x00000010,
   PIF_ATTACHED_SESSION_NAME = 0x00000020,
   PIF_CREATION_TIME         = 0x00000040,
   PIF_FLAGS                 = 0x00000080,
   PIF_ALL                   = 0x000000ff
};
typedef DWORD PROCESS_INFO_FIELDS;
```

```csharp
public enum enum_PROCESS_INFO_FIELDS { 
   PIF_FILE_NAME             = 0x00000001,
   PIF_BASE_NAME             = 0x00000002,
   PIF_TITLE                 = 0x00000004,
   PIF_PROCESS_ID            = 0x00000008,
   PIF_SESSION_ID            = 0x00000010,
   PIF_ATTACHED_SESSION_NAME = 0x00000020,
   PIF_CREATION_TIME         = 0x00000040,
   PIF_FLAGS                 = 0x00000080,
   PIF_ALL                   = 0x000000ff
};
```

## <a name="fields"></a>Campos
 `PIF_FILE_NAME`\
 Inicializar/usar o `bstrFileName` campo da estrutura de [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md) .

 `PIF_BASE_NAME`\
 Inicializar/usar o `bstrBaseName` campo da `PROCESS_INFO` estrutura.

 `PIF_TITLE`\
 Inicializar/usar o `bstrTitle` campo da `PROCESS_INFO` estrutura.

 `PIF_PROCESS_ID`\
 Inicializar/usar o `ProcessId` campo da `PROCESS_INFO` estrutura.

 `PIF_SESSION_ID`\
 Inicializar/usar o `dwSessionId` campo da `PROCESS_INFO` estrutura.

 `PIF_ATTACHED_SESSION_NAME`\
 Inicializar/usar o `bstrAttachedSessionName` campo da `PROCESS_INFO` estrutura.

 `PIF_CREATION_TIME`\
 Inicializar/usar o `CreationTime` campo da `PROCESS_INFO` estrutura.

 `PIF_FLAGS`\
 Inicializar/usar o `Flags` campo da `PROCESS_INFO` estrutura.

 `PIF_ALL`\
 Preenche todos os campos.

## <a name="remarks"></a>Comentários
 Passado para o método [GetInfo](../../../extensibility/debugger/reference/idebugprocess2-getinfo.md) para indicar quais campos da estrutura de [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md) devem ser inicializados.

 Também usado no `Fields` campo da `PROCESS_INFO` estrutura para indicar quais campos são usados e válidos.

 Esses sinalizadores podem ser combinados com uma operadora de bits `OR` .

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)
