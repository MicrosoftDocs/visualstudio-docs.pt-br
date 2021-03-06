---
description: Essa interface fornece uma interface proxy para exibir e alterar os dados de um objeto.
title: IPropertyProxyProvider | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyProvider
helpviewer_keywords:
- IPropertyProxyProvider interface
ms.assetid: 52e9f7fc-6fe0-4d23-890b-5673dca8c3cb
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3d8d92f6d616d86b82a9f4efa443f459a082256e
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102225533"
---
# <a name="ipropertyproxyprovider"></a>IPropertyProxyProvider
Essa interface fornece uma interface proxy para exibir e alterar os dados de um objeto.

## <a name="syntax"></a>Sintaxe

```
IPropertyProxyProvider : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O avaliador de expressão (EE) implementa essa interface no mesmo objeto que implementa a interface [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md) como parte do suporte do EE dos visualizadores de tipo.

## <a name="notes-for-callers"></a>Observações para chamadores
 Chame [QueryInterface](/cpp/atl/queryinterface) em uma `IDebugProperty3` interface para obter essa interface.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A `IPropertyProxyProvider` interface implementa o seguinte método:

|Método|Descrição|
|------------|-----------------|
|[GetPropertyProxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md)|Recupera uma interface de proxy de propriedade para exibir dados em um objeto.|

## <a name="remarks"></a>Comentários
 Embora o EE Implemente essa interface, a implementação de [GetPropertyProxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md) normalmente é manipulada pelo [GetPropertyProxy](../../../extensibility/debugger/reference/ieevisualizerservice-getpropertyproxy.md). Consulte [visualizando e exibindo dados](../../../extensibility/debugger/visualizing-and-viewing-data.md) para obter detalhes sobre como obter a interface IEEVisualizerService.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetPropertyProxy](../../../extensibility/debugger/reference/ieevisualizerservice-getpropertyproxy.md)
- [Visualizador de tipo e visualizador personalizado](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
- [Visualizando e exibindo dados](../../../extensibility/debugger/visualizing-and-viewing-data.md)
