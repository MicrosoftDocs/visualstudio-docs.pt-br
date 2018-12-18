---
title: Envio de eventos | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], sending events
ms.assetid: 064231e7-59b5-4437-8240-a23c0a7ec2a9
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 369a2aa92c47c4db7b1036097ffb49f6d8de8a14
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49895412"
---
# <a name="send-events"></a>Enviar eventos
O mecanismo de comunicação entre o depurador e o mecanismo de depuração (DES) é um modelo de evento com base no DCOM. Os eventos são enviados como objetos COM, e cada evento tem parâmetros que especificam:  
  
- O DE que o evento de chamada.  
  
- Uma descrição do que aconteceu.  
  
- O processo, programa e informações de thread que identifica o contexto de onde o evento ocorreu. O processo não é enviado para eventos enviados a partir DE.  
  
- O tipo de evento que indica se o evento é síncrona ou assíncrona.  
  
  Todos os eventos de depuração são enviados usando o método [IDebugEventCallback2::Event](../../extensibility/debugger/reference/idebugeventcallback2-event.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Fontes de evento](../../extensibility/debugger/event-sources-visual-studio-sdk.md)  
 Explica as duas fontes de eventos: o mecanismo de depuração (DE) e a sessão de depuração do SDM (Gerenciador).  
  
 [Tipos de eventos com suporte](../../extensibility/debugger/supported-event-types.md)  
 Discute os tipos de eventos com suporte no momento: síncrono e assíncrono.  
  
 [Descrições de eventos](../../extensibility/debugger/event-descriptions.md)  
 Define os eventos e os motivos para seu uso.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Criando um mecanismo de depuração personalizado](../../extensibility/debugger/creating-a-custom-debug-engine.md)  
 Descreve como a DE funciona com o sistema operacional ou interpretador para fornecer serviços de depuração.