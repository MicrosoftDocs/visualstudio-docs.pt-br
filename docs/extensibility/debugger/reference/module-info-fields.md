---
description: Especifica os sinalizadores para as informações do módulo de depuração.
title: MODULE_INFO_FIELDS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MODULE_INFO_FIELDS
helpviewer_keywords:
- MODULE_INFO_FIELDS enumeration
ms.assetid: 8bed85f4-235f-4192-b58f-5fad7a4d7a78
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4c530caa530a230dc0fc0344a31e0ab7793f336f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079768"
---
# <a name="module_info_fields"></a>MODULE_INFO_FIELDS
Especifica os sinalizadores para as informações do módulo de depuração.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_MODULE_INFO_FIELDS { 
   MIF_NONE              = 0x0000,
   MIF_NAME              = 0x0001,
   MIF_URL               = 0x0002,
   MIF_VERSION           = 0x0004,
   MIF_DEBUGMESSAGE      = 0x0008,
   MIF_LOADADDRESS       = 0x0010,
   MIF_PREFFEREDADDRESS  = 0x0020,
   MIF_SIZE              = 0x0040,
   MIF_LOADORDER         = 0x0080,
   MIF_TIMESTAMP         = 0x0100,
   MIF_URLSYMBOLLOCATION = 0x0200,
   MIF_FLAGS             = 0x0400,
   MIF_ALLFIELDS         = 0x07ff
};
typedef DWORD MODULE_INFO_FIELDS;
```

```csharp
public enum enum_MODULE_INFO_FIELDS { 
   MIF_NONE              = 0x0000,
   MIF_NAME              = 0x0001,
   MIF_URL               = 0x0002,
   MIF_VERSION           = 0x0004,
   MIF_DEBUGMESSAGE      = 0x0008,
   MIF_LOADADDRESS       = 0x0010,
   MIF_PREFFEREDADDRESS  = 0x0020,
   MIF_SIZE              = 0x0040,
   MIF_LOADORDER         = 0x0080,
   MIF_TIMESTAMP         = 0x0100,
   MIF_URLSYMBOLLOCATION = 0x0200,
   MIF_FLAGS             = 0x0400,
   MIF_ALLFIELDS         = 0x07ff
};
```

## <a name="fields"></a>Campos
 `MIF_NONE`\
 Inicializar/usar nenhum dos campos na estrutura.

 `MIF_NAME`\
 Inicializar/usar o `m_bstrName` campo na estrutura de [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md) .

 `MIF_URL`\
 Inicializar/usar o `m_bstrUrl` campo na `MODULE_INFO` estrutura.

 `MIF_VERSION`\
 Inicializar/usar o `m_bstrVersion` campo na `MODULE_INFO` estrutura.

 `MIF_DEBUGMESSAGE`\
 Inicializar/usar o `m_bstrDebugMessage` campo na `MODULE_INFO` estrutura.

 `MIF_LOADADDRESS`\
 Inicializar/usar o `m_addrLoadAddress` campo na `MODULE_INFO` estrutura.

 `MIF_PREFFEREDADDRESS`\
 Inicializar/usar o `m_addrPreferredLoadAddress` campo na `MODULE_INFO` estrutura.

 `MIF_SIZE`\
 Inicializar/usar o `m_dwSize` campo na `MODULE_INFO` estrutura.

 `MIF_LOADORDER`\
 Inicializar/usar o `m_dwLoadOrder` campo na `MODULE_INFO` estrutura.

 `MIF_TIMESTAMP`\
 Inicializar/usar o `m_TimeStamp` campo na `MODULE_INFO` estrutura.

 `MIF_URLSYMBOLLOCATION`\
 Inicializar/usar o `m_bstrUrlSymbolLocation` campo na `MODULE_INFO` estrutura.

 `MIF_FLAGS`\
 Inicializar/usar o `m_dwModuleFlags` campo na `MODULE_INFO` estrutura.

 `MIF_ALLFIELDS`\
 Inicializar/usar todos os campos na `MODULE_INFO` estrutura.

## <a name="remarks"></a>Comentários
 Esses valores são passados como um argumento para o método [GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md) para indicar quais campos da estrutura de [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md) devem ser inicializados.

 Esses valores também são usados na `MODULE_INFO` estrutura para indicar quais campos são usados e válidos.

 Esses sinalizadores podem ser combinados com uma operadora de bits `OR` .

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)
