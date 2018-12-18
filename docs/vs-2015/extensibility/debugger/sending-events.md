---
title: Envio de eventos | Microsoft Docs
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
- debugging [Debugging SDK], sending events
ms.assetid: 064231e7-59b5-4437-8240-a23c0a7ec2a9
caps.latest.revision: 8
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 9099cfe070f3c572823f8aa07a51e4456190f7b6
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51749437"
---
# <a name="sending-events"></a>Enviando eventos
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

O mecanismo de comunicação entre o depurador e o mecanismo de depuração (DES) é um modelo de evento com base no DCOM. Os eventos são enviados como objetos COM, e cada evento tem parâmetros que especificam o seguinte:  
  
- O DE que o evento de chamada.  
  
- Uma descrição do que aconteceu.  
  
- O processo, programa e informações de thread que identifica o contexto de onde o evento ocorreu. O processo não é enviado para eventos enviados a partir DE.  
  
- O tipo de evento que indica se o evento é síncrona ou assíncrona.  
  
  Todos os eventos de depuração são enviados usando o método [IDebugEventCallback2::Event](../../extensibility/debugger/reference/idebugeventcallback2-event.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Event Sources](../../extensibility/debugger/event-sources-visual-studio-sdk.md)  
 Explica as duas fontes de eventos: o mecanismo de depuração (DE) e a sessão de depuração do SDM (Gerenciador).  
  
 [Tipos de eventos com suporte](../../extensibility/debugger/supported-event-types.md)  
 Discute os tipos de eventos com suporte no momento: síncrono e assíncrono.  
  
 [Descrição do evento](../../extensibility/debugger/event-descriptions.md)  
 Define os eventos e os motivos para seu uso.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Criar um mecanismo de depuração personalizado](../../extensibility/debugger/creating-a-custom-debug-engine.md)  
 Descreve como a DE funciona com o sistema operacional ou interpretador para fornecer serviços de depuração.

