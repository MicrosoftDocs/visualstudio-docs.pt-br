---
description: Descreve um erro de exceção ou tempo de execução gerado pelo programa que está sendo depurado.
title: EXCEPTION_INFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EXCEPTION_INFO
helpviewer_keywords:
- EXCEPTION_INFO structure
ms.assetid: d046957a-b97d-420b-b46b-c67cbaef709e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1ec97b56cc7fca8c2185d7180a8d34e87b084b11
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059464"
---
# <a name="exception_info"></a>EXCEPTION_INFO
Descreve um erro de exceção ou tempo de execução gerado pelo programa que está sendo depurado.

## <a name="syntax"></a>Sintaxe

```cpp
typedef struct tagEXCEPTION_INFO {
    IDebugProgram2* pProgram;
    BSTR            bstrProgramName;
    BSTR            bstrExceptionName;
    DWORD           dwCode;
    EXCEPTION_STATE dwState;
    GUID            guidType;
} EXCEPTION_INFO;
```

```csharp
public struct EXCEPTION_INFO {
    public IDebugProgram2 pProgram;
    public string         bstrProgramName;
    public string         bstrExceptionName;
    public uint           dwCode;
    public uint           dwState;
    public Guid           guidType;
};
```

## <a name="members"></a>Membros
`pProgram`\
O objeto [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) que representa o programa no qual a exceção ocorreu.

`bstrProgramName`\
O nome do programa no qual a exceção ocorreu.

`bstrExceptionName`\
O nome da exceção.

`dwCode`\
O código de identificação para a exceção ou erro de tempo de execução.

`dwState`\
Um valor da enumeração [EXCEPTION_STATE](../../../extensibility/debugger/reference/exception-state.md) que define o estado da exceção.

`guidType`\
O identificador de idioma do GUID, `guidLang` ou `guidEng` .

## <a name="remarks"></a>Comentários
Essa estrutura é passada como um parâmetro para os métodos [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md) e [RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md) . Essa estrutura também é passada para o método [GetException](../../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md) que será preenchido.

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [EXCEPTION_STATE](../../../extensibility/debugger/reference/exception-state.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)
- [RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md)
- [GetException](../../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md)
