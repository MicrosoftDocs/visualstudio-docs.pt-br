---
description: Essa interface é usada pelo mecanismo de depuração (DE) para enviar uma mensagem para o Visual Studio que requer uma resposta do usuário.
title: IDebugMessageEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMessageEvent2
helpviewer_keywords:
- IDebugMessageEvent2 interface
ms.assetid: a9ff3d00-e9ac-4cd6-bda9-584a4815aff8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c5593e822b974ddb7c666f622192e3e4630b7222
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058424"
---
# <a name="idebugmessageevent2"></a>IDebugMessageEvent2
Essa interface é usada pelo mecanismo de depuração (DE) para enviar uma mensagem para o Visual Studio que requer uma resposta do usuário.

## <a name="syntax"></a>Sintaxe

```
IDebugMessageEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O DE implementa essa interface para enviar uma mensagem ao Visual Studio que requer uma resposta do usuário. A interface [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) deve ser implementada no mesmo objeto que essa interface. O SDM usa [QueryInterface](/cpp/atl/queryinterface) para acessar a `IDebugEvent2` interface.

 A implementação dessa interface deve comunicar a chamada de [Setresponse](../../../extensibility/debugger/reference/idebugmessageevent2-setresponse.md) do Visual Studio para o de. Por exemplo, isso pode ser feito com uma mensagem postada no thread DE manipulação DE mensagens DE DE, ou o objeto que implementa essa interface pode conter uma referência para a DE e retornar para o DE com a resposta passada para `IDebugMessageEvent2::SetResponse` .

## <a name="notes-for-callers"></a>Observações para chamadores
 O DE cria e envia este objeto de evento para exibir uma mensagem para o usuário que requer uma resposta. O evento é enviado usando a função de retorno de chamada [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) que é fornecida pelo SDM quando ele é anexado ao programa que está sendo depurado.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugMessageEvent2` .

|Método|Descrição|
|------------|-----------------|
|[GetMessage](../../../extensibility/debugger/reference/idebugmessageevent2-getmessage.md)|Obtém a mensagem a ser exibida.|
|[SetResponse](../../../extensibility/debugger/reference/idebugmessageevent2-setresponse.md)|Define a resposta, se houver, da caixa de mensagem.|

## <a name="remarks"></a>Comentários
 O DE usará essa interface se exigir uma resposta específica do usuário para uma mensagem específica. Por exemplo, se o DE receber uma mensagem DE "acesso negado" após uma tentativa de anexar remotamente a um programa, o DE enviará essa mensagem específica para o Visual Studio em um `IDebugMessageEvent2` evento com o estilo da caixa de mensagem `MB_RETRYCANCEL` . Isso permite que o usuário tente novamente ou cancele a operação de anexação.

 O DE especifica como essa mensagem deve ser tratada seguindo as convenções da função do Win32 `MessageBox` (consulte [AfxMessageBox](/cpp/mfc/reference/cstring-formatting-and-message-box-display#afxmessagebox) para obter detalhes).

 Use a interface [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md) para enviar mensagens para o Visual Studio que não exigem uma resposta do usuário.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)
