---
title: Enviar eventos de inicialização após uma inicialização | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- debugging [Debugging SDK], startup events
ms.assetid: 306ea0b4-6d9e-4871-8d8d-a4032d422940
caps.latest.revision: 10
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 0cc0642c085510e69fe7cd16abe195095c993219
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51769125"
---
# <a name="sending-startup-events-after-a-launch"></a>Enviado eventos de inicialização após uma inicialização
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Depois que o mecanismo de depuração (DES) é anexado ao programa, ele envia uma série de eventos de inicialização para a sessão de depuração.  
  
 Eventos de inicialização enviados de volta para a sessão de depuração incluem o seguinte:  
  
- Um evento de criação de mecanismo.  
  
- Um evento de criação do programa.  
  
- Thread de criação e eventos de carregamento de módulo.  
  
- Um evento de conclusão de carga, enviado quando o código é carregado e pronto para ser executado, mas antes de qualquer código é executado  
  
  > [!NOTE]
  >  Quando esse evento é continuado, variáveis globais são inicializadas e executar rotinas de inicialização.  
  
- Possível que outros threads criação e eventos de carregamento de módulo.  
  
- Um evento de ponto de entrada, que sinaliza que o programa atingiu seu ponto de entrada principal, como **principal** ou `WinMain`. Esse evento não é enviado normalmente se o DE anexar a um programa que já está em execução.  
  
  O DE forma programática, primeiro o Gerenciador de sessão de depuração (SDM) envia uma [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) interface, que representa um evento de criação de mecanismo, seguido por um [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) , que representa um evento de criação do programa.  
  
  Isso é normalmente seguido por um ou mais [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md) eventos de criação de thread e [IDebugModuleLoadEvent2](../../extensibility/debugger/reference/idebugmoduleloadevent2.md) eventos de carregamento de módulo.  
  
  Quando o código é carregado e pronto para ser executado, mas antes de qualquer código é executado, o DE envia o SDM uma [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) evento de conclusão de carga. Por fim, se o programa não estiver sendo executado, o DE envia um [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) evento de ponto de entrada, sinalizando que o programa tiver atingido seu ponto de entrada principal e está pronto para depuração.  
  
## <a name="see-also"></a>Consulte também  
 [Controle de execução](../../extensibility/debugger/control-of-execution.md)   
 [Tarefas de depuração](../../extensibility/debugger/debugging-tasks.md)

