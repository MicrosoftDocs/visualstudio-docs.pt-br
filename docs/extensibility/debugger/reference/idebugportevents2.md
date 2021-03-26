---
description: Essa interface notifica um ouvinte (normalmente o Gerenciador de depuração de sessão [SDM] ou um mecanismo de depuração) de criação e destruição de processos e programas em uma porta específica.
title: IDebugPortEvents2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEvents2
helpviewer_keywords:
- IDebugPortEvents2 interface
ms.assetid: 2c017094-3ba2-4067-83f9-147df1d96bce
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d8e1ccbb2726fb0f90fae2d31a4b07daad9bae91
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065379"
---
# <a name="idebugportevents2"></a>IDebugPortEvents2
Essa interface notifica um ouvinte (normalmente o Gerenciador de depuração de sessão [SDM] ou um mecanismo de depuração) de criação e destruição de processos e programas em uma porta específica. Essas informações podem ser usadas para apresentar uma exibição em tempo real dos processos e programas em execução na porta.

## <a name="syntax"></a>Sintaxe

```
IDebugPortEvents2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O Visual Studio normalmente implementa essa interface para receber notificações sobre a criação e a destruição de programas. Um mecanismo de depuração também pode implementar essa interface para escutar eventos de porta.

## <a name="notes-for-callers"></a>Observações para chamadores
 Todas as interfaces [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) podem ser consultadas para uma <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer> interface. Em seguida, o <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer.FindConnectionPoint%2A> método para `IDebugPortEvents2` é chamado na <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer> interface para obter uma <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint> interface. Por fim, o <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint.Advise%2A> método na <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint> interface é chamado para enviar os eventos por meio do método de [evento](../../../extensibility/debugger/reference/idebugportevents2-event.md) .

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra o método de `IDebugPortEvents2` .

|Método|Descrição|
|------------|-----------------|
|[Evento](../../../extensibility/debugger/reference/idebugportevents2-event.md)|Envia eventos que descrevem a criação e a destruição de processos e programas na porta.|

## <a name="remarks"></a>Comentários
 `IDebugPortEvents2` também é usado pelo SDM para depurar programas que são executados em um processo que já está sendo depurado.

 Os eventos de porta são passados para o SDM por essa interface.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
