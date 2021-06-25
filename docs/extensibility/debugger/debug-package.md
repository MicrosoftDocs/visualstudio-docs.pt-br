---
title: Depurar o pacote | Microsoft Docs
description: Saiba como o pacote de depuração é executado no shell Visual Studio e lida com a interface do usuário consumindo as interfaces de depuração e comunicando-se com o gerenciador de depuração de sessão.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], packages
ms.assetid: 99947fd4-fb87-4c69-b26c-65634e17d285
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8be920ae352067a6e77593ca0a922474d68851d9
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905664"
---
# <a name="debug-package"></a>Depurar pacote
O pacote de depuração é executado no shell Visual Studio e lida com toda a interface do usuário. Ele consome as interfaces Visual Studio depuração e se comunica com o SDM (gerenciador de depuração de sessão).

 Os eventos de quebra enviados por meio do SDM alternam o depurador do modo de executar para o modo de quebra e alteram o foco para o programa em que a quebra ocorreu. O pacote de depuração rastreia o quadro de pilha e o thread das informações enviadas a ele pelos eventos.

 O pacote de depuração não tem nenhuma linguagem ou dependências de ambiente em tempo de run-time. Não é necessário implementar ou modificar o pacote de depuração.

 O pacote de depuração é implementado *porvsdebug.dll*.

## <a name="see-also"></a>Confira também
- [Gerenciador de depuração de sessão](../../extensibility/debugger/session-debug-manager.md)
- [Quadros de pilha](../../extensibility/debugger/stack-frames.md)
- [Threads](../../extensibility/debugger/threads.md)
- [Componentes do depurador](../../extensibility/debugger/debugger-components.md)
