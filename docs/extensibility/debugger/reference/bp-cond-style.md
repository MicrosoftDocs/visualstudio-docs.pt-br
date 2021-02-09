---
title: BP_COND_STYLE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_COND_STYLE
helpviewer_keywords:
- BP_COND_STYLE enumeration
ms.assetid: a93b1412-f447-48a1-af9d-38f3dbb3092f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4f98f02e7e756a744d8042a9955802165065d54d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99862156"
---
# <a name="bp_cond_style"></a>BP_COND_STYLE
Especifica o estilo de condição do ponto de interrupção para pontos de interrupção pendentes e associados.

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

## <a name="fields"></a>Campos
`BP_COND_NONE`\
Dispara o ponto de interrupção quando a posição do ponto de interrupção é atingida. Nenhuma condição de ponto de interrupção especificada.

`BP_COND_WHEN_TRUE`\
Dispara o ponto de interrupção somente quando a expressão condicional associada ao ponto de interrupção é avaliada como `true` .

`BP_COND_WHEN_CHANGED`\
Dispara o ponto de interrupção somente quando o valor da expressão condicional associada ao ponto de interrupção foi alterado de sua avaliação anterior.

## <a name="remarks"></a>Comentários
Usado para o `styleCondition` membro da estrutura de [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md) .

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)
