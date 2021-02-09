---
title: IDebugQueryEngine2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugQueryEngine2
helpviewer_keywords:
- IDebugQueryEngine2 interface
ms.assetid: 8f0e1838-a818-4459-9138-a3dceb7408de
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b555ac218ceee1d376c9f7cf3c9df87f7c2e2da0
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99909776"
---
# <a name="idebugqueryengine2"></a>IDebugQueryEngine2
Essa interface permite que o SDM (Gerenciador de depuração de sessão) recupere uma interface que representa o mecanismo DE depuração (DE).

## <a name="syntax"></a>Sintaxe

```
IDebugQueryEngine2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O DE implementa essa interface nos objetos que implementam as interfaces mais comuns (como [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md), [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)e [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)) para permitir o acesso à interface [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) da própria.

## <a name="notes-for-callers"></a>Observações para chamadores
 Chame [QueryInterface](/cpp/atl/queryinterface) em uma interface típica para obter essa interface.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugQueryEngine2` .

|Método|Descrição|
|------------|-----------------|
|[GetEngineInterface](../../../extensibility/debugger/reference/idebugqueryengine2-getengineinterface.md)|Obtém uma interface do mecanismo DE depuração personalizado (DE).|

## <a name="remarks"></a>Comentários
 Normalmente, essa interface é implementada no objeto que implementa a interface [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) para dar suporte à passagem causalidade por meio de funções; ou seja, quando o depurador está saindo de uma função, a função Next a ser executada pode não ser a função anterior na pilha, mas uma função em outro thread. Para obter uma definição de "causalidade", consulte o [Glossário do depurador do Visual Studio](../../../extensibility/debugger/reference/visual-studio-debugger-glossary.md).

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
