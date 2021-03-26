---
title: Enviando os eventos necessários | Microsoft Docs
description: Saiba mais sobre os eventos ordenados que são necessários ao criar um mecanismo de depuração e anexá-lo a um programa na depuração do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], required events
ms.assetid: 08319157-43fb-44a9-9a63-50b919fe1377
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a53f4d7a89b1f5902f576490d827148e9fb816bf
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070369"
---
# <a name="send-the-required-events"></a>Enviar os eventos necessários
Use este procedimento para enviar os eventos necessários.

## <a name="process-for-sending-required-events"></a>Processo para enviar os eventos necessários
 Os eventos a seguir são necessários, nesta ordem, ao criar um mecanismo DE depuração (DE) e anexá-lo a um programa:

1. Envie um objeto de evento [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) para o SDM (Gerenciador de depuração de sessão) quando o de for inicializado para depurar um ou mais programas em um processo.

2. Quando o programa a ser depurado é anexado a, envie um objeto de evento [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) para o SDM. Esse evento pode ser um evento de interrupção, dependendo do design do seu mecanismo.

3. Se o programa estiver anexado ao quando o processo for iniciado, envie um objeto de evento [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md) para o SDM para notificar o IDE do novo thread. Esse evento pode ser um evento de interrupção, dependendo do design do seu mecanismo.

4. Envie um objeto de evento [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) para o SDM quando o programa que está sendo depurado terminar de ser carregado ou quando a anexação ao programa for concluída. Esse evento deve ser um evento de parada.

5. Se o aplicativo a ser depurado for iniciado, envie um objeto de evento [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) para o SDM quando a primeira instrução de código na arquitetura de tempo de execução estiver prestes a ser executada. Esse evento é sempre um evento de interrupção. Ao passar para a sessão de depuração, o IDE é interrompido nesse evento.

> [!NOTE]
> Muitas linguagens usam inicializadores globais ou funções pré-compiladas externas (da biblioteca CRT ou _Main) no início do código. Se o idioma do programa que você está depurando contiver qualquer um desses tipos de elementos antes do ponto de entrada inicial, esse código será executado e o evento de ponto de entrada será enviado quando o ponto de entrada do usuário, como **Main** ou `WinMain` , for atingido.

## <a name="see-also"></a>Confira também
- [Habilitando um programa a ser depurado](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
