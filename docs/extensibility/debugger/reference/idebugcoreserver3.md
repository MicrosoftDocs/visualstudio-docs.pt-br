---
title: IDebugCoreServer3 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugCoreServer3
helpviewer_keywords:
- IDebugCoreServer3 interface
ms.assetid: 51f5f41b-a5a4-4df0-a703-41f3d1811d7f
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 5066521dbed42790d508becc1a3591dff3ae559d
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31108525"
---
# <a name="idebugcoreserver3"></a>IDebugCoreServer3
Essa interface fornece acesso às informações sobre o processo está em execução no servidor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugCoreServer3 : IDebugCoreServer2  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 O Visual Studio implementa essa interface.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Use [QueryInterface](/cpp/atl/queryinterface) para obter essa interface de um [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md) interface. Uma chamada para [GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md) também pode retornar a esta interface. Essa interface é usada com mais frequência por um fornecedor de porta personalizada para iniciar programas em um servidor (local ou remoto).  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
 Além dos métodos de [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md) interface, essa interface implementa os métodos a seguir:  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetServerName](../../../extensibility/debugger/reference/idebugcoreserver3-getservername.md)|Recupera o nome do servidor.|  
|[GetServerFriendlyName](../../../extensibility/debugger/reference/idebugcoreserver3-getserverfriendlyname.md)|Recupera uma versão amigável do nome do servidor|  
|[EnableAutoAttach](../../../extensibility/debugger/reference/idebugcoreserver3-enableautoattach.md)|Informa os mecanismos de depuração específicos para anexar automaticamente processos quando iniciar esses processos.|  
|[DiagnoseWebDebuggingError](../../../extensibility/debugger/reference/idebugcoreserver3-diagnosewebdebuggingerror.md)|Recupera um código de erro específico quando Falha ao anexar automático.|  
|[CreateInstanceInServer](../../../extensibility/debugger/reference/idebugcoreserver3-createinstanceinserver.md)|Cria uma instância de um mecanismo de depuração no servidor.|  
|[QueryIsLocal](../../../extensibility/debugger/reference/idebugcoreserver3-queryislocal.md)|Recupera um sinalizador que indica se o servidor está no mesmo computador que o chamador.|  
|[GetConnectionProtocol](../../../extensibility/debugger/reference/idebugcoreserver3-getconnectionprotocol.md)|Recupera um valor que indica o protocolo usado para se comunicar com o servidor.|  
|[DisableAutoAttach](../../../extensibility/debugger/reference/idebugcoreserver3-disableautoattach.md)|Desabilita todos os anexar automaticamente as configurações para todos os mecanismos de depuração que neste servidor conhece.|  
  
## <a name="remarks"></a>Comentários  
 Um fornecedor de porta personalizada recebe o [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md) interface em uma chamada para [evento](../../../extensibility/debugger/reference/idebugportevents2-event.md). O `IDebugCoreServer3` interface pode ser obtida da interface.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)   
 [GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)