---
title: 'IDebugProperty3:: GetCustomViewerList | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3::GetCustomViewerList
helpviewer_keywords:
- IDebugProperty3::GetCustomViewerList
ms.assetid: 74490fd8-6f44-4618-beea-dab64961bb8a
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bdabe777bf2147dee2b98ca552183ae0e14d16f1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99888206"
---
# <a name="idebugproperty3getcustomviewerlist"></a>IDebugProperty3::GetCustomViewerList
Obtém uma lista de visualizadores personalizados associados a esta propriedade.

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
no O número de visualizadores para ignorar.

`celtRequested`\
no O número de visualizadores a serem recuperados (também especifica o tamanho da `rgViewers` matriz).

`rgViewers`\
[entrada, saída] Matriz de estruturas de [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md) a serem preenchidas.

`pceltFetched`\
fora O número real de visualizadores retornado.

## <a name="return-value"></a>Valor retornado
Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
Para dar suporte a visualizadores de tipo, esse método encaminha a chamada para o método [GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md) . Se o avaliador de expressão também oferecer suporte a visualizadores personalizados para esse tipo de propriedade, esse método poderá acrescentar os visualizadores personalizados apropriados à lista.

Consulte Visualizador de [tipos e visualizador personalizado](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md) para obter detalhes sobre as diferenças entre visualizadores de tipo e visualizadores personalizados.

## <a name="example"></a>Exemplo
O exemplo a seguir mostra como implementar esse método para um objeto **CProperty** que expõe a interface [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md) .

```cpp
STDMETHODIMP CProperty::GetCustomViewerList(ULONG celtSkip, ULONG celtRequested, DEBUG_CUSTOM_VIEWER* prgViewers, ULONG* pceltFetched)
{
    if (NULL == prgViewers)
    {
        return E_POINTER;
    }

    if (GetVisualizerService())
    {
        return m_pIEEVisualizerService->GetCustomViewerList(celtSkip, celtRequested, prgViewers, pceltFetched);
    }
    else
    {
        return E_NOTIMPL;
    }
}
```

## <a name="see-also"></a>Confira também
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md)
- [GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)
- [Visualizador de tipo e visualizador personalizado](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
