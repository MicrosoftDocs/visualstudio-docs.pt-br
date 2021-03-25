---
description: O mecanismo de depuração (DE) pode enviar esse evento opcional para o SDM (Gerenciador de depuração de sessão) quando um programa for interrompido.
title: IDebugStopCompleteEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugStopCompleteEvent2 interface
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8e4fd1826f44cb1d830ef45874b1c41c21a34895
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087139"
---
# <a name="idebugstopcompleteevent2"></a>IDebugStopCompleteEvent2

O mecanismo de depuração (DE) pode enviar esse evento opcional para o SDM (Gerenciador de depuração de sessão) quando um programa for interrompido.

## <a name="syntax"></a>Sintaxe

```
IDebugStopCompleteEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores

Essa interface foi introduzida com o Visual Studio 2005. Versões anteriores não suportavam a interrupção assíncrona.

- [Stop](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md) é chamado pelo SDM em cenários de vários processos ou vários programas. Quando um programa envia um evento de parada para o SDM, o SDM solicita que outros programas parem também.

Stop é usado para informar de forma assíncrona o SDM que um programa parou. Informar o SDM é útil para um mecanismo de depuração de intérprete, no qual às vezes nenhum código está sendo executado dentro do programa depurado, portanto, [Stop](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md) não pode ser concluído de forma síncrona. Se um mecanismo de depuração quiser empregar essa notificação assíncrona, ele deverá retornar `S_ASYNC_STOP` de [Stop](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md).

## <a name="requirements"></a>Requisitos

Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll
