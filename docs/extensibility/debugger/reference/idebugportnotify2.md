---
description: Essa interface registra ou cancela o registro de um programa que pode ser depurado com a porta em que ele está sendo executado.
title: IDebugPortNotify2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortNotify2
helpviewer_keywords:
- IDebugPortNotify2 interface
ms.assetid: 43278b79-bf16-4c08-bcf1-6f7f7a17feab
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 759be0ff57da7c6bb65ed6ca8191720f835b894a
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102169334"
---
# <a name="idebugportnotify2"></a>IDebugPortNotify2
Essa interface registra ou cancela o registro de um programa que pode ser depurado com a porta em que ele está sendo executado.

## <a name="syntax"></a>Sintaxe

```
IDebugPortNotify2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Um fornecedor de porta personalizado implementa essa interface para dar suporte à adição e remoção de programas da porta. Normalmente, ele é implementado no mesmo objeto que implementa a interface [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) .

## <a name="notes-for-callers"></a>Observações para chamadores
 Uma chamada para [QueryInterface](/cpp/atl/queryinterface) na `IDebugPort2` interface retorna essa interface. Além disso, uma chamada para [GetPortNotify](../../../extensibility/debugger/reference/idebugdefaultport2-getportnotify.md) retorna essa interface. Um mecanismo de depuração pode ver essa interface como um parâmetro para [WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md).

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugPortNotify2` .

|Método|Descrição|
|------------|-----------------|
|[AddProgramNode](../../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)|Registra um programa que pode ser depurado com a porta em que está sendo executado.|
|[RemoveProgramNode](../../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md)|Cancela o registro de um programa que pode ser depurado a partir da porta em que ele está sendo executado.|

## <a name="remarks"></a>Comentários
 A menos que uma porta de depuração tenha uma maneira de saber quando os programas são carregados ou descarregados, um fornecedor de porta personalizado deve implementar essa interface. Todos os programas que são carregados para depuração por meio de uma determinada porta são controlados usando essa interface.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
