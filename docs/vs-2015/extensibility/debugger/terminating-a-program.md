---
title: Encerrar um programa | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- programs, termination events
- debugging [Debugging SDK], terminating a program
ms.assetid: eedda0a3-5e05-44fe-841d-a2f4866ac72d
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f0b9ad248751af0885fa4edc0275be2ede5ddd9f
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58923765"
---
# <a name="terminating-a-program"></a>Terminando um programa
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

A seguir está uma descrição do encerramento de um único programa com um thread.  
  
## <a name="termination-process"></a>Processo de encerramento  
  
1. O envia DE um [IDebugThreadDestroyEvent2](../../extensibility/debugger/reference/idebugthreaddestroyevent2.md) com uma validade [IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md).  
  
2. O envia DE um [IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) com uma validade [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md).  
  
   O IDE entra no modo de design. O mecanismo de depuração ou o ambiente de tempo de execução chama [IDebugPortNotify2::RemoveProgramNode](../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md) para remover o programa da porta.  
  
## <a name="see-also"></a>Consulte também  
 [Chamar eventos do depurador](../../extensibility/debugger/calling-debugger-events.md)
