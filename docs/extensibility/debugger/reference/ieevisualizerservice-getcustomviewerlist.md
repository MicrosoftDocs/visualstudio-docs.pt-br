---
title: 'IEEVisualizerService:: GetCustomViewerList | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerService::GetCustomViewerList
helpviewer_keywords:
- IEEVisualizerService::GetCustomViewerList method
ms.assetid: 249d26ca-914f-43af-a400-8162477223f4
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2ba63a1f27e043ca114a3b954adfe403b60283ca
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99907805"
---
# <a name="ieevisualizerservicegetcustomviewerlist"></a>IEEVisualizerService::GetCustomViewerList
Esse método retorna uma lista de visualizadores de tipo que esse serviço conhece.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetCustomViewerList(
   ULONG                celtSkip,
   ULONG                celtRequested,
   DEBUG_CUSTOM_VIEWER* rgViewers,
   ULONG*               pceltFetched
);
```

```csharp
int GetCustomViewerList(
   uint                  celtSkip,
   uint                  celtRequested,
   DEBUG_CUSTOM_VIEWER[] rgViewers,
   out uint              pceltFetched
);
```

## <a name="parameters"></a>Parâmetros
`celtSkip`\
no Número de visualizadores para ignorar.

`celRequested`\
no Número de visualizadores a serem recuperados (também especifica o tamanho da `rgViewers` matriz).

`rgViewers`\
[entrada, saída] Matriz de estruturas de [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md) a serem preenchidas.

`pceltFetched`\
fora Número de visualizadores recuperados na verdade.

## <a name="return-value"></a>Valor retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
- [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) passa a solicitação para esse método como parte de seu suporte para visualizadores de tipo. Se o avaliador de expressão também fornecer visualizadores personalizados para o mesmo tipo, ele poderá acrescentar estruturas de [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md) preenchidas adequadamente para esses visualizadores personalizados à lista. Certifique-se de que [GetCustomViewerCount](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md) reflete esses visualizadores adicionais.

 Consulte Visualizador de [tipos e visualizador personalizado](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md) para obter detalhes sobre as diferenças entre visualizadores e visualizadores.

## <a name="see-also"></a>Confira também
- [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)
- [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md)
- [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)
- [GetCustomViewerCount](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)
- [Visualizador de tipo e visualizador personalizado](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
