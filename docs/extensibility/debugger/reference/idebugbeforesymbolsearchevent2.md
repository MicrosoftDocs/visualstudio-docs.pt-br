---
description: O mecanismo de depuração (DE) envia essa interface para o SDM (Gerenciador de depuração de sessão) para definir a mensagem da barra de status durante cargas de símbolo.
title: IDebugBeforeSymbolSearchEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugBeforeSymbolSearchEvent2 interface
ms.assetid: 679fd7b1-765a-41a8-a046-63240c09a499
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fdf292a309e514f5b437b129bbfc6ee125df8269
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102167731"
---
# <a name="idebugbeforesymbolsearchevent2"></a>IDebugBeforeSymbolSearchEvent2
O mecanismo de depuração (DE) envia essa interface para o SDM (Gerenciador de depuração de sessão) para definir a mensagem da barra de status durante cargas de símbolo.

## <a name="syntax"></a>Sintaxe

```
IDebugBeforeSymbolSearchEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O DE implementa essa interface quando ela deve definir a mensagem da barra de status durante cargas de símbolo. Essa interface é implementada somente por mecanismos de depuração que funcionam com o ou fazem parte de intérpretes de script. A interface [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) deve ser implementada no mesmo objeto que essa interface (o SDM usa **QueryInterface** para acessar a interface **IDebugEvent2** ).

## <a name="notes-for-callers"></a>Observações para chamadores
 O DE cria e envia esse objeto DE evento quando ele deve definir a mensagem da barra de status durante cargas de símbolo. O evento é enviado usando a função de retorno de chamada [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) fornecida pelo SDM quando ele é anexado ao programa que está sendo depurado.

## <a name="methods"></a>Métodos
 A tabela a seguir mostra os métodos de `IDebugBeforeSymbolSearchEvent2` .

|Método|Descrição|
|------------|-----------------|
|[GetModuleName](../../../extensibility/debugger/reference/idebugbeforesymbolsearchevent2-getmodulename.md)|Recupera o nome do módulo que está sendo depurado no momento.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: Msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll
