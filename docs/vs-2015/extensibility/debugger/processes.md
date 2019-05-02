---
title: Processos | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], processes
ms.assetid: a6a1efdc-b243-40c8-a778-6f69f6b018be
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 82718a7ceb7a18f9978840f35ca0c5fce5628e81
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58929420"
---
# <a name="processes"></a>Processos
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Em termos de arquitetura do depurador, uma **processo**:  
  
- É um contêiner para um conjunto de programas. Ele está estreitamente análogo a um processo do Windows, que é um contêiner para um conjunto de threads.  
  
- Pode identificar em si por nome, identificador ou identificador físico.  
  
- Pode enumerar todos os programas em execução (e seus threads).  
  
- Pode descrever em si, a porta que ele está em execução no e a máquina que o contém.  
  
- Pode criar um ou mais programas, encerrar qualquer um dos programas que ele cria ou fazer com que um programa parar.  
  
- É representado por um [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md) interface, que é criado quando o processo é iniciado. Um processo é iniciado pelo qualquer sessão Gerenciador de depuração (SDM) ou [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md).  
  
  O pacote de depuração pode anexar um mecanismo de depuração (DES) a um processo chamando [Attach](../../extensibility/debugger/reference/idebugprocess2-attach.md). Isso significa que o DE anexa a todos os programas possíveis em execução no processo que pode manipular. Por exemplo, se o common language runtime DE anexar a um processo, ele anexa somente para programas que estão executando o código gerenciado.  
  
## <a name="see-also"></a>Consulte também  
 [Programas](../../extensibility/debugger/programs.md)   
 [Threads](../../extensibility/debugger/threads.md)   
 [Conceitos do depurador](../../extensibility/debugger/debugger-concepts.md)   
 [Pacote de depuração](../../extensibility/debugger/debug-package.md)   
 [Mecanismo de depuração](../../extensibility/debugger/debug-engine.md)   
 [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)   
 [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)   
 [Anexar](../../extensibility/debugger/reference/idebugprocess2-attach.md)
