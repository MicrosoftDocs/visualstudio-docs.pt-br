---
title: IDebugBreakEvent2 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugBreakEvent2
helpviewer_keywords:
- IDebugBreakEvent2 interface
ms.assetid: 57dfdbc2-4e68-4dbf-9579-006cd6fb1c62
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: adfe4bf801d419d2eb25ba2191a180ca261a6c3f
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31103290"
---
# <a name="idebugbreakevent2"></a>IDebugBreakEvent2
Essa interface informa o Gerenciador de sessão de depuração (SDM) que uma quebra de assíncrona foi concluída com êxito.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugBreakEvent2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 O DE implementa essa interface para oferecer suporte a quebras de usuário em um programa. O [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) interface deve ser implementada no mesmo objeto dessa interface (usa o SDM [QueryInterface](/cpp/atl/queryinterface) para acessar o `IDebugEvent2` interface).  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 As chamadas SDM [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md) quando o usuário solicitou o programa que está sendo depurado para ser pausado. Quando o programa foi pausado com êxito, o DE envia o `IDebugBreakEvent2` evento. Esse evento é enviado usando o [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) função de retorno de chamada fornecida pelo SDM quando anexado ao programa que está sendo depurado.  
  
## <a name="remarks"></a>Comentários  
 Por exemplo, um usuário pode selecionar o **quebra todos** comando o **depurar** menu para sair de um programa que executa um loop infinito. O SDM informa o programa para parar chamando [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md). O envia DE `IDebugBreakEvent2` quando o programa for interrompido por último.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)   
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)