---
description: Permite que um nó de programa seja notificado sobre uma tentativa de anexar ao programa associado.
title: IDebugProgramNodeAttach2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNodeAttach2
helpviewer_keywords:
- IDebugProgramNodeAttach2 interface
ms.assetid: 46b37ac9-a026-4ad3-997b-f19e2f8deb73
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1a1de6c7480e1ce4dcc0723614741a05dcc961a6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071461"
---
# <a name="idebugprogramnodeattach2"></a>IDebugProgramNodeAttach2
Permite que um nó de programa seja notificado sobre uma tentativa de anexar ao programa associado.

## <a name="syntax"></a>Sintaxe

```
IDebugProgramNodeAttach2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Essa interface é implementada na mesma classe que implementa a interface [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) para receber a notificação de uma operação de anexação e fornecer uma oportunidade para cancelar a operação de anexação.

## <a name="notes-for-callers"></a>Observações para chamadores
 Obtenha essa interface chamando o `QueryInterface` método em um objeto [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) . O método [onattach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) deve ser chamado antes do método [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) para dar ao nó do programa uma chance de interromper o processo de anexação.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 Essa interface implementa o seguinte método:

|Método|Descrição|
|------------|-----------------|
|[OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)|Anexa ao programa associado ou adia o processo de anexação para o método [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) .|

## <a name="remarks"></a>Comentários
 Essa interface é a alternativa preferida para o método de [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md) preterido. Todos os mecanismos de depuração sempre são carregados com a `CoCreateInstance` função, ou seja, eles são instanciados fora do espaço de endereço do programa que está sendo depurado.

 Se uma implementação anterior do `IDebugProgramNode2::Attach_V7` método fosse simplesmente definir o `GUID` do programa que está sendo depurado, somente o método [onattach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) precisará ser implementado.

 Se uma implementação anterior do `IDebugProgramNode2::Attach_V7` método usou a interface de retorno de chamada fornecida, essa funcionalidade precisará ser movida para uma implementação do método [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) e a `IDebugProgramNodeAttach2` interface não precisará ser implementada.

## <a name="requirements"></a>Requisitos
 Cabeçalho: Msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)
