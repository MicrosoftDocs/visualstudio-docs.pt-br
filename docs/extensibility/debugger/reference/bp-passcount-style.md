---
description: Especifica a condição associada à contagem de passagens de ponto de interrupção que faz com que o ponto de interrupção seja acionado.
title: BP_PASSCOUNT_STYLE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_PASSCOUNT_STYLE
helpviewer_keywords:
- BP_PASSCOUNT_STYLE structure
ms.assetid: 0a647047-e2d5-4724-a0b8-68108425ecad
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 39a0dba08aa74386c442a7732b6522d8ee27652c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094465"
---
# <a name="bp_passcount_style"></a>BP_PASSCOUNT_STYLE
Especifica a condição associada à contagem de passagens de ponto de interrupção que faz com que o ponto de interrupção seja acionado.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_BP_PASSCOUNT_STYLE {
    BP_PASSCOUNT_NONE             = 0x0000,
    BP_PASSCOUNT_EQUAL            = 0x0001,
    BP_PASSCOUNT_EQUAL_OR_GREATER = 0x0002,
    BP_PASSCOUNT_MOD              = 0x0003
};
typedef DWORD BP_PASSCOUNT_STYLE;
```

```csharp
public enum enum_BP_PASSCOUNT_STYLE {
    BP_PASSCOUNT_NONE             = 0x0000,
    BP_PASSCOUNT_EQUAL            = 0x0001,
    BP_PASSCOUNT_EQUAL_OR_GREATER = 0x0002,
    BP_PASSCOUNT_MOD              = 0x0003
};
```

## <a name="fields"></a>Campos
`BP_PASSCOUNT_NONE`\
Especifica nenhum estilo de contagem de passe de ponto de interrupção.

`BP_PASSCOUNT_EQUAL`\
Define o estilo de contagem de passagens de ponto de interrupção como igual. O ponto de interrupção é acionado quando o número de vezes que o ponto de interrupção é atingido é igual à contagem de aprovações.

`BP_PASSCOUNT_EQUAL_OR_GREATER`\
Define o estilo de contagem de passagens de ponto de interrupção como igual ou maior. O ponto de interrupção é acionado quando o número de vezes que o ponto de interrupção é atingido é igual ou maior que a contagem de aprovações.

`BP_PASSCOUNT_MOD`\
Especifica uma contagem de passagens de módulo. Por exemplo, se a contagem Pass for do tipo `BP_PASSCOUNT_MOD` e o valor da contagem Pass for 4, o ponto de interrupção será acionado sempre que a contagem de vezes for um múltiplo de 4.

## <a name="remarks"></a>Comentários
Usado para o `stylePassCount` membro da estrutura de [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md) que, por sua vez, é um membro das estruturas [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) e [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) .

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
