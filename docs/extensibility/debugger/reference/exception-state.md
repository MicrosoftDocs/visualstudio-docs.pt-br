---
description: Especifica o estado da exceção.
title: EXCEPTION_STATE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EXCEPTION_STATE
helpviewer_keywords:
- EXCEPTION_STATE enumeration
ms.assetid: 597f4f4c-9b70-485c-b5dc-3c2e3aecc664
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 297c5de3afd2b5f81444dd29278fc294cd71aa6a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059438"
---
# <a name="exception_state"></a>EXCEPTION_STATE
Especifica o estado da exceção.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_EXCEPTION_STATE {
    EXCEPTION_NONE                          = 0x0000,
    EXCEPTION_STOP_FIRST_CHANCE             = 0x0001,
    EXCEPTION_STOP_SECOND_CHANCE            = 0x0002,
    EXCEPTION_STOP_USER_FIRST_CHANCE        = 0x0010,
    EXCEPTION_STOP_USER_UNCAUGHT            = 0x0020,
    EXCEPTION_STOP_ALL                      = 0x00FF,
    EXCEPTION_CANNOT_BE_CONTINUED           = 0x0100,

    // These are for exception types only
    EXCEPTION_CODE_SUPPORTED                = 0x1000,
    EXCEPTION_CODE_DISPLAY_IN_HEX           = 0x2000,
    EXCEPTION_JUST_MY_CODE_SUPPORTED        = 0x4000,
    EXCEPTION_MANAGED_DEBUG_ASSISTANT       = 0x8000,

    // These are no longer used
    EXCEPTION_STOP_FIRST_CHANCE_USE_PARENT      = 0x0004,
    EXCEPTION_STOP_SECOND_CHANCE_USE_PARENT     = 0x0008,
    EXCEPTION_STOP_USER_FIRST_CHANCE_USE_PARENT = 0x0040,
    EXCEPTION_STOP_USER_UNCAUGHT_USE_PARENT     = 0x0080,
};
typedef DWORD EXCEPTION_STATE;
```

```csharp
public enum enum_EXCEPTION_STATE {
    EXCEPTION_NONE                          = 0x0000,
    EXCEPTION_STOP_FIRST_CHANCE             = 0x0001,
    EXCEPTION_STOP_SECOND_CHANCE            = 0x0002,
    EXCEPTION_STOP_USER_FIRST_CHANCE        = 0x0010,
    EXCEPTION_STOP_USER_UNCAUGHT            = 0x0020,
    EXCEPTION_STOP_ALL                      = 0x00FF,
    EXCEPTION_CANNOT_BE_CONTINUED           = 0x0100,

    // These are for exception types only
    EXCEPTION_CODE_SUPPORTED                = 0x1000,
    EXCEPTION_CODE_DISPLAY_IN_HEX           = 0x2000,
    EXCEPTION_JUST_MY_CODE_SUPPORTED        = 0x4000,
    EXCEPTION_MANAGED_DEBUG_ASSISTANT       = 0x8000,

    // These are no longer used
    EXCEPTION_STOP_FIRST_CHANCE_USE_PARENT      = 0x0004,
    EXCEPTION_STOP_SECOND_CHANCE_USE_PARENT     = 0x0008,
    EXCEPTION_STOP_USER_FIRST_CHANCE_USE_PARENT = 0x0040,
    EXCEPTION_STOP_USER_UNCAUGHT_USE_PARENT     = 0x0080,
};
```

## <a name="fields"></a>Campos
`EXCEPTION_NONE`\
Não pare na exceção.

`EXCEPTION_STOP_FIRST_CHANCE`\
Pare no primeiro acionamento da exceção. Ao descrever um evento de exceção, esse sinalizador indica que o evento de exceção é um evento de exceção de primeira chance.

`EXCEPTION_STOP_SECOND_CHANCE`\
Parar no segundo acionamento de exceção. Ao descrever um evento de exceção, indica que o evento de exceção é um evento de exceção de segunda chance.

`EXCEPTION_STOP_USER_FIRST_CHANCE`\
Pare no primeiro acionamento de uma exceção de modo de usuário. Ao descrever um evento de exceção, indica que o evento de exceção é um evento de exceção de usuário de primeira chance.

`EXCEPTION_STOP_USER_UNCAUGHT`\
Parar quando uma exceção de modo de usuário não for detectada. Ao descrever um evento de exceção, indica que o evento de exceção é um evento de exceção de modo de usuário não percebido.

`EXCEPTION_STOP_ALL`\
Pare em qualquer exceção. Não usado ao descrever um evento de exceção.

`EXCEPTION_CANNOT_BE_CONTINUED`\
Ao descrever um evento de exceção, indica que a exceção não pode continuar.

`EXCEPTION_CODE_SUPPORTED`\
Indica que a exceção tem código que o suporta. Usado na exibição de uma exceção

`EXCEPTION_CODE_DISPLAY_IN_HEX`\
Indica que o código de exceção deve ser exibido em hexadecimal. Usado na exibição de uma exceção.

`EXCEPTION_JUST_MY_CODE_SUPPORTED`\
Indica que o código de exceção dá suporte a JustMyCode. Usado na exibição de uma exceção.

`EXCEPTION_MANAGED_DEBUG_ASSISTANT`\
Indica que o depurador de código gerenciado deve tratar exceções. Se não estiver definido, o depurador padrão tratará as exceções. Isso é passado para o método [SetAllExceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md) e não é usado na estrutura [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md) .

`EXCEPTION_STOP_FIRST_CHANCE_USE_PARENT`\
OBSOLETO, NÃO USE.

`EXCEPTION_STOP_SECOND_CHANCE_USE_PARENT`\
OBSOLETO, NÃO USE.

`EXCEPTION_STOP_USER_FIRST_CHANCE_USE_PARENT`\
OBSOLETO, NÃO USE.

`EXCEPTION_STOP_USER_SECOND_CHANCE_USE_PARENT`\
OBSOLETO, NÃO USE.

## <a name="remarks"></a>Comentários
Usado como o `dwState` membro da estrutura de [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md) para indicar o estado da exceção e o que pode ser feito sobre ela.

Esses valores também são passados para o método [SetAllExceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md) para definir o estado de todas as exceções.

Esses sinalizadores podem ser combinados com um OR bit a bit.

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)
- [SetAllExceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md)
