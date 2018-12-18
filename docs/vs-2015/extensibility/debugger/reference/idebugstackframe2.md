---
title: IDebugStackFrame2 | Microsoft Docs
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
- IDebugStackFrame2
helpviewer_keywords:
- IDebugStackFrame2 interface
ms.assetid: bd212a6a-dcc6-4756-a77a-e8dfda38b104
caps.latest.revision: 15
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: bc6a6ea1b1d864c3f14158b9687181e6bdb6bc4a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51816653"
---
# <a name="idebugstackframe2"></a>IDebugStackFrame2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Essa interface representa um quadro de pilha única em uma pilha de chamadas em um thread específico.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugStackFrame2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 O mecanismo de depuração (DES) implementa essa interface para representar um quadro de pilha.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Chame [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) para recuperar um [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md) interface. Chame [próxima](../../../extensibility/debugger/reference/ienumdebugframeinfo2-next.md) para recuperar um [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) estrutura que contém o `IDebugStackFrame2` interface.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem de Vtable  
 A tabela a seguir mostra os métodos de `IDebugStackFrame2`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)|Obtém o contexto de código para este registro de ativação.|  
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)|Obtém o contexto do documento para este registro de ativação.|  
|[GetName](../../../extensibility/debugger/reference/idebugstackframe2-getname.md)|Obtém o nome do quadro de pilha.|  
|[GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)|Obtém uma descrição do quadro de pilha.|  
|[GetPhysicalStackRange](../../../extensibility/debugger/reference/idebugstackframe2-getphysicalstackrange.md)|Obtém uma representação depende do computador do intervalo de endereços físicos associados a um quadro de pilha.|  
|[GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)|Obtém um contexto de avaliação para fazer a avaliação da expressão dentro do contexto atual de um quadro de pilha e thread.|  
|[GetLanguageInfo](../../../extensibility/debugger/reference/idebugstackframe2-getlanguageinfo.md)|Obtém o idioma associado a um quadro de pilha.|  
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)|Obtém uma descrição das propriedades associadas com um quadro de pilha.|  
|[EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)|Cria um enumerador para a pilha de propriedades do quadro.|  
|[GetThread](../../../extensibility/debugger/reference/idebugstackframe2-getthread.md)|Obtém o thread associado a um quadro de pilha.|  
  
## <a name="remarks"></a>Comentários  
 Essa interface é obtida somente quando o programa que está sendo depurado foi interrompido no ponto de interrupção (seja causada por um ponto de interrupção definido pelo usuário ou uma exceção). Nessa interface, um contexto de expressão pode ser obtido para avaliar expressões, uma lista de registros pode ser retornada ou a pilha de chamadas pode ser obtida e examinada.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Principais interfaces](../../../extensibility/debugger/reference/core-interfaces.md)

