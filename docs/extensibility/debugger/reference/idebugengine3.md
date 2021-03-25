---
description: Representa um único mecanismo DE depuração (DE) que controla a depuração de um ou mais módulos.
title: IDebugEngine3 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3
helpviewer_keywords:
- IDebugEngine3 interface
ms.assetid: 8bdf4bb7-3b5d-4991-8981-772d4f6bb656
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3a10f439ba344b71cd31fd990928b7804b6c11d4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066178"
---
# <a name="idebugengine3"></a>IDebugEngine3
Representa um único mecanismo DE depuração (DE) que controla a depuração de um ou mais módulos.

## <a name="syntax"></a>Sintaxe

```
IDebugEngine3 : IDebugEngine2
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Essa interface é implementada por um DE um personalizado (se oferecer suporte a símbolos) para habilitar o estado JustMyCode. Essa interface deve ser implementada pelo DE se oferecer suporte a símbolos e JustMyCode.

## <a name="notes-for-callers"></a>Observações para chamadores
 Essa interface é chamada pelo SDM (Gerenciador de depuração de sessão) para passar as opções do usuário para locais dos quais carregar símbolos. Também é chamado para definir o GUID do mecanismo quando ele é instanciado (esse GUID é baseado nas métricas do momento do registro do mecanismo). O SDM também chama essa interface para definir o estado JustMyCode e definir todas as exceções conhecidas pelo depurador para um estado especificado.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 Além dos métodos herdados de [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md), a `IDebugEngine3` interface expõe os métodos a seguir.

|Método|Descrição|
|------------|-----------------|
|[SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)|Define o caminho ou caminhos que o deve usar para procurar símbolos de depuração.|
|[LoadSymbols](../../../extensibility/debugger/reference/idebugengine3-loadsymbols.md)|Carrega os símbolos para todos os módulos que ainda não tinham seus símbolos carregados.|
|[SetJustMyCodeState](../../../extensibility/debugger/reference/idebugengine3-setjustmycodestate.md)|Informa o sobre as informações de JustMyCode.|
|[SetEngineGuid](../../../extensibility/debugger/reference/idebugengine3-setengineguid.md)|Define o GUID de da métrica.|
|[SetAllExceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md)|Defina todas as exceções atualmente pendentes para um estado especificado.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
