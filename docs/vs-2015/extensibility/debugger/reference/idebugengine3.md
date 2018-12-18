---
title: IDebugEngine3 | Microsoft Docs
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
- IDebugEngine3
helpviewer_keywords:
- IDebugEngine3 interface
ms.assetid: 8bdf4bb7-3b5d-4991-8981-772d4f6bb656
caps.latest.revision: 16
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: f66a17335c2bd9a4401f8490887f7ab2ab77ae80
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51760996"
---
# <a name="idebugengine3"></a>IDebugEngine3
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Representa um mecanismo de depuração único (DES) que controla a depuração de um ou mais módulos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugEngine3 : IDebugEngine2  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 Essa interface é implementada por um DE personalizado (se ele dá suporte a símbolos) para habilitar o estado de JustMyCode. Esta interface deve ser implementada por DE se ele dá suporte a símbolos e JustMyCode.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Essa interface é chamada pelo Gerenciador de depuração de sessão (SDM) para passar opções de usuário para locais de onde carregar os símbolos. Ele também é chamado para definir o GUID do mecanismo de quando ela é instanciada (esse GUID com base nas métricas do momento do mecanismo de registro). O SDM também chama essa interface para definir o estado de JustMyCode e definir todas as exceções conhecidas pelo depurador para um estado especificado.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem de Vtable  
 Além dos métodos herdados de [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md), o `IDebugEngine3` interface expõe os métodos a seguir.  
  
|Método|Descrição|  
|------------|-----------------|  
|[SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)|Define o caminho ou caminhos que o DE será usado para procurar símbolos de depuração.|  
|[LoadSymbols](../../../extensibility/debugger/reference/idebugengine3-loadsymbols.md)|Carrega os símbolos para todos os módulos que ainda não tiveram seus símbolos carregados.|  
|[SetJustMyCodeState](../../../extensibility/debugger/reference/idebugengine3-setjustmycodestate.md)|Informa o DE sobre as informações de JustMyCode.|  
|[SetEngineGuid](../../../extensibility/debugger/reference/idebugengine3-setengineguid.md)|Define o GUID DE métricas.|  
|[SetAllExceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md)|Defina todas as exceções pendente no momento para um estado especificado.|  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)

