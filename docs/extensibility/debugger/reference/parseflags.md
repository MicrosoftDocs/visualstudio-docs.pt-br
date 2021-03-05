---
description: Especifica como analisar uma expressão.
title: PARSEFLAGS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PARSEFLAGS
helpviewer_keywords:
- PARSEFLAGS enumeration
ms.assetid: 47943f0a-54cb-4493-a62e-5dba97bd4c35
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 192e4de399540ce189bbf52cbb0f615b2b9bc855
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102222140"
---
# <a name="parseflags"></a>PARSEFLAGS
Especifica como analisar uma expressão.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_PARSEFLAGS { 
   PARSE_EXPRESSION            = 0x0001,
   PARSE_FUNCTION_AS_ADDRESS   = 0x0002,
   PARSE_DESIGN_TIME_EXPR_EVAL = 0x1000
};
typedef DWORD PARSEFLAGS;
```

```csharp
public enum enum_PARSEFLAGS { 
   PARSE_EXPRESSION            = 0x0001,
   PARSE_FUNCTION_AS_ADDRESS   = 0x0002,
   PARSE_DESIGN_TIME_EXPR_EVAL = 0x1000
};
```

## <a name="fields"></a>Campos
 `PARSE_EXPRESSION`\
 Indica que a expressão não é uma instrução.

 `PARSE_FUNCTION_AS_ADDRESS`\
 Indica que a expressão deve ser analisada (e posteriormente avaliada) como um endereço.

 `PARSE_DESIGN_TIME_EXPR_EVAL`\
 Indica que a expressão está sendo analisada durante o tempo de design (ou seja, quando um designer está aberto).

## <a name="remarks"></a>Comentários
 Passado como um parâmetro para os métodos [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) e [Parse](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) .

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)
- [Analisar](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)
