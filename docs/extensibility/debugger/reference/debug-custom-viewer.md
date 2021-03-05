---
description: Uma estrutura que identifica um visualizador personalizado ou um visualizador de tipo.
title: DEBUG_CUSTOM_VIEWER | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUG_CUSTOM_VIEWER
helpviewer_keywords:
- DEBUG_CUSTOM_VIEWER structure
ms.assetid: 8e0ef3f0-0107-48e8-a037-6e52b4c4ed9d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 46133d2b2800977b0819835f578b04569c4f5ce8
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102151051"
---
# <a name="debug_custom_viewer"></a>DEBUG_CUSTOM_VIEWER
Uma estrutura que identifica um visualizador personalizado ou um visualizador de tipo.

## <a name="syntax"></a>Sintaxe

```cpp
typedef struct tagDEBUG_CUSTOM_VIEWER {
    DWORD dwID;
    BSTR  bstrMenuName;
    BSTR  bstrDescription;
    GUID  guidLang;
    GUID  guidVendor;
    BSTR  bstrMetric;
} DEBUG_CUSTOM_VIEWER;
```

```csharp
public struct DEBUG_CUSTOM_VIEWER {
    public uint   dwID;
    public string bstrMenuName;
    public string bstrDescription;
    public Guid   guidLang;
    public Guid   guidVendor;
    public string bstrMetric;
};
```

## <a name="members"></a>Membros
`dwID`\
Uma ID para diferenciar vários visualizadores ou visualizadores implementados por um `GUID` .

`bstrMenuName`\
O texto que será exibido no menu suspenso.

`bstrDescription`\
Uma descrição do visualizador personalizado ou do Visualizador de tipo (deve ser um valor nulo se não for usado).

`guidLang`\
Idioma do avaliador de expressão de fornecimento.

`guidVendor`\
Fornecedor do avaliador de expressão de fornecimento.

`bstrMetric`\
Métrica sob a qual o visualizador personalizado ou o Visualizador de tipo `CLSID` é armazenado.

## <a name="remarks"></a>Comentários
Uma lista dessa estrutura é retornada por uma chamada para o método [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) (e, por extensão, o método [GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md) ).

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)
- [GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)
