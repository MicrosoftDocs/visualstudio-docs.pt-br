---
description: Especifica quais informações sobre um thread serão recuperadas.
title: THREADPROPERTY_FIELDS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- THREADPROPERTY_FIELDS
helpviewer_keywords:
- THREADPROPERTY_FIELDS enumeration
ms.assetid: 5b88acb9-03ea-4c29-a788-f0087dccbe23
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 81d185a80761e42e706dc3ef36da056bb37b0b1c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070863"
---
# <a name="threadproperty_fields"></a>THREADPROPERTY_FIELDS
Especifica quais informações sobre um thread serão recuperadas.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_THREADPROPERTY_FIELDS { 
   TPF_ID           = 0x0001,
   TPF_SUSPENDCOUNT = 0x0002,
   TPF_STATE        = 0x0004,
   TPF_PRIORITY     = 0x0008,
   TPF_NAME         = 0x0010,
   TPF_LOCATION     = 0x0020,
   TPF_ALLFIELDS    = 0xffffffff
};
typedef DWORD THREADPROPERTY_FIELDS;
```

```csharp
public enum enum_THREADPROPERTY_FIELDS { 
   TPF_ID           = 0x0001,
   TPF_SUSPENDCOUNT = 0x0002,
   TPF_STATE        = 0x0004,
   TPF_PRIORITY     = 0x0008,
   TPF_NAME         = 0x0010,
   TPF_LOCATION     = 0x0020,
   TPF_ALLFIELDS    = 0xffffffff
};
```

## <a name="fields"></a>Campos
 `TPF_ID`\
 Inicializar/usar o `dwThreadId` campo da estrutura [threadproperties](../../../extensibility/debugger/reference/threadproperties.md) .

 `TPF_SUSPENDCOUNT`\
 Inicializar/usar o `dwSuspendCount` campo da `THREADPROPERTIE` estrutura S.

 `TPF_STATE`\
 Inicializar/usar o `dwThreadState` campo da `THREADPROPERTIE` estrutura S.

 `TPF_PRIORITY`\
 Inicializar/usar o `bstrPriority` campo da `THREADPROPERTIE` estrutura S.

 `TPF_NAME`\
 Inicializar/usar o `bstrName` campo da `THREADPROPERTIE` estrutura S.

 `TPF_LOCATION`\
 Inicializar/usar o `bstrLocation` campo da `THREADPROPERTIE` estrutura S.

 `TPF_ALLFIELDS`\
 Especifica todos os campos.

## <a name="remarks"></a>Comentários
 Esses valores são passados como um argumento para o método [Getthreadproperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md) para indicar quais campos da estrutura [threadproperties](../../../extensibility/debugger/reference/threadproperties.md) devem ser inicializados.

 Esses valores também são usados em `dwFields` membro da `THREADPROPERTIES` estrutura para indicar quais campos são usados e válidos.

 Esses sinalizadores podem ser combinados com uma operadora de bits `OR` .

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)
- [GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)
