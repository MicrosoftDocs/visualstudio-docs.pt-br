---
title: IEnumDebugCodeContexts2 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IEnumDebugCodeContexts2
helpviewer_keywords:
- IEnumDebugCodeContexts2
ms.assetid: 72915146-215f-4c99-a034-131b2b474e0e
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: dc6ff9a173bcfbb87606fe493697857d7ec2b323
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31122555"
---
# <a name="ienumdebugcodecontexts2"></a>IEnumDebugCodeContexts2
Essa interface enumera os contextos de código associados com a sessão de depuração, ou com um determinado programa ou documento.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IEnumDebugCodeContexts2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 O mecanismo de depuração (DE) implementa essa interface para representar uma lista de contextos de código para uma posição de texto específico em um programa, ou uma lista de contextos de código para um contexto de documento específico.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Chamar [EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md) para obter essa interface que representa uma lista de contextos de código para uma posição de um texto específico no documento de origem do programa.  
  
 Chamar [EnumCodeContexts](../../../extensibility/debugger/reference/idebugdocumentcontext2-enumcodecontexts.md) para obter essa interface que representa uma lista de todos os contextos de código em um documento de origem em particular.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
 A tabela a seguir mostra os métodos de `IEnumDebugCodeContexts2`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[Avançar](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-next.md)|Recupera um número especificado de contextos de código em uma sequência de enumeração.|  
|[Skip](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-skip.md)|Ignora um número especificado de contextos de código em uma sequência de enumeração.|  
|[Redefinir](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-reset.md)|Redefine uma sequência de enumeração para o início.|  
|[Clone](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-clone.md)|Cria um enumerador que contém o mesmo estado de enumeração do enumerador atual.|  
|[GetCount](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-getcount.md)|Obtém o número de contextos de código em um enumerador.|  
  
## <a name="remarks"></a>Comentários  
 Chamadas do Visual Studio [EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md) para preencher uma lista de contextos de código do usuário poderá escolher quando definir próxima instrução ou Mostrar desmontagem para um arquivo de origem. Vários contextos de código podem ocorrer, por exemplo, quando há várias instâncias de um modelo de estilo C++.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de núcleo](../../../extensibility/debugger/reference/core-interfaces.md)   
 [EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)   
 [EnumCodeContexts](../../../extensibility/debugger/reference/idebugdocumentcontext2-enumcodecontexts.md)