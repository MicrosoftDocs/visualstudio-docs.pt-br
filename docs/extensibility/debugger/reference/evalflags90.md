---
description: Enumera os valores válidos para sinalizadores que controlam a avaliação da expressão.
title: EVALFLAGS90 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- EVALFLAGS90 enumeration
ms.assetid: 64fb0139-8b04-4726-b52c-db2e04d65498
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 32e75b938f45df5d4fa91bec4b59964dfc6a54e5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105095921"
---
# <a name="evalflags90"></a>EVALFLAGS90
Enumera os valores válidos para sinalizadores que controlam a avaliação da expressão. Essa enumeração estende a enumeração [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md) .

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_EVALFLAGS90
{
    // VS 8.0 values
    EVAL90_RETURNVALUE                 = 0x0002,
    EVAL90_NOSIDEEFFECTS               = 0x0004,
    EVAL90_ALLOWBPS                    = 0x0008,
    EVAL90_ALLOWERRORREPORT            = 0x0010,
    EVAL90_FUNCTION_AS_ADDRESS         = 0x0040,
    EVAL90_NOFUNCEVAL                  = 0x0080,
    EVAL90_NOEVENTS                    = 0x1000,
    EVAL90_DESIGN_TIME_EXPR_EVAL       = 0x2000,
    EVAL90_ALLOW_IMPLICIT_VARS         = 0x4000,

    // Values added in VS 9.0
    EVAL90_FORCE_EVALUATION_NOW        = 0x8000
};
typedef DWORD EVALFLAGS90;
```

```csharp
public enum enum_EVALFLAGS90
{
    // VS 8.0 values
    EVAL90_RETURNVALUE                 = 0x0002,
    EVAL90_NOSIDEEFFECTS               = 0x0004,
    EVAL90_ALLOWBPS                    = 0x0008,
    EVAL90_ALLOWERRORREPORT            = 0x0010,
    EVAL90_FUNCTION_AS_ADDRESS         = 0x0040,
    EVAL90_NOFUNCEVAL                  = 0x0080,
    EVAL90_NOEVENTS                    = 0x1000,
    EVAL90_DESIGN_TIME_EXPR_EVAL       = 0x2000,
    EVAL90_ALLOW_IMPLICIT_VARS         = 0x4000,

    // Values added in VS 9.0
    EVAL90_FORCE_EVALUATION_NOW        = 0x8000
};
```

## <a name="fields"></a>Campos
`EVAL90_RETURNVALUE`\
Especifica que o valor de retorno, se houver, será avaliado.

`EVAL90_NOSIDEEFFECTS`\
Especifica que os efeitos colaterais não são permitidos.

`EVAL90_ALLOWBPS`\
Especifica a interrupção nos pontos de interrupção.

`EVAL90_ALLOWERRORREPORT`\
Especifica o relatório de erros para o host a ser permitido. Usado principalmente para avaliação de expressão no script no Internet Explorer.

`EVAL90_FUNCTION_AS_ADDRESS`\
Força as funções a serem avaliadas como endereços, em vez de invocar a função.

`EVAL90_NOFUNCEVAL`\
Impede que a função seja avaliada. Por exemplo, considere o `int` token na expressão `myExpression(int) + 10` . Essa função pode ser avaliada corretamente como um endereço, mas não como um valor.

`EVAL90_NOEVENTS`\
Sinalizador para indicar que os eventos que ocorrem durante a avaliação da expressão não devem ser enviados para o SDM (Gerenciador de depuração de sessão) ou para o IDE.

`EVAL90_DESIGN_TIME_EXPR_EVAL`\
Habilita a avaliação de expressão em tempo de design.

`EVAL90_ALLOW_IMPLICIT_VARS`\
Permite a criação de variável implícita.

`EVAL90_FORCE_EVALUATION_NOW`\
Força a avaliação a ocorrer imediatamente. Isso é útil ao atender a uma solicitação, como uma solicitação de usuário.

## <a name="requirements"></a>Requisitos
Cabeçalho: Msdbg90. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
