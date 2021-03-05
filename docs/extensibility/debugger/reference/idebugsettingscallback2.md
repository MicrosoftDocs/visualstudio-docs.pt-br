---
description: Habilita os mecanismos de depuração para ler as configurações de métrica remotamente.
title: IDebugSettingsCallback2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSettingsCallback2 interface
ms.assetid: 7e525d0b-7d7a-4d1c-8b78-e1398fa922f2
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7053c45ba86f4bea54befc3bde67d831cc9c822e
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102168654"
---
# <a name="idebugsettingscallback2"></a>IDebugSettingsCallback2
Habilita os mecanismos de depuração para ler as configurações de métrica remotamente.

## <a name="syntax"></a>Sintaxe

```
IDebugSettingsCallback2D : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
Essa interface é implementada pelo retorno de chamada do evento do Gerenciador de depuração de sessão e consumida pelos mecanismos de depuração. Ele também pode ser usado localmente em vez de Dbgmetric [d]. lib.

## <a name="methods"></a>Métodos
A tabela a seguir mostra os métodos de `IDebugSettingsCallback2` .

|Método|Descrição|
|------------|-----------------|
|[EnumEEs](../../../extensibility/debugger/reference/idebugsettingscallback2-enumees.md)|Enumera os avaliadores de expressão disponíveis de acordo com os identificadores de idioma e fornecedor.|
|[GetEELocalObject](../../../extensibility/debugger/reference/idebugsettingscallback2-geteelocalobject.md)|Recupera um objeto local do avaliador de expressão dado a métrica.|
|[GetEEMetricDword](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricdword.md)|Recupera um valor que corresponde à métrica especificada do avaliador de expressão.|
|[GetEEMetricFile](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricfile.md)|Recupera o arquivo de métrica do avaliador de expressão dado o nome ou a métrica.|
|[GetEEMetricGuid](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricguid.md)|Recupera o identificador exclusivo para uma métrica do avaliador de expressão Considerando seu nome.|
|[GetEEMetricString](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricstring.md)|Recupera a cadeia de caracteres de valor de uma métrica do avaliador de expressão Considerando seu nome.|
|[GetMetricDword](../../../extensibility/debugger/reference/idebugsettingscallback2-getmetricdword.md)|Recupera o valor de uma métrica de acordo com seu nome.|
|[GetMetricGuid](../../../extensibility/debugger/reference/idebugsettingscallback2-getmetricguid.md)|Recupera o identificador exclusivo de uma métrica de acordo com seu nome.|
|[GetMetricString](../../../extensibility/debugger/reference/idebugsettingscallback2-getmetricstring.md)|Recupera a cadeia de caracteres de valor da métrica de acordo com seu nome.|

## <a name="requirements"></a>Requisitos
Cabeçalho: Msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="example"></a>Exemplo
O exemplo a seguir mostra uma função que usa um objeto **IDebugSettingsCallback2** como um parâmetro.

```cpp
HRESULT GetDebugSettingsCallback (IDebugSettingsCallback2 **ppCallback)
{
    HRESULT hRes = E_FAIL;

    if ( ppCallback )
    {
        if ( EVAL(m_pdec) )
            hRes = m_pdec->QueryInterface(IID_IDebugSettingsCallback2, (void **)ppCallback);
        else
            hRes = E_FAIL;
    }
    else
        hRes = E_INVALIDARG;

    return ( hRes );
}
```
