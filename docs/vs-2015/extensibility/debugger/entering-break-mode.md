---
title: Entrar no modo de interrupção | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- break mode
- debugging [Debugging SDK], entering break mode
ms.assetid: e9a8a241-cd21-4d4e-999a-283554c288b1
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c4251779593e237713258fd54c80dcb311ce4b80
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68182245"
---
# <a name="entering-break-mode"></a>Entrando no modo de interrupção
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

O exemplo a seguir descreve o processo que ocorre quando um ponto de interrupção é encontrado depois de entrar em uma função, em execução para a linha de código-fonte que contém o cursor de ou em execução para um ponto de interrupção.  
  
## <a name="break-mode-process"></a>Processo do modo de interrupção  
  
1. O mecanismo de depuração (DES) envia [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md), [IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md), ou qualquer outro evento de interrupção para fazer com que o IDE entrar no modo de interrupção.  
  
2. O SDM obtém as informações de pilha de chamadas do thread, da seguinte maneira:  
  
    - [IDebugThread2::EnumFrameInfo](../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)  
  
    - [IEnumDebugFrameInfo2::GetCount](../../extensibility/debugger/reference/ienumdebugframeinfo2-getcount.md)  
  
    - [IEnumDebugFrameInfo2::Next](../../extensibility/debugger/reference/ienumdebugframeinfo2-next.md)  
  
    - [IDebugStackFrame2::GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md) para obter as informações de código fonte  
  
    - [IDebugDocumentContext2::GetName](../../extensibility/debugger/reference/idebugdocumentcontext2-getname.md) para obter o nome do arquivo  
  
    - [IDebugDocumentContext2::GetStatementRange](../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md) obter o intervalo de instrução  
  
    - [IDebugStackFrame2::GetCodeContext](../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md) para obter informações de memória  
  
## <a name="see-also"></a>Consulte também  
 [Chamar eventos do depurador](../../extensibility/debugger/calling-debugger-events.md)
