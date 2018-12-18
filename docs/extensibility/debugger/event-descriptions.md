---
title: Descrições de eventos | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], events
ms.assetid: 09f61652-7e16-4bb0-8055-f61a84bf384e
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: afcad096b9f2991939b1378e44524c9cd83a9baf
ms.sourcegitcommit: 25a62c2db771f938e3baa658df8b1ae54a960e4f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2018
ms.locfileid: "39231028"
---
# <a name="event-descriptions"></a>Descrições de eventos
Cada tipo de evento tem uma finalidade específica.  
  
## <a name="events-and-the-reasons-for-their-use"></a>Eventos e os motivos para seu uso  
  
|evento|Descrição|  
|-----------|-----------------|  
|Ativar eventos do documento|Ocorre quando o mecanismo de depuração (DES) deseja que o IDE para abrir ou abrir um documento para o primeiro plano.|  
|Ponto de interrupção associada ou eventos de erro de ponto de interrupção|Enviado quando um ponto de interrupção está associado ou quando não é possível associar a um ponto de interrupção e um erro será retornado.|  
|Eventos de ponto de interrupção não associado|Ocorre quando um ponto de interrupção associado desvincula do código.|  
|Pode interromper eventos|Enviado para o IDE para determinar se o usuário deseja parar em um ponto especificado no código.|  
|Eventos de ponto de interrupção|Ocorra quando um ponto de interrupção de dados ou de código é atingido.|  
|Eventos de texto do documento|Ocorre quando o texto em um documento é alterado. Esses eventos não são enviados por meio de `IDebugEventCallBack2::Event` método.|  
|Criar eventos do mecanismo|Enviado quando um mecanismo é criado.|  
|Eventos de ponto de entrada|Enviado quando o programa que está sendo depurado tem executar seu código de inicialização e atingido seu primeiro ponto de entrada do usuário.|  
|Eventos de exceção|Enviado quando um programa em execução atinge uma exceção.|  
|Eventos de conclusão de avaliação de expressão|Enviado quando a avaliação da expressão assíncrona for concluída.|  
|Encontrar eventos de símbolo|Enviado sempre que o DE precisa solicitar que o usuário para localizar símbolos para um módulo.|  
|Eventos de conclusão de carga|Enviado apenas quando a carga inicial do programa for concluída e o primeiro código está prestes a ser executado no programa.|  
|Eventos de mensagem|Enviado quando as mensagens são enviadas aos usuários.|  
|Eventos de carregamento de módulo|Enviado quando um novo módulo é carregado ou descarregado.|  
|Eventos de cadeia de caracteres de saída|Enviado quando o programa grava a saída de depuração.|  
|Criar e destruir a eventos|Enviado para anunciar a criação ou destruição de threads, programas, propriedades, sessões e processos, portanto o IDE do Visual Studio pode acompanhar o estado dos programas que está sendo depurado.|  
|Eventos de conclusão da etapa|Enviado quando uma etapa for concluída.|  
|Eventos de alteração de nome de thread|Enviado quando o usuário altera o nome de um thread.|  
|Eventos de alteração de nome de programa|Enviado quando o usuário altera o nome de um programa.|  
  
## <a name="see-also"></a>Consulte também  
 [Envio de eventos](../../extensibility/debugger/sending-events.md)