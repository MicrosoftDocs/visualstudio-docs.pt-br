---
description: Esse método retorna um serviço solicitado.
title: 'IDebugBinder3:: GetEEService | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3::GetEEService
helpviewer_keywords:
- IDebugBinder3::GetEEService method
ms.assetid: eb07aa40-8cd9-4a52-a4c7-4affd2307a01
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5ecd439ba1af40a54512c3ef15efb4728c8c54a1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102167666"
---
# <a name="idebugbinder3geteeservice"></a>IDebugBinder3::GetEEService
Esse método retorna um serviço solicitado.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetEEService(
   [in] GUID        vendor,
   [in] GUID        language,
   [in] GUID        iid,
   [out] IUnknown** ppService
);
```

```csharp
Int GetEEService(
   Guid       vendor,
   Guid       language,
   Guid       iid,
   out object ppService
);
```

## <a name="parameters"></a>Parâmetros
`vendor`\
[in] `GUID` de um fornecedor (um valor nulo é aceitável).

`language`\
[in] `GUID` de um idioma (um valor nulo é aceitável).

`iid`\
[in] `IID` do serviço a ser obtido.

`ppService`\
fora Uma interface para o serviço solicitado.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Passe o `IID` para a interface [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md) ( `IID_IEEVisualizerServiceProvider` ) para ver se o serviço Visualizador de tipo está disponível. Nesse caso, o avaliador de expressão pode obter a interface [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md) para dar suporte a visualizadores de tipo. Consulte [visualizando e exibindo dados](../../../extensibility/debugger/visualizing-and-viewing-data.md) para obter detalhes.

## <a name="see-also"></a>Confira também
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
- [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)
- [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)
- [Visualizando e exibindo dados](../../../extensibility/debugger/visualizing-and-viewing-data.md)
