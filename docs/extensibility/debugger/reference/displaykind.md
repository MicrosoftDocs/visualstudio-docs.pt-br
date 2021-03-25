---
description: Enumera os valores válidos que representam os tipos de informações a serem executadas de um objeto IDebugField e são exibidos para o usuário.
title: DisplayKind | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- DisplayKind enumeration
ms.assetid: 940968c5-6065-4bda-8ee6-c31597db4d71
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b8c474c9295ceedbdffd286e99975c375ea69fc4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096025"
---
# <a name="displaykind"></a>DisplayKind
Enumera os valores válidos que representam os tipos de informações a serem executadas de um objeto [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) e são exibidos para o usuário.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_DisplayKind
{
    DisplayKind_Value = 0x1,
    DisplayKind_Name = 0x2,
    DisplayKind_Type = 0x3,
};
typedef DWORD DisplayKind;
```

```csharp
public enum enum_DisplayKind
{
    DisplayKind_Value = 0x1,
    DisplayKind_Name = 0x2,
    DisplayKind_Type = 0x3,
};
```

## <a name="fields"></a>Campos
`DisplayKind_Value`\
Valor do campo.

`DisplayKind_Name`\
Nome do campo.

`DisplayKind_Type`\
Tipo de campo.

## <a name="requirements"></a>Requisitos
Cabeçalho: EE. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetValueDisplayStringCount](../../../extensibility/debugger/reference/ieevisualizerservice-getvaluedisplaystringcount.md)
