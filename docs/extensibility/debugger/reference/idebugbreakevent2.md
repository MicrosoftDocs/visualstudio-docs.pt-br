---
description: Essa interface diz ao SDM (Gerenciador de depuração de sessão) que uma interrupção assíncrona foi concluída com êxito.
title: IDebugBreakEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakEvent2
helpviewer_keywords:
- IDebugBreakEvent2 interface
ms.assetid: 57dfdbc2-4e68-4dbf-9579-006cd6fb1c62
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: dddf2c69cf7ccf221c00e88fc159b762284483ff
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102143578"
---
# <a name="idebugbreakevent2"></a>IDebugBreakEvent2
Essa interface diz ao SDM (Gerenciador de depuração de sessão) que uma interrupção assíncrona foi concluída com êxito.

## <a name="syntax"></a>Sintaxe

```
IDebugBreakEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O DE implementa essa interface para dar suporte a quebras de usuário em um programa. A interface [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) deve ser implementada no mesmo objeto que essa interface (o SDM usa [QueryInterface](/cpp/atl/queryinterface) para acessar a `IDebugEvent2` interface).

## <a name="notes-for-callers"></a>Observações para chamadores
 O SDM chama [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md) quando o usuário solicitou a depuração do programa a ser pausado. Quando o programa foi pausado com êxito, o DE envia o `IDebugBreakEvent2` evento. Esse evento é enviado usando a função de retorno de chamada [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) fornecida pelo SDM quando ele é anexado ao programa que está sendo depurado.

## <a name="remarks"></a>Comentários
 Por exemplo, um usuário pode selecionar o comando **quebrar tudo** no menu **depurar** para interromper um programa que está executando um loop infinito. O SDM informa o programa para parar chamando [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md). O DE envia `IDebugBreakEvent2` quando o programa finalmente para.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
