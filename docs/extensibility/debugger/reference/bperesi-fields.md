---
description: Especifica as informações a serem recuperadas sobre uma resolução com falha de um ponto de interrupção.
title: BPERESI_FIELDS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BPERESI_FIELDS
helpviewer_keywords:
- BPERESI_FIELDS enumeration
ms.assetid: dd7dd89c-1043-46a1-a929-099cc039c344
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8164f377e56c884149fb0711286d7702fe92eb82
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067680"
---
# <a name="bperesi_fields"></a>BPERESI_FIELDS
Especifica as informações a serem recuperadas sobre uma resolução com falha de um ponto de interrupção.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_BPERESI_FIELDS {
    PERESI_BPRESLOCATION = 0x0001,
    BPERESI_PROGRAM      = 0x0002,
    BPERESI_THREAD       = 0x0004,
    BPERESI_MESSAGE      = 0x0008,
    BPERESI_TYPE         = 0x0010,
    BPERESI_ALLFIELDS    = 0xffffffff
};
typedef DWORD BPERESI_FIELDS;
```

```csharp
public enum enum_BPERESI_FIELDS {
    PERESI_BPRESLOCATION = 0x0001,
    BPERESI_PROGRAM      = 0x0002,
    BPERESI_THREAD       = 0x0004,
    BPERESI_MESSAGE      = 0x0008,
    BPERESI_TYPE         = 0x0010,
    BPERESI_ALLFIELDS    = 0xffffffff
};
```

## <a name="fields"></a>Campos
`PERESI_BPRESLOCATION`\
Inicializar/usar o `bpResLocation` campo (local de resolução de ponto de interrupção) da estrutura de [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md) .

`BPERESI_PROGRAM`\
Inicializar/usar o `pProgram` campo da `BP_ERROR_RESOLUTION_INFO` estrutura.

`BPERESI_THREAD`\
Inicializar/usar o `pThread` campo da `BP_ERROR_RESOLUTION_INFO` estrutura.

`BPERESI_MESSAGE`\
Inicializar/usar o `bstrMessage` campo da `BP_ERROR_RESOLUTION_INFO` estrutura.

`BPERESI_TYPE`\
Inicializar/usar o `dwType` campo (tipo de ponto de interrupção) da `BP_ERROR_RESOLUTION_INFO` estrutura.

`BPERESI_ALLFIELDS`\
Inicializar/usar todos os campos da `BP_ERROR_RESOLUTION_INFO` estrutura.

## <a name="remarks"></a>Comentários
Passado como um parâmetro para o método [GetResolutionInfo](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md) para indicar quais campos da estrutura de [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md) devem ser inicializados.

Esses valores também são usados para indicar quais campos na `BP_ERROR_RESOLUTION_INFO` estrutura são usados e válidos quando essa estrutura é retornada.

Esses valores podem ser combinados com um bit a bit `OR` .

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)
- [GetResolutionInfo](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)
