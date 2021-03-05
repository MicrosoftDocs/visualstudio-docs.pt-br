---
description: Essa interface é enviada pelo mecanismo de depuração (DE) para o SDM (Gerenciador de depuração de sessão) para gerar uma cadeia de caracteres.
title: IDebugOutputStringEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugOutputStringEvent2
helpviewer_keywords:
- IDebugOutputStringEvent2 interface
ms.assetid: 86596fd1-cecc-4813-8add-dc3d70068f9b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 604eace2f5f4be7a35b6f4b736722b435cf06928
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102169945"
---
# <a name="idebugoutputstringevent2"></a>IDebugOutputStringEvent2
Essa interface é enviada pelo mecanismo de depuração (DE) para o SDM (Gerenciador de depuração de sessão) para gerar uma cadeia de caracteres.

## <a name="syntax"></a>Sintaxe

```
IDebugOutputStringEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O DE implementa essa interface para enviar uma cadeia de caracteres para a janela de **saída** do IDE. A interface [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) deve ser implementada no mesmo objeto que essa interface. O SDM usa [QueryInterface](/cpp/atl/queryinterface) para acessar a `IDebugEvent2` interface.

## <a name="notes-for-callers"></a>Observações para chamadores
 O DE cria e envia este objeto de evento para enviar uma cadeia de caracteres para a janela de **saída** . O evento é enviado usando a função de retorno de chamada [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) que é fornecida pelo SDM quando ele é anexado ao programa que está sendo depurado.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra o método de `IDebugOutputStringEvent2` .

|Método|Descrição|
|------------|-----------------|
|[GetString](../../../extensibility/debugger/reference/idebugoutputstringevent2-getstring.md)|Obtém a mensagem de exibição.|

## <a name="remarks"></a>Comentários
 Por exemplo, no código não gerenciado, a cadeia de caracteres a ser impressa pode se originar quando o programa que está sendo depurado envia uma cadeia de caracteres para a função do Win32 `OutputDebugString` . Essa cadeia de caracteres é interceptada pelo DE e enviada para o SDM como o `IDebugOutputStringEvent2` evento.

 Use [IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md) para enviar uma mensagem que requer uma resposta do usuário.

 Use [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md) para enviar uma mensagem de erro que não requer uma resposta.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md)
- [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
