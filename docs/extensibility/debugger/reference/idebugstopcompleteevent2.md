---
title: IDebugStopCompleteEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugStopCompleteEvent2 interface
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bee46a1f097d1bee98354acb792f75ea9431f301
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99897214"
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
