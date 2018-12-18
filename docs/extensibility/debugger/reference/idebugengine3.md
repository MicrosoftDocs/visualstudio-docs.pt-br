---
title: IDebugEngine3 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugEngine3
helpviewer_keywords:
- IDebugEngine3 interface
ms.assetid: 8bdf4bb7-3b5d-4991-8981-772d4f6bb656
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 291f5ca6f945abe9e0322839eb80c38b60674ce4
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31114411"
---
# <a name="idebugengine3"></a>IDebugEngine3
Representa um mecanismo de depuração única (DE) que controla a depuração de um ou mais módulos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugEngine3 : IDebugEngine2  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 Essa interface é implementada por um DE personalizados (se ele dá suporte a símbolos) para habilitar o estado de /justmycode. Esta interface deve ser implementada por DE se ele dá suporte a símbolos e /justmycode.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Essa interface é chamada, o Gerenciador de sessão de depuração (SDM) para passar opções de usuário para locais de onde carregar símbolos. Ele também é chamado para definir o GUID do mecanismo de quando ele é instanciado (esse GUID com base nas métricas do mecanismo de registro). O SDM também chama essa interface para definir o estado de /justmycode e definir todas as exceções conhecidas pelo depurador para um estado especificado.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
 Além dos métodos herdados de [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md), o `IDebugEngine3` interface expõe os métodos a seguir.  
  
|Método|Descrição|  
|------------|-----------------|  
|[SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)|Define o caminho ou caminhos que o DE usará para pesquisa de símbolos de depuração.|  
|[LoadSymbols](../../../extensibility/debugger/reference/idebugengine3-loadsymbols.md)|Carrega símbolos para todos os módulos que ainda não tiveram seus símbolos carregados.|  
|[SetJustMyCodeState](../../../extensibility/debugger/reference/idebugengine3-setjustmycodestate.md)|Informa o DE sobre as informações de /justmycode.|  
|[SetEngineGuid](../../../extensibility/debugger/reference/idebugengine3-setengineguid.md)|Define o GUID DE métricas.|  
|[SetAllExceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md)|Defina todas as exceções pendente no momento para um estado especificado.|  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)