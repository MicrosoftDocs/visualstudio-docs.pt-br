---
title: IDebugExceptionEvent2 | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- IDebugExceptionEvent2
helpviewer_keywords:
- IDebugExceptionEvent2 interface
ms.assetid: 53d32e59-a84b-4710-833e-c5ab08100516
caps.latest.revision: 12
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 6ac2e9a85d66ad93b8b0ae1c80ee82e915fa9d86
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51743358"
---
# <a name="idebugexceptionevent2"></a>IDebugExceptionEvent2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

O mecanismo de depuração (DES) envia essa interface para o Gerenciador de sessão de depuração (SDM) quando uma exceção é lançada no programa que está sendo executado no momento.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugExceptionEvent2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 O DE implementa essa interface para relatórios que ocorreu uma exceção no programa que está sendo depurado. O [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) interface deve ser implementada no mesmo objeto como essa interface. Usa o SDM [QueryInterface](http://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) para acessar o `IDebugEvent2` interface.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 O DE cria e envia esse objeto de evento para relatar uma exceção. O evento é enviado usando o [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) função de retorno de chamada que é fornecida pelo SDM quando anexado a programa que está sendo depurado.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem de Vtable  
 A tabela a seguir mostra os métodos de `IDebugExceptionEvent2`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetException](../../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md)|Obtém informações detalhadas sobre a exceção que disparou este evento.|  
|[GetExceptionDescription](../../../extensibility/debugger/reference/idebugexceptionevent2-getexceptiondescription.md)|Obtém uma descrição legível por humanos para a exceção gerada que disparou este evento.|  
|[CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)|Determina se o mecanismo de depuração (DES) oferece suporte a opção de passar essa exceção para o programa que está sendo depurado quando a execução é retomada.|  
|[PassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-passtodebuggee.md)|Especifica se a exceção deve ser passada para o programa que está sendo depurado quando a execução é retomada, ou se a exceção deve ser descartada.|  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="remarks"></a>Comentários  
 Antes de enviar o evento, o DE verifica para ver se esse evento de exceção tiver sido designado uma exceção de primeira chance ou segunda chance por uma chamada anterior a [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md). Se ele tiver sido designado para ser uma exceção de primeira chance, o `IDebugExceptionEvent2` evento é enviado para o SDM. Caso contrário, o DE dá ao aplicativo a oportunidade de lidar com a exceção. Se nenhum manipulador de exceção é fornecido e se a exceção tiver sido designada como uma exceção de segunda chance de `IDebugExceptionEvent2` evento é enviado para o SDM. Caso contrário, o DE retoma a execução do programa, e o sistema operacional ou o tempo de execução trata a exceção.  
  
## <a name="see-also"></a>Consulte também  
 [Principais Interfaces](../../../extensibility/debugger/reference/core-interfaces.md)   
 [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)   
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)

