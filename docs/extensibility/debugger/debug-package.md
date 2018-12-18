---
title: Depurar pacote | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], packages
ms.assetid: 99947fd4-fb87-4c69-b26c-65634e17d285
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 04eb6802cabd4ae36151580c573d28b977ca348e
ms.sourcegitcommit: 36835f1b3ec004829d6aedf01938494465587436
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2018
ms.locfileid: "39204038"
---
# <a name="debug-package"></a>Pacote de depuração
O pacote de depuração é executado no shell do Visual Studio e manipula toda a interface do usuário. Ele consome as interfaces de depuração do Visual Studio e se comunica com o Gerenciador de sessão de depuração (SDM).  
  
 Eventos de interrupção enviados por meio do SDM alternar o depurador do modo de execução para o modo de interrupção e altere o foco para o programa onde a quebra ocorreu. O pacote de depuração acompanha o quadro de pilha e o thread a partir das informações enviadas a ele pelos eventos.  
  
 O pacote de depuração não tem idioma ou as dependências do ambiente de tempo de execução. Não é necessário implementar ou modificar o pacote de depuração.  
  
 O pacote de depuração é implementado pelo *vsdebug.dll*.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciador de sessão de depuração](../../extensibility/debugger/session-debug-manager.md)   
 [Quadros de pilha](../../extensibility/debugger/stack-frames.md)   
 [Threads](../../extensibility/debugger/threads.md)   
 [Componentes do depurador](../../extensibility/debugger/debugger-components.md)