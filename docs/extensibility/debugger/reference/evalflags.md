---
title: EVALFLAGS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EVALFLAGS
helpviewer_keywords:
- EVALFLAGS enumeration
ms.assetid: 7b2cb14a-511a-4fef-9e4f-308139719fba
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4136726e5c8b798121dbd38975d8f2bb935ed04a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "80737114"
---
# <a name="evalflags"></a>EVALFLAGS
Especifica os sinalizadores que controlam a avaliação da expressão.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_EVALFLAGS {
    EVAL_RETURNVALUE = 0x0002,
    EVAL_NOSIDEEFFECTS = 0x0004,
    EVAL_ALLOWBPS = 0x0008,
    EVAL_ALLOWERRORREPORT = 0x0010,
    EVAL_FUNCTION_AS_ADDRESS = 0x0040,
    EVAL_NOFUNCEVAL = 0x0080,
    EVAL_NOEVENTS = 0x1000
};
typedef DWORD EVALFLAGS;
```

```csharp
public enum enum_EVALFLAGS {
    EVAL_RETURNVALUE = 0x0002,
    EVAL_NOSIDEEFFECTS = 0x0004,
    EVAL_ALLOWBPS = 0x0008,
    EVAL_ALLOWERRORREPORT = 0x0010,
    EVAL_FUNCTION_AS_ADDRESS = 0x0040,
    EVAL_NOFUNCEVAL = 0x0080,
    EVAL_NOEVENTS = 0x1000
}
```

## <a name="fields"></a>Campos
`EVAL_RETURNVALUE`\
Especifica que o valor de retorno, se houver, será avaliado.

`EVAL_NOSIDEEFFECTS`\
Especifica que os efeitos colaterais não são permitidos.

`EVAL_ALLOWBPS`\
Especifica a interrupção nos pontos de interrupção.

`EVAL_ALLOWERRORREPORT`\
Especifica o relatório de erros para o host a ser permitido. Usado principalmente para avaliação de expressão no script no Internet Explorer.

`EVAL_FUNCTION_AS_ADDRESS`\
Força as funções a serem avaliadas como endereços, em vez de invocar a função.

`EVAL_NOFUNCEVAL`\
Impede que a função seja avaliada. Por exemplo, considere o `int` token na expressão `myExpression(int) + 10` . Essa função pode ser avaliada corretamente como um endereço, mas não como um valor.

`EVAL_NOEVENTS`\
Sinalizador para indicar que os eventos que ocorrem durante a avaliação da expressão não devem ser enviados para o SDM (Gerenciador de depuração de sessão) ou para o IDE.

## <a name="remarks"></a>Comentários
Esses sinalizadores são passados como um argumento para os métodos [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) e [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) .

Esses sinalizadores podem ser combinados com um OR bit a bit.

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)
