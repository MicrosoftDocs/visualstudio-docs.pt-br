---
title: Enviando eventos | Microsoft Docs
description: Saiba como o depurador e o mecanismo de depuração usam um modelo de evento baseado no DCOM. Os eventos são enviados como objetos COM.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], sending events
ms.assetid: 064231e7-59b5-4437-8240-a23c0a7ec2a9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6e9af2618150df522a459e47f312c1dc1e6a220c
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902248"
---
# <a name="send-events"></a>Enviar eventos
O mecanismo de comunicação entre o depurador e o mecanismo DE depuração (DE) é um modelo de evento baseado no DCOM. Os eventos são enviados como objetos COM e cada evento tem parâmetros que especificam:

- O que chamou o evento.

- Uma descrição do que aconteceu.

- As informações de processo, programa e thread que identificam o contexto de onde o evento ocorreu. O processo não é enviado para eventos enviados de um DE.

- O tipo de evento que indica se o evento é síncrono ou assíncrono.

  Todos os eventos de depuração são enviados usando o método [IDebugEventCallback2:: Event](../../extensibility/debugger/reference/idebugeventcallback2-event.md).

## <a name="in-this-section"></a>Nesta seção
 [Origens do evento](../../extensibility/debugger/event-sources-visual-studio-sdk.md) Explica as duas fontes de eventos: o mecanismo de depuração (DE) e o SDM (Gerenciador de depuração de sessão).

 [Tipos de eventos com suporte](../../extensibility/debugger/supported-event-types.md) Discute os tipos de evento com suporte no momento: assíncrono e síncrono.

 [Descrições de eventos](../../extensibility/debugger/event-descriptions.md) Define eventos e os motivos para seu uso.

## <a name="related-sections"></a>Seções relacionadas
 [Criando um mecanismo de depuração personalizado](../../extensibility/debugger/creating-a-custom-debug-engine.md) Descreve como um DE funciona com o interpretador ou o sistema operacional para fornecer serviços de depuração.
