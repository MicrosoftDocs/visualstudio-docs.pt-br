---
description: Especifica as informações a serem recuperadas sobre um objeto de quadro de pilha.
title: FRAMEINFO_FLAGS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- FRAMEINFO_FLAGS
helpviewer_keywords:
- FRAMEINFO_FLAGS enumeration
ms.assetid: 41578062-8455-412a-9d8b-1e1e9dc8d52e
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4029212aae6d4557e17c42a0c0e024a83c94b0a1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102150816"
---
# <a name="frameinfo_flags"></a>FRAMEINFO_FLAGS
Especifica as informações a serem recuperadas sobre um objeto de quadro de pilha.

## <a name="syntax"></a>Sintaxe

```cpp
enum enum_FRAMEINFO_FLAGS {
    FIF_FUNCNAME              = 0x00000001,
    FIF_RETURNTYPE            = 0x00000002,
    FIF_ARGS                  = 0x00000004,
    FIF_LANGUAGE              = 0x00000008,
    FIF_MODULE                = 0x00000010,
    FIF_STACKRANGE            = 0x00000020,
    FIF_FRAME                 = 0x00000040,
    FIF_DEBUGINFO             = 0x00000080,
    FIF_STALECODE             = 0x00000100,
    FIF_ANNOTATEDFRAME        = 0x00000200,
    FIF_DEBUG_MODULEP         = 0x00000400,
    FIF_FUNCNAME_FORMAT       = 0x00001000,
    FIF_FUNCNAME_RETURNTYPE   = 0x00002000,
    FIF_FUNCNAME_ARGS         = 0x00004000,
    FIF_FUNCNAME_LANGUAGE     = 0x00008000,
    FIF_FUNCNAME_MODULE       = 0x00010000,
    FIF_FUNCNAME_LINES        = 0x00020000,
    FIF_FUNCNAME_OFFSET       = 0x00040000,
    FIF_FUNCNAME_ARGS_TYPES   = 0x00100000,
    FIF_FUNCNAME_ARGS_NAMES   = 0x00200000,
    FIF_FUNCNAME_ARGS_VALUES  = 0x00400000,
    FIF_FUNCNAME_ARGS_ALL     = 0x00700000,
    FIF_ARGS_TYPES            = 0x01000000,
    FIF_ARGS_NAMES            = 0x02000000,
    FIF_ARGS_VALUES           = 0x04000000,
    FIF_ARGS_ALL              = 0x07000000,
    FIF_ARGS_NOFORMAT         = 0x08000000,
    FIF_ARGS_NO_FUNC_EVAL     = 0x10000000,
    FIF_FILTER_NON_USER_CODE  = 0x20000000,
    FIF_ARGS_NO_TOSTRING      = 0x40000000,
    FIF_DESIGN_TIME_EXPR_EVAL = 0x80000000
};
typedef DWORD FRAMEINFO_FLAGS;
```

```csharp
public enum enum_FRAMEINFO_FLAGS {
    FIF_FUNCNAME              = 0x00000001,
    FIF_RETURNTYPE            = 0x00000002,
    FIF_ARGS                  = 0x00000004,
    FIF_LANGUAGE              = 0x00000008,
    FIF_MODULE                = 0x00000010,
    FIF_STACKRANGE            = 0x00000020,
    FIF_FRAME                 = 0x00000040,
    FIF_DEBUGINFO             = 0x00000080,
    FIF_STALECODE             = 0x00000100,
    FIF_ANNOTATEDFRAME        = 0x00000200,
    FIF_DEBUG_MODULEP         = 0x00000400,
    FIF_FUNCNAME_FORMAT       = 0x00001000,
    FIF_FUNCNAME_RETURNTYPE   = 0x00002000,
    FIF_FUNCNAME_ARGS         = 0x00004000,
    FIF_FUNCNAME_LANGUAGE     = 0x00008000,
    FIF_FUNCNAME_MODULE       = 0x00010000,
    FIF_FUNCNAME_LINES        = 0x00020000,
    FIF_FUNCNAME_OFFSET       = 0x00040000,
    FIF_FUNCNAME_ARGS_TYPES   = 0x00100000,
    FIF_FUNCNAME_ARGS_NAMES   = 0x00200000,
    FIF_FUNCNAME_ARGS_VALUES  = 0x00400000,
    FIF_FUNCNAME_ARGS_ALL     = 0x00700000,
    FIF_ARGS_TYPES            = 0x01000000,
    FIF_ARGS_NAMES            = 0x02000000,
    FIF_ARGS_VALUES           = 0x04000000,
    FIF_ARGS_ALL              = 0x07000000,
    FIF_ARGS_NOFORMAT         = 0x08000000,
    FIF_ARGS_NO_FUNC_EVAL     = 0x10000000,
    FIF_FILTER_NON_USER_CODE  = 0x20000000,
    FIF_ARGS_NO_TOSTRING      = 0x40000000,
    FIF_DESIGN_TIME_EXPR_EVAL = 0x80000000
};
```

## <a name="fields"></a>Campos
`FIF_FUNCNAME`\
Inicializar/usar o `m_bstrFuncName` campo.

`FIF_RETURNTYPE`\
Inicializar/usar o `m_bstrReturnType` campo.

`FIF_ARGS`\
Inicializar/usar o `m_bstrArgs` campo.

`FIF_LANGUAGE`\
Inicializar/usar o `m_bstrLanguage` campo.

`FIF_MODULE`\
Inicializar/usar o `m_bstrModule` campo.

`FIF_STACKRANGE`\
Inicializar/usar os `m_addrMin` `m_addrMax` campos e (intervalo de pilha).

`FIF_FRAME`\
Inicializar/usar o `m_pFrame` campo.

`FIF_DEBUGINFO`\
Inicializar/usar o `m_fHasDebugInfo` campo.

`FIF_STALECODE`\
Inicializar/usar o `m_fStaleCode` campo.

`FIF_ANNOTATEDFRAME`\
Inicializar/usar o `m_fAnnotatedFrame` campo.

`FIF_DEBUG_MODULEP`\
Inicializar/usar o `m_pModule` campo.

`FIF_FUNCNAME_FORMAT`\
Formata o nome da função. O resultado é retornado no `m_bstrFunName` campo e nenhum outro campo é preenchido.

`FIF_FUNCNAME_RETURNTYPE`\
Adiciona o tipo de retorno ao `m_bstrFuncName` campo.

`FIF_FUNCNAME_ARGS`\
Adiciona os argumentos ao `m_bstrFuncName` campo.

`FIF_FUNCNAME_LANGUAGE`\
Adiciona o idioma ao `m_bstrFuncName` campo.

`FIF_FUNCNAME_MODULE`\
Adiciona o nome do módulo ao `m_bstrFuncName` campo.

`FIF_FUNCNAME_LINES`\
Adiciona o número de linhas ao `m_bstrFuncName` campo.

`FIF_FUNCNAME_OFFSET`\
Adiciona ao `m_bstrFuncName` campo o deslocamento em bytes do início da linha, se `FIF_FUNCNAME_LINES` for especificado. Se `FIF_FUNCNAME_LINES` não for especificado, ou se os números de linha não estiverem disponíveis, o adicionará o deslocamento em bytes do início da função.

`FIF_FUNCNAME_ARGS_TYPES`\
Adiciona o tipo de cada argumento de função ao `m_bstrFuncName` campo.

`FIF_FUNCNAME_ARGS_NAMES`\
Adiciona o nome de cada argumento de função ao `m_bstrFuncName` campo.

`FIF_FUNCNAME_ARGS_VALUES`\
Adiciona o valor de cada argumento de função ao `m_bstrFuncName` campo.

`FIF_FUNCNAME_ARGS_ALL`\
Adiciona o tipo, o nome e o valor de todos os argumentos ao `m_bstrFuncName` campo.

`FIF_ARGS_TYPES`\
Os tipos de argumento são recuperados e formatados.

`FIF_ARGS_NAMES`\
Os nomes dos argumentos são recuperados e formatados.

`FIF_ARGS_VALUES`\
Os valores de argumento são recuperados e formatados.

`FIF_ARGS_ALL`\
Recupere e formate o tipo, o nome e o valor de todos os argumentos.

`FIF_ARGS_NOFORMAT`\
Especifica que os argumentos não são formatados (por exemplo, não adicione parênteses de abertura e fechamento ao contrário da lista de argumentos nem adicione um separador entre argumentos).

`FIF_ARGS_NO_FUNC_EVAL`\
Especifica que a avaliação da função (Propriedade) não deve ser usada ao recuperar valores de argumento.

`FIF_FILTER_NON_USER_CODE`\
O mecanismo de depuração é filtrar os quadros de código que não são de usuário para que não sejam incluídos.

`FIF_ARGS_NO_TOSTRING`\
Não permita a `ToString()` avaliação ou a formatação da função ao retornar argumentos de função.

`FIF_DESIGN_TIME_EXPR_EVAL`\
As informações do quadro devem ser provenientes do domínio do aplicativo hospedado em vez do processo de hospedagem.

## <a name="remarks"></a>Comentários
Esses sinalizadores são passados para os métodos [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) e [GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md) para indicar quais campos devem ser inicializados na estrutura ou nas estruturas do [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) .

Esses sinalizadores também são usados para indicar quais campos da estrutura [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) são usados e válidos quando a estrutura é retornada. Esses valores podem ser combinados com um bit a bit `OR` .

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)
- [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)
