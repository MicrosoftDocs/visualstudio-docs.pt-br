---
description: Enviado do mecanismo de depuração (DE) para o SDM (Gerenciador de depuração de sessão) quando o nome de um programa é alterado.
title: IDebugProgramNameChangedEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProgramNameChangedEvent2 interface
ms.assetid: be1f1cd5-0b2f-435c-a052-dca28a7c978d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 60fbc8aac3fd621a8f19074682bd82fbe957ed3b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053692"
---
# <a name="idebugprogramnamechangedevent2"></a>IDebugProgramNameChangedEvent2
Enviado do mecanismo de depuração (DE) para o SDM (Gerenciador de depuração de sessão) quando o nome de um programa é alterado.

## <a name="syntax"></a>Sintaxe

```
IDebugProgramNameChangedEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O DE implementa essa interface para relatar que o nome do programa foi alterado. A interface [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) deve ser implementada no mesmo objeto que essa interface. O SDM usa [QueryInterface](/cpp/atl/queryinterface) para acessar a interface **IDebugEvent2** .

## <a name="notes-for-callers"></a>Observações para chamadores
 O DE cria e envia este objeto de evento para relatar uma alteração de nome de programa. O DE envia esse evento usando a função de retorno de chamada [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) que é fornecida pelo SDM quando anexada ao programa que está sendo depurado. O fornecedor da porta personalizada envia esse evento usando a interface I.

## <a name="requirements"></a>Requisitos
 Cabeçalho: Msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll
