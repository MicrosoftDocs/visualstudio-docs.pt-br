---
description: Essa interface é enviada pelo mecanismo de depuração (DE) para indicar que os símbolos de depuração para um módulo que está sendo depurado foram carregados.
title: IDebugSymbolSearchEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolSearchEvent2
helpviewer_keywords:
- IDebugSymbolSearchEvent2
ms.assetid: 9b946d55-ff85-44eb-b40a-efbf8282eafd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5a4ef5008740f563f2f7f986f73c8bbfbb94ef6b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053133"
---
# <a name="idebugsymbolsearchevent2"></a>IDebugSymbolSearchEvent2
Essa interface é enviada pelo mecanismo de depuração (DE) para indicar que os símbolos de depuração para um módulo que está sendo depurado foram carregados.

## <a name="syntax"></a>Sintaxe

```
IDebugSymbolSearchEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O DE implementa essa interface para relatar que os símbolos de um módulo foram carregados. A interface [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) deve ser implementada no mesmo objeto que essa interface. O SDM usa [QueryInterface](/cpp/atl/queryinterface) para acessar a `IDebugEvent2` interface.

## <a name="notes-for-callers"></a>Observações para chamadores
 O DE cria e envia este objeto de evento para relatar que os símbolos de um módulo foram carregados. O evento é enviado usando a função de retorno de chamada [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) que é fornecida pelo SDM quando anexada ao programa que está sendo depurado.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A `IDebugSymbolSearchEvent2` interface expõe o método a seguir.

|Método|Descrição|
|------------|-----------------|
|[GetSymbolSearchInfo](../../../extensibility/debugger/reference/idebugsymbolsearchevent2-getsymbolsearchinfo.md)|Recupera informações sobre os resultados de uma pesquisa de símbolo.|

## <a name="remarks"></a>Comentários
 Esse evento será enviado mesmo que os símbolos não sejam carregados. A chamada `IDebugSymbolSearchEvent2::GetSymbolSearchInfo` permite que o manipulador desse evento determine se o módulo realmente tem qualquer símbolo.

 O Visual Studio normalmente usa esse evento para atualizar o status dos símbolos carregados na janela **módulos** .

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
