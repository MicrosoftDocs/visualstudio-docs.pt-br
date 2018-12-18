---
title: IDebugModule3 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugModule3
helpviewer_keywords:
- IDebugModule3 interface
ms.assetid: 44f8e96e-9c59-4ffc-9a08-9c908a0e4de7
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 0b74063aa73db8258b2986ac1310d02e36027bf6
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31118447"
---
# <a name="idebugmodule3"></a>IDebugModule3
Essa interface representa um módulo que dá suporte a locais alternativos de símbolos e /justmycode estados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugModule3 : IDebugModule2  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 O mecanismo de depuração (DE) implementa essa interface para oferecer suporte a locais alternativos de símbolos e trabalhar com os estados de /justmycode (consulte a [Glossário de depurador do Visual Studio](../../../extensibility/debugger/reference/visual-studio-debugger-glossary.md) para uma definição de "/justmycode").  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Uma chamada para [GetSymbolSearchInfo](../../../extensibility/debugger/reference/idebugsymbolsearchevent2-getsymbolsearchinfo.md) retorna essa interface. O envia do [IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md) interface para o Gerenciador de depuração de sessão (SDM) usando o [evento](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) método. Além disso, uma chamada para [QueryInterface](/cpp/atl/queryinterface) em uma [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md) interface retorna essa interface.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
 Além dos métodos de [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md) interface, essa interface implementa os métodos a seguir:  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetSymbolInfo](../../../extensibility/debugger/reference/idebugmodule3-getsymbolinfo.md)|Retorna uma lista de caminhos pesquisados para símbolos e os resultados da pesquisa de cada caminho.|  
|[LoadSymbols](../../../extensibility/debugger/reference/idebugmodule3-loadsymbols.md)|Carrega e inicializa os símbolos para o módulo atual.|  
|[IsUserCode](../../../extensibility/debugger/reference/idebugmodule3-isusercode.md)|Sinalizador retorna especificando se o módulo representa o código do usuário.|  
|[SetJustMyCodeState](../../../extensibility/debugger/reference/idebugmodule3-setjustmycodestate.md)|Especifica se o módulo deve ser considerado o código do usuário ou não.|  
  
## <a name="remarks"></a>Comentários  
 O Visual Studio é o consumidor típico desta interface.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de núcleo](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)   
 [IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)   
 [GetSymbolSearchInfo](../../../extensibility/debugger/reference/idebugsymbolsearchevent2-getsymbolsearchinfo.md)