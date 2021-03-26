---
description: Essa interface registrada permite que o SDM (Gerenciador de depuração de sessão) obtenha informações sobre programas que foram publicados por meio da interface IDebugProgramPublisher2.
title: IDebugProgramProvider2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramProvider2
helpviewer_keywords:
- IDebugProgramProvider2 interface
ms.assetid: a9ec7b3e-a59c-4069-b2ee-6f45916eeb78
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5bead60e23c708d8a23fcd382b4db0f3f9f7e4c1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065236"
---
# <a name="idebugprogramprovider2"></a>IDebugProgramProvider2
Essa interface registrada permite que o SDM (Gerenciador de depuração de sessão) obtenha informações sobre programas que foram "publicados" por meio da interface [IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md) .

## <a name="syntax"></a>Sintaxe

```
IDebugProgramProvider2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
O mecanismo de depuração (DE) implementa essa interface para fornecer informações sobre os programas que estão sendo depurados. Essa interface é registrada na seção de do registro usando a métrica `metricProgramProvider` , conforme descrito em [auxiliares de SDK para depuração](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md).

## <a name="notes-for-callers"></a>Observações para chamadores
Chame `CoCreateInstance` a função de com com o `CLSID` do provedor de programa que é obtido do registro. Consulte o exemplo.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable

|Método|Descrição|
|------------|-----------------|
|[GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)|Obtém informações sobre programas em execução, filtrados de várias maneiras.|
|[GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)|Obtém um nó de programa, dado uma ID de processo específica.|
|[WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)|Estabelece um retorno de chamada para inspecionar eventos de provedor associados a tipos específicos de processos.|
|[SetLocale](../../../extensibility/debugger/reference/idebugprogramprovider2-setlocale.md)|Estabelece uma localidade para qualquer recurso específico de idioma necessário para o DE.|

## <a name="remarks"></a>Comentários
Normalmente, um processo usa essa interface para descobrir sobre os programas em execução nesse processo.

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="example"></a>Exemplo

```cpp
IDebugProgramProvider2 *GetProgramProvider(GUID *pDebugEngineGuid)
{
    // This is typically defined globally. For this example, it is
    // defined here.
    static const WCHAR strRegistrationRoot[] = L"Software\\Microsoft\\VisualStudio\\8.0Exp";
    IDebugProgramProvider2 *pProvider = NULL;
    if (pDebugEngineGuid != NULL) {
        CLSID clsidProvider = { 0 };
        ::GetMetric(NULL,
                    metrictypeEngine,
                    *pDebugEngineGuid,
                    metricProgramProvider,
                    &clsidProvider,
                    strRegistrationRoot);
        if (!IsEqualGUID(clsidProvider,GUID_NULL)) {
            CComPtr<IDebugProgramProvider2> spProgramProvider;
            spProgramProvider.CoCreateInstance(clsidProvider);
            if (spProgramProvider != NULL) {
                pProvider = spProgramProvider.Detach();
            }
        }
    }
    return(pProvider);
}
```

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)
- [Auxiliares do SDK para depuração](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
