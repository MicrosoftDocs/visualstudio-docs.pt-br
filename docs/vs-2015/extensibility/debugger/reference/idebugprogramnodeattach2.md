---
title: IDebugProgramNodeAttach2 | Microsoft Docs
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
- IDebugProgramNodeAttach2
helpviewer_keywords:
- IDebugProgramNodeAttach2 interface
ms.assetid: 46b37ac9-a026-4ad3-997b-f19e2f8deb73
caps.latest.revision: 4
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 0ba1dd00fc661e6b35f30998376c1970096a4d57
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51774764"
---
# <a name="idebugprogramnodeattach2"></a>IDebugProgramNodeAttach2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Permite que um nó de programa ser notificado de uma tentativa de anexar ao programa associado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugProgramNodeAttach2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 Essa interface é implementada na mesma classe que implementa o [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) interface para receber a notificação de uma operação de anexação e oferecem uma oportunidade de cancelar a operação de anexação.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Obtenha essa interface por meio da chamada a `QueryInterface` método em um [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) objeto. O [OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) método deve ser chamado antes do [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) método para permitir que o nó de programa para interromper o processo de anexação.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem de Vtable  
 Essa interface implementa o método a seguir:  
  
|Método|Descrição|  
|------------|-----------------|  
|[OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)|Anexa ao programa associado ou adia o processo de anexação para o [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) método.|  
  
## <a name="remarks"></a>Comentários  
 Essa interface é a alternativa preferida para preteridas [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md) método. Todos os mecanismos de depuração são sempre carregados com o `CoCreateInstance` de função, ou seja, eles são instanciados fora do espaço de endereço do programa que está sendo depurado.  
  
 Se uma implementação anterior da `IDebugProgramNode2::Attach_V7` método era simplesmente definindo o `GUID` do programa que está sendo depurado, em seguida, somente os [OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) método precisa ser implementado.  
  
 Se uma implementação anterior da `IDebugProgramNode2::Attach_V7` método usado a interface de retorno de chamada que foi fornecida, em seguida, essa funcionalidade precisa ser movidos para uma implementação do [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) método e o `IDebugProgramNodeAttach2` interface não a serem implementadas.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: Msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Principais Interfaces](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)   
 [Anexar](../../../extensibility/debugger/reference/idebugengine2-attach.md)   
 [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)

