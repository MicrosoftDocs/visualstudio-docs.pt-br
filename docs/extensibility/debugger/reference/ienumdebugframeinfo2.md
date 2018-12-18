---
title: IEnumDebugFrameInfo2 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IEnumDebugFrameInfo2
helpviewer_keywords:
- IEnumDebugFrameInfo2
ms.assetid: 994e30ad-435a-4f9e-9272-d96d9e01099c
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 858250c3c951880cf905ea6ee150f1ff61008204
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31123912"
---
# <a name="ienumdebugframeinfo2"></a>IEnumDebugFrameInfo2
Essa interface enumera [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) estruturas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IEnumDebugFrameInfo2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 O mecanismo de depuração (DE) implementa essa interface para fornecer uma lista de estruturas que descreve a pilha de chamadas atual.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Chamadas do Visual Studio [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) para obter essa interface sempre que um ponto de interrupção, interrupção ou exceção ocorre em um programa que está sendo depurado.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
 A tabela a seguir mostra os métodos de `IEnumDebugFrameInfo2`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[Avançar](../../../extensibility/debugger/reference/ienumdebugframeinfo2-next.md)|Recupera um número especificado de [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) estruturas em uma sequência de enumeração.|  
|[Skip](../../../extensibility/debugger/reference/ienumdebugframeinfo2-skip.md)|Ignora um número especificado de [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) estruturas em uma sequência de enumeração.|  
|[Redefinir](../../../extensibility/debugger/reference/ienumdebugframeinfo2-reset.md)|Redefine uma sequência de enumeração para o início.|  
|[Clone](../../../extensibility/debugger/reference/ienumdebugframeinfo2-clone.md)|Cria um enumerador que contém o mesmo estado de enumeração do enumerador atual.|  
|[GetCount](../../../extensibility/debugger/reference/ienumdebugframeinfo2-getcount.md)|Obtém o número de [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) estruturas em um enumerador.|  
  
## <a name="remarks"></a>Comentários  
 O Visual Studio obtém essa interface como a primeira etapa para lidar com um ponto de interrupção, exceção ou gerados pelo usuário pausar sobre o programa que está sendo depurado. A lista de [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) estruturas representa a pilha de chamadas atual, com a chamada de função atual no início da lista e a função mais antiga de chamadas no final da lista. Cada `FRAMEINFO` representa um quadro de pilha, um contexto no qual as expressões podem ser avaliadas e analisamos as variáveis locais.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de núcleo](../../../extensibility/debugger/reference/core-interfaces.md)   
 [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)   
 [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)