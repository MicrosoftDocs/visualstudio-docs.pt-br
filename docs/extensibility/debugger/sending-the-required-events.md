---
title: Enviando os eventos necessários | Microsoft Docs
description: Saiba mais sobre os eventos ordenados necessários ao criar um mecanismo de depuração e anexá-lo a um programa no Visual Studio depuração.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debugging [Debugging SDK], required events
ms.assetid: 08319157-43fb-44a9-9a63-50b919fe1377
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b04ca7ed68b975bc68fa509cdc75dc507b9603d6
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902261"
---
# <a name="send-the-required-events"></a>Enviar os eventos necessários
Use este procedimento para enviar eventos necessários.

## <a name="process-for-sending-required-events"></a>Processo para enviar eventos necessários
 Os seguintes eventos são necessários, nesta ordem, ao criar um DE (mecanismo de depuração) e anexá-lo a um programa:

1. Envie um objeto de evento [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) para o SDM (gerenciador de depuração de sessão) quando o DE for inicializado para depurar um ou mais programas em um processo.

2. Quando o programa a ser depurado estiver anexado, envie um objeto de evento [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) para o SDM. Esse evento pode ser um evento de interrupção, dependendo do design do mecanismo.

3. Se o programa estiver anexado ao quando o processo for lançado, envie um objeto de evento [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md) para o SDM para notificar o IDE do novo thread. Esse evento pode ser um evento de interrupção, dependendo do design do mecanismo.

4. Envie um objeto de evento [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) para o SDM quando o programa que está sendo depurado terminar de ser carregado ou quando a anexação ao programa for concluída. Esse evento deve ser um evento de interrupção.

5. Se o aplicativo a ser depurado for lançado, envie um objeto de evento [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) para o SDM quando a primeira instrução de código na arquitetura de tempo de execução estiver prestes a ser executada. Esse evento é sempre um evento de interrupção. Ao entrar na sessão de depuração, o IDE para neste evento.

> [!NOTE]
> Muitas linguagens usam inicializadores globais ou funções pré-comcompiladas externas (da biblioteca CRT ou _Main) no início do código. Se o idioma do programa que você está depurando contiver qualquer um desses tipos de elementos antes do ponto de entrada inicial, esse código será executado e o evento de ponto de entrada será enviado quando o ponto de entrada do usuário, como **main** ou , for `WinMain` atingido.

## <a name="see-also"></a>Confira também
- [Habilitando um programa a ser depurado](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
