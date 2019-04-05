---
title: IEnumDebugFrameInfo2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugFrameInfo2
helpviewer_keywords:
- IEnumDebugFrameInfo2
ms.assetid: 994e30ad-435a-4f9e-9272-d96d9e01099c
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6cc6a0ff332fd6feac72ce4abf38b5319e63c913
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58922310"
---
# <a name="ienumdebugframeinfo2"></a>IEnumDebugFrameInfo2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Essa interface enumera [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) estruturas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IEnumDebugFrameInfo2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 O mecanismo de depuração (DES) implementa essa interface para fornecer uma lista de estruturas que descreve a pilha de chamadas atual.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Chamadas do Visual Studio [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) para obter essa interface sempre que um ponto de interrupção, exceção ou interrupção ocorre em um programa que está sendo depurado.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem de Vtable  
 A tabela a seguir mostra os métodos de `IEnumDebugFrameInfo2`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[Avançar](../../../extensibility/debugger/reference/ienumdebugframeinfo2-next.md)|Recupera um número especificado de [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) estruturas em uma sequência de enumeração.|  
|[Skip](../../../extensibility/debugger/reference/ienumdebugframeinfo2-skip.md)|Ignora um número especificado de [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) estruturas em uma sequência de enumeração.|  
|[Reiniciar](../../../extensibility/debugger/reference/ienumdebugframeinfo2-reset.md)|Redefine uma sequência de enumeração para o início.|  
|[Clonar](../../../extensibility/debugger/reference/ienumdebugframeinfo2-clone.md)|Cria um enumerador que contém o mesmo estado de enumeração que o enumerador atual.|  
|[GetCount](../../../extensibility/debugger/reference/ienumdebugframeinfo2-getcount.md)|Obtém o número de [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) estruturas em um enumerador.|  
  
## <a name="remarks"></a>Comentários  
 Visual Studio obtém essa interface como a primeira etapa para lidar com um ponto de interrupção, exceção ou gerados pelo usuário pausa o programa que está sendo depurado. A lista de [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) estruturas representa a pilha de chamadas atual, com a chamada de função atual no início da lista e a função mais antiga chamar no final da lista. Cada `FRAMEINFO` representa um quadro de pilha, um contexto no qual as expressões podem ser avaliadas e examinamos de variáveis locais.  
  
## <a name="requirements"></a>Requisitos  
 Header: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Principais Interfaces](../../../extensibility/debugger/reference/core-interfaces.md)   
 [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)   
 [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)
