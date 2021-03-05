---
description: Chamado por um manipulador de eventos para recuperar resultados sobre um processo de carregamento de símbolo.
title: 'IDebugSymbolSearchEvent2:: GetSymbolSearchInfo | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolSearchEvent2::GetSymbolSearchInfo
helpviewer_keywords:
- IDebugSymbolSearchEvent2::GetSymbolSearchInfo
ms.assetid: ae9eb72b-f2aa-43b8-87ca-da19d2e78d17
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9f03562f3370268f720b2d8053bbd6a2979f6a19
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102145762"
---
# <a name="idebugsymbolsearchevent2getsymbolsearchinfo"></a>IDebugSymbolSearchEvent2::GetSymbolSearchInfo
Chamado por um manipulador de eventos para recuperar resultados sobre um processo de carregamento de símbolo.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetSymbolSearchInfo(
   IDebugModule3**    pModule,
   BSTR*              pbstrDebugMessage,
   MODULE_INFO_FLAGS* pdwModuleInfoFlags
);
```

```csharp
int GetSymbolSearchInfo(
   IDebugModule3              pModule,
   ref string                 pbstrDebugMessage,
   out enum_MODULE_INFO_FLAGS pdwModuleInfoFlags
);
```

## <a name="parameters"></a>Parâmetros
`pModule`\
fora Um objeto IDebugModule3 que representa o módulo para o qual os símbolos foram carregados.

`pbstrDebugMessage`\
[entrada, saída] Retorna uma cadeia de caracteres que contém qualquer mensagem de erro do módulo. Se não houver nenhum erro, essa cadeia de caracteres conterá apenas o nome do módulo, mas nunca estará vazia.

> [!NOTE]
> [C++] `pbstrDebugMessage` Não pode ser `NULL` e deve ser liberado com `SysFreeString` .

`pdwModuleInfoFlags`\
fora Uma combinação de sinalizadores da enumeração [MODULE_INFO_FLAGS](../../../extensibility/debugger/reference/module-info-flags.md) indicando se os símbolos foram carregados.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Quando um manipulador recebe o evento [IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md) depois que é feita uma tentativa de carregar símbolos de depuração para um módulo, o manipulador pode chamar Thismethod para determinar os resultados dessa carga.

## <a name="see-also"></a>Confira também
- [IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)
- [MODULE_INFO_FLAGS](../../../extensibility/debugger/reference/module-info-flags.md)
- [IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)
