---
description: Essa interface representa um programa que está sendo executado em um processo e estende a execução fornecendo informações de thread.
title: IDebugProgram3 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProgram3 interface
ms.assetid: 4301ba23-c00c-4ce5-8b1e-3f27da312034
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 339aff9bdd41a27f48ef1a7ef1e01d9529835403
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084331"
---
# <a name="idebugprogram3"></a>IDebugProgram3
Essa interface representa um programa que está sendo executado em um processo e estende a [execução](../../../extensibility/debugger/reference/idebugprogram2-execute.md) fornecendo informações de thread.

## <a name="syntax"></a>Sintaxe

```
IDebugProgram3 : IDebugProgram3
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O mecanismo de depuração (DE) e um fornecedor de porta personalizado implementam essa interface para representar um programa em um processo. O SDM (Gerenciador de depuração de sessão) também implementa essa interface para fornecer informações a serem [anexadas](../../../extensibility/debugger/reference/idebugprogram2-attach.md).

## <a name="notes-for-callers"></a>Observações para chamadores
 O evento [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md) retorna essa interface para um novo programa. Essa interface também é usada como um parâmetro para muitos métodos em várias interfaces.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugProgram3` .

|Método|Descrição|
|------------|-----------------|
|[ExecuteOnThread](../../../extensibility/debugger/reference/idebugprogram3-executeonthread.md)|Executa o programa. O thread é retornado para fornecer as informações do depurador sobre qual thread o usuário está exibindo durante a execução.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="remarks"></a>Comentários
 Um programa é um contêiner de threads em execução em uma arquitetura de tempo de execução específica, enquanto um processo é composto de um ou mais programas.

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [GetProgram](../../../extensibility/debugger/reference/idebugthread2-getprogram.md)
- [Próximo](../../../extensibility/debugger/reference/ienumdebugprograms2-next.md)
- [Evento](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)
- [Evento](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)
