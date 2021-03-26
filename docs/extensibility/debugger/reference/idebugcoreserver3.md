---
description: Essa interface fornece acesso a informações sobre o servidor em que o processo está sendo executado.
title: IDebugCoreServer3 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3
helpviewer_keywords:
- IDebugCoreServer3 interface
ms.assetid: 51f5f41b-a5a4-4df0-a703-41f3d1811d7f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ab605db6a49b8b7cc9893692ff1bb9e6da15171f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088140"
---
# <a name="idebugcoreserver3"></a>IDebugCoreServer3
Essa interface fornece acesso a informações sobre o servidor em que o processo está sendo executado.

## <a name="syntax"></a>Sintaxe

```
IDebugCoreServer3 : IDebugCoreServer2
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O Visual Studio implementa essa interface.

## <a name="notes-for-callers"></a>Observações para chamadores
 Use [QueryInterface](/cpp/atl/queryinterface) para obter essa interface de uma interface [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md) . Uma chamada para [GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md) também pode retornar essa interface. Essa interface é usada com mais frequência por um fornecedor de porta personalizado para iniciar programas em um servidor (local ou remoto).

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 Além dos métodos na interface [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md) , essa interface implementa os seguintes métodos:

|Método|Descrição|
|------------|-----------------|
|[GetServerName](../../../extensibility/debugger/reference/idebugcoreserver3-getservername.md)|Recupera o nome do servidor.|
|[GetServerFriendlyName](../../../extensibility/debugger/reference/idebugcoreserver3-getserverfriendlyname.md)|Recupera uma versão amigável do nome do servidor|
|[EnableAutoAttach](../../../extensibility/debugger/reference/idebugcoreserver3-enableautoattach.md)|Informa aos mecanismos de depuração específicos para anexar automaticamente aos processos quando esses processos são iniciados.|
|[DiagnoseWebDebuggingError](../../../extensibility/debugger/reference/idebugcoreserver3-diagnosewebdebuggingerror.md)|Recupera um código de erro específico quando o anexo automático falha.|
|[CreateInstanceInServer](../../../extensibility/debugger/reference/idebugcoreserver3-createinstanceinserver.md)|Cria uma instância de um mecanismo de depuração no servidor.|
|[QueryIsLocal](../../../extensibility/debugger/reference/idebugcoreserver3-queryislocal.md)|Recupera um sinalizador que indica se o servidor está no mesmo computador que o chamador.|
|[GetConnectionProtocol](../../../extensibility/debugger/reference/idebugcoreserver3-getconnectionprotocol.md)|Recupera um valor que indica o protocolo que está sendo usado para se comunicar com o servidor.|
|[DisableAutoAttach](../../../extensibility/debugger/reference/idebugcoreserver3-disableautoattach.md)|Desabilita todas as configurações de anexo automático para todos os mecanismos de depuração sobre os quais este servidor sabe.|

## <a name="remarks"></a>Comentários
 Um fornecedor de porta personalizado recebe a interface [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md) em uma chamada para [evento](../../../extensibility/debugger/reference/idebugportevents2-event.md). A `IDebugCoreServer3` interface pode ser obtida a partir dessa interface.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
- [GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)
