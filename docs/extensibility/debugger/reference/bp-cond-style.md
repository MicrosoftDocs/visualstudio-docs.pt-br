---
title: BP_COND_STYLE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_COND_STYLE
helpviewer_keywords:
- BP_COND_STYLE enumeration
ms.assetid: a93b1412-f447-48a1-af9d-38f3dbb3092f
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 70ab3655d27e810b3c05d0e0e81d81bc15a26950
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/22/2019
ms.locfileid: "56685853"
---
# <a name="bpcondstyle"></a>BP_COND_STYLE
Especifica o estilo de condição de ponto de interrupção para pendentes e associados a pontos de interrupção.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_BP_COND_STYLE {
    BP_COND_NONE         = 0x0000,
    BP_COND_WHEN_TRUE    = 0x0001,
    BP_COND_WHEN_CHANGED = 0x0002
};
typedef DWORD BP_COND_STYLE;
```

```csharp
public enum enum_BP_COND_STYLE {
    BP_COND_NONE         = 0x0000,
    BP_COND_WHEN_TRUE    = 0x0001,
    BP_COND_WHEN_CHANGED = 0x0002
};
```

## <a name="members"></a>Membros
BP_COND_NONE dispara o ponto de interrupção quando a posição do ponto de interrupção é atingida. Nenhuma condição de ponto de interrupção especificada.

BP_COND_WHEN_TRUE dispara o ponto de interrupção somente quando a expressão condicional é associado com o ponto de interrupção é avaliada como `true`.

BP_COND_WHEN_CHANGED dispara o ponto de interrupção somente quando o valor da expressão condicional associado com o ponto de interrupção foi alterado de sua avaliação anterior.

## <a name="remarks"></a>Comentários
Usado para o `styleCondition` membro a [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md) estrutura.

## <a name="requirements"></a>Requisitos
Header: msdbg.h

Namespace: Microsoft.VisualStudio.Debugger.Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Consulte também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)
