---
description: Obtém o contexto do documento para este quadro de pilhas.
title: 'IDebugStackFrame2:: GetDocumentContext | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::GetDocumentContext
helpviewer_keywords:
- IDebugStackFrame2::GetDocumentContext
ms.assetid: 69e81439-1238-4f18-9028-6fd1c1ba5e4a
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9e1645cb7daebb9dc344085d13a2fecb87fc0106
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102145970"
---
# <a name="idebugstackframe2getdocumentcontext"></a>IDebugStackFrame2::GetDocumentContext
Obtém o contexto do documento para este quadro de pilhas.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetDocumentContext ( 
   IDebugDocumentContext2** ppCxt
);
```

```csharp
int GetDocumentContext ( 
   out IDebugDocumentContext2 ppCxt
);
```

## <a name="parameters"></a>Parâmetros
`ppCxt`\
fora Retorna um objeto [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) que representa a posição atual em um documento de origem.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Esse método é mais rápido do que chamar o método [GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md) e, em seguida, chamar o método [GetDocumentContext](../../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md) no contexto do código. No entanto, não há garantia de que cada mecanismo DE depuração (DE) implementará esse método.

## <a name="see-also"></a>Confira também
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [GetDocumentContext](../../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md)
- [GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)
