---
title: Processos | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], processes
ms.assetid: a6a1efdc-b243-40c8-a778-6f69f6b018be
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: df35a6e1614b558f7b94c24956e2dcdbc676a9e5
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49927132"
---
# <a name="processes"></a>Processos
Na arquitetura do depurador, uma *processo*:  
  
- É um contêiner para um conjunto de programas. Ele está estreitamente análogo a um processo do Windows, que é um contêiner para um conjunto de threads.  
  
- Pode identificar em si por nome, identificador ou identificador físico.  
  
- Pode enumerar todos os programas em execução (e seus threads).  
  
- Pode descrever em si, a porta que ele está em execução no e a máquina que o contém.  
  
- Pode criar um ou mais programas, encerrar qualquer um dos programas que ele cria ou fazer com que um programa parar.  
  
- É representado por um [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md) interface, que é criado quando o processo é iniciado. Um processo é iniciado pelo qualquer sessão Gerenciador de depuração (SDM) ou [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md).  
  
  O pacote de depuração pode anexar um mecanismo de depuração (DES) a um processo chamando [Attach](../../extensibility/debugger/reference/idebugprocess2-attach.md), que significa que o DE anexa a todos os programas possíveis em execução no processo que pode manipular. Por exemplo, se o common language runtime DE anexar a um processo, ele anexa somente para programas que estão executando o código gerenciado.  
  
## <a name="see-also"></a>Consulte também  
 [Programas](../../extensibility/debugger/programs.md)   
 [Threads](../../extensibility/debugger/threads.md)   
 [Conceitos do depurador](../../extensibility/debugger/debugger-concepts.md)   
 [Pacote de depuração](../../extensibility/debugger/debug-package.md)   
 [Mecanismo de depuração](../../extensibility/debugger/debug-engine.md)   
 [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)   
 [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)   
 [Anexar](../../extensibility/debugger/reference/idebugprocess2-attach.md)