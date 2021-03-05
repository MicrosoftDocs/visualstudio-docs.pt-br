---
description: Essa interface fornece vários métodos para acessar os recursos de notificação e servidor de uma porta.
title: IDebugDefaultPort2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDefaultPort2
helpviewer_keywords:
- IDebugDefaultPort2 interface
ms.assetid: 7b3452af-9a96-4c4c-9946-4339b72d3d7b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a5ec637daa197574710978af7cb22195c969f48b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102154412"
---
# <a name="idebugdefaultport2"></a>IDebugDefaultPort2
Essa interface fornece vários métodos para acessar os recursos de notificação e servidor de uma porta.

## <a name="syntax"></a>Sintaxe

```
IDebugDefaultPort2 : IDebugPort2
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O Visual Studio implementa essa interface para representar a porta de depuração para acessar programas. Um fornecedor de porta personalizado também pode implementar essa interface se tratar da depuração remota.

## <a name="notes-for-callers"></a>Observações para chamadores
 Um argumento para métodos na interface [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md) fornece essa interface. Chamar [QueryInterface](/cpp/atl/queryinterface) em uma interface [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) também pode obter essa interface.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 Além dos métodos definidos no [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md), essa interface implementa os seguintes métodos:

|Método|Descrição|
|------------|-----------------|
|[GetPortNotify](../../../extensibility/debugger/reference/idebugdefaultport2-getportnotify.md)|Obtém a interface de notificação de porta desta porta.|
|[GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)|Obtém a interface para o servidor que hospeda essa porta.|
|[QueryIsLocal](../../../extensibility/debugger/reference/idebugdefaultport2-queryislocal.md)|Determina se esta porta está em execução no computador local.|

## <a name="remarks"></a>Comentários
 O nome " `IDebugDefaultPort2` " é um pouco de um nome, pois não representa uma porta padrão. Ele poderia ser chamado de "IDebugPort3".

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)
