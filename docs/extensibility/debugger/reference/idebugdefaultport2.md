---
title: IDebugDefaultPort2 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugDefaultPort2
helpviewer_keywords:
- IDebugDefaultPort2 interface
ms.assetid: 7b3452af-9a96-4c4c-9946-4339b72d3d7b
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: c6d131ab24cc57af1846f89b61afa2d89ae2cacb
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31106897"
---
# <a name="idebugdefaultport2"></a>IDebugDefaultPort2
Essa interface fornece vários métodos para acessar o servidor de uma porta e recursos de notificação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugDefaultPort2 : IDebugPort2  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 O Visual Studio implementa essa interface para representar a porta de depuração para acessar os programas. Um fornecedor de porta personalizada também pode implementar essa interface se trata de depuração remota.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Um argumento para métodos de [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md) interface fornece essa interface. Chamando [QueryInterface](/cpp/atl/queryinterface) em uma [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) interface também pode obter essa interface.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
 Além dos métodos definidos no [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md), essa interface implementa os métodos a seguir:  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetPortNotify](../../../extensibility/debugger/reference/idebugdefaultport2-getportnotify.md)|Obtém a interface de notificação de porta desta porta.|  
|[GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)|Obtém a interface para o servidor que hospeda essa porta.|  
|[QueryIsLocal](../../../extensibility/debugger/reference/idebugdefaultport2-queryislocal.md)|Determina se essa porta está em execução no computador local.|  
  
## <a name="remarks"></a>Comentários  
 O nome "`IDebugDefaultPort2`" é uma designação incorreta, pois ele não representa uma porta padrão. Ele pode ser chamado "IDebugPort3".  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)   
 [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)