---
title: IEnumDebugThreads2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugThreads2
helpviewer_keywords:
- IEnumDebugThreads2
ms.assetid: 1854f078-3b49-42c2-b65b-33e3b506fd63
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6e3771545d4a5fe545382344d17ed5ea929999d1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99852772"
---
# <a name="ienumdebugthreads2"></a>IEnumDebugThreads2
Essa interface enumera os threads em execução na sessão de depuração atual.

## <a name="syntax"></a>Sintaxe

```
IEnumDebugThreads2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O mecanismo de depuração (DE) implementa essa interface para representar uma lista de threads em um programa.

## <a name="notes-for-callers"></a>Observações para chamadores
 Chame [EnumThreads](../../../extensibility/debugger/reference/idebugprocess2-enumthreads.md) para obter essa interface representando uma lista de todos os threads em todos os programas em execução em um processo. Chame [EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md) para obter essa interface representando uma lista de threads em execução em um programa.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IEnumDebugThreads2` .

|Método|Descrição|
|------------|-----------------|
|[Próximo](../../../extensibility/debugger/reference/ienumdebugthreads2-next.md)|Recupera um número especificado de threads na sequência de enumeração.|
|[Skip](../../../extensibility/debugger/reference/ienumdebugthreads2-skip.md)|Ignora um número especificado de threads em uma sequência de enumeração.|
|[Redefinir](../../../extensibility/debugger/reference/ienumdebugthreads2-reset.md)|Redefine uma sequência de enumeração para o início.|
|[8i](../../../extensibility/debugger/reference/ienumdebugthreads2-clone.md)|Cria um enumerador que contém o mesmo estado de enumeração que o atual.|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugthreads2-getcount.md)|Obtém o número de threads em um enumerador.|

## <a name="remarks"></a>Comentários
 O Visual Studio normalmente obtém essa interface para atualizar a janela **threads** , bem como para obter o primeiro thread da lista, a fim de chamar [Execute](../../../extensibility/debugger/reference/idebugprocess3-execute.md), [continue](../../../extensibility/debugger/reference/idebugprocess3-continue.md)e [Step](../../../extensibility/debugger/reference/idebugprocess3-step.md).

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Consulte também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumThreads](../../../extensibility/debugger/reference/idebugprocess2-enumthreads.md)
- [EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)
- [Step](../../../extensibility/debugger/reference/idebugprocess3-step.md)
- [Continuar](../../../extensibility/debugger/reference/idebugprocess3-continue.md)
- [Executar](../../../extensibility/debugger/reference/idebugprocess3-execute.md)
