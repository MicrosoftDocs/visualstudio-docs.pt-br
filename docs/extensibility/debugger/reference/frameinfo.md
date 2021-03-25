---
description: Descreve um quadro de pilha.
title: FRAMEINFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- FRAMEINFO
helpviewer_keywords:
- FRAMEINFO structure
ms.assetid: 95001b89-dddb-45bb-889d-8327994e38a5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0df1689a6d72e972c2bb0f18082041997511843b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059243"
---
# <a name="frameinfo"></a>FRAMEINFO
Descreve um quadro de pilha.

## <a name="syntax"></a>Sintaxe

```cpp
typedef struct tagFRAMEINFO {
    FRAMEINFO_FLAGS    m_dwValidFields;
    BSTR               m_bstrFuncName;
    BSTR               m_bstrReturnType;
    BSTR               m_bstrArgs;
    BSTR               m_bstrLanguage;
    BSTR               m_bstrModule;
    UINT64             m_addrMin;
    UINT64             m_addrMax;
    IDebugStackFrame2* m_pFrame;
    IDebugModule2*     m_pModule;
    BOOL               m_fHasDebugInfo;
    BOOL               m_fStaleCode;
    BOOL               m_fAnnotatedFrame;
} FRAMEINFO;
```

```csharp
public struct FRAMEINFO {
    public uint              m_dwValidFields;
    public string            m_bstrFuncName;
    public string            m_bstrReturnType;
    public string            m_bstrArgs;
    public string            m_bstrLanguage;
    public string            m_bstrModule;
    public ulong             m_addrMin;
    public ulong             m_addrMax;
    public IDebugStackFrame2 m_pFrame;
    public IDebugModule2     m_pModule;
    public int               m_fHasDebugInfo;
    public int               m_fStaleCode;
    public int               m_fAnnotatedFrame;
} FRAMEINFO;
```

## <a name="members"></a>Membros
`m_dwValidFields`\
Uma combinação de sinalizadores da enumeração [FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md) que especifica quais campos são preenchidos.

`m_bstrFuncName`\
O nome da função associada ao registro de ativação.

`m_bstrReturnType`\
O tipo de retorno associado ao registro de ativação.

`m_bstrArgs`\
Os argumentos para a função associada ao registro de ativação.

`m_bstrLanguage`\
O idioma no qual a função é implementada.

`m_bstrModule`\
O nome do módulo associado ao quadro da pilha.

`m_addrMin`\
O endereço de pilha física mínimo.

`m_addrMAX`\
O endereço de pilha física máximo.

`m_pFrame`\
O objeto [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) que representa esse quadro de pilhas.

`m_pModule`\
O objeto [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md) que representa o módulo que contém esse quadro de pilhas.

`m_fHasDebugInfo`\
Diferente de zero ( `TRUE` ) se houver informações de depuração no quadro determinado.

`m_fStaleCode`\
Diferente de zero ( `TRUE` ) se o registro de ativação estiver associado a um código que não é mais válido.

`m_fAnnotatedFrame`\
Diferente de zero ( `TRUE` ) se o registro de ativação for anotado pelo SDM (Gerenciador de depuração de sessão).

## <a name="remarks"></a>Comentários
Essa estrutura é passada para o método [GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md) a ser preenchido. Essa estrutura também está contida em uma lista contida na interface [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md) que, por sua vez, é retornada de uma chamada para o método [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) .

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)
- [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)
- [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)
