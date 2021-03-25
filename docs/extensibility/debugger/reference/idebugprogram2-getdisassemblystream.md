---
description: Obtém o fluxo de desmontagem para este programa ou uma parte deste programa.
title: 'IDebugProgram2:: GetDisassemblyStream | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetDisassemblyStream
helpviewer_keywords:
- IDebugProgram2::GetDisassemblyStream
ms.assetid: beda0da5-267e-4bf3-96c4-b659d29e2254
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c7016c003642b9ef2688390de7cdb39be412bded
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075894"
---
# <a name="idebugprogram2getdisassemblystream"></a>IDebugProgram2::GetDisassemblyStream
Obtém o fluxo de desmontagem para este programa ou uma parte deste programa.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetDisassemblyStream( 
   DISASSEMBLY_STREAM_SCOPE   dwScope,
   IDebugCodeContext2*        pCodeContext,
   IDebugDisassemblyStream2** ppDisassemblyStream
);
```

```csharp
int GetDisassemblyStream( 
   enum_DISASSEMBLY_STREAM_SCOPE  dwScope,
   IDebugCodeContext2             pCodeContext,
   out IDebugDisassemblyStream2   ppDisassemblyStream
);
```

## <a name="parameters"></a>Parâmetros
`dwScope`\
no Especifica um valor da enumeração [DISASSEMBLY_STREAM_SCOPE](../../../extensibility/debugger/reference/disassembly-stream-scope.md) que define o escopo do fluxo de desmontagem.

`pCodeContext`\
no Um objeto [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) que representa a posição de onde iniciar o fluxo de desmontagem.

`ppDisassemblyStream`\
fora Retorna um objeto [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md) que representa o fluxo de desmontagem.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro. Retorna `E_DISASM_NOTSUPPORTED` se a desmontagem não for suportada para esta arquitetura específica.

## <a name="remarks"></a>Comentários
 Se o `dwScopes` parâmetro tiver o `DSS_HUGE` sinalizador do conjunto de enumeração [DISASSEMBLY_STREAM_SCOPE](../../../extensibility/debugger/reference/disassembly-stream-scope.md) , espera-se que a desmontagem retorne um grande número de instruções de desmontagem, por exemplo, para um arquivo ou módulo inteiro. Se o `DSS_HUGE` sinalizador não estiver definido, espera-se que a desmontagem seja confinada em uma região pequena, normalmente a de uma única função.

## <a name="see-also"></a>Confira também
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [DISASSEMBLY_STREAM_SCOPE](../../../extensibility/debugger/reference/disassembly-stream-scope.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)
