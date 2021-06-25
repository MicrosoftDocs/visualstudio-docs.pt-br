---
title: Descrições de evento | Microsoft Docs
description: Saiba mais sobre os tipos de eventos e os motivos para seu uso. Cada tipo de evento tem uma finalidade específica.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], events
ms.assetid: 09f61652-7e16-4bb0-8055-f61a84bf384e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ee2eedac924b3bbd58fac6980da9151a88da9196
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902638"
---
# <a name="event-descriptions"></a>Descrições de eventos
Cada tipo de evento tem uma finalidade específica.

## <a name="events-and-the-reasons-for-their-use"></a>Eventos e os motivos para seu uso

|Evento|Descrição|
|-----------|-----------------|
|Ativar eventos de documento|Ocorre quando o mecanismo de depuração (DE) deseja que o IDE abra ou traga um documento para o primeiro plano.|
|Eventos de erro de ponto de interrupção ou vinculados|Enviado quando um ponto de interrupção é associado ou quando um ponto de interrupção não pode ser ligado e um erro é retornado.|
|Eventos não associados de ponto de interrupção|Ocorre quando um ponto de interrupção associado é desassociado do código.|
|Pode parar eventos|Enviado ao IDE para determinar se o usuário deseja parar em um ponto especificado no código.|
|Eventos de ponto de interrupção|Ocorre quando um ponto de interrupção de código ou de dados é atingido.|
|Eventos de texto do documento|Ocorre quando o texto em um documento é alterado. Esses eventos não são enviados por meio do `IDebugEventCallBack2::Event` método.|
|Eventos de criação de mecanismo|Enviado quando um mecanismo é criado pela primeira vez.|
|Eventos de ponto de entrada|Enviado quando o programa que está sendo depurado executa seu código de inicialização e atingiu seu primeiro ponto de entrada de usuário.|
|Eventos de exceção|Enviado quando um programa em execução atinge uma exceção.|
|Eventos de avaliação de expressão concluída|Enviado quando a avaliação de expressão assíncrona é concluída.|
|Localizar eventos de símbolo|Enviado sempre que for necessário solicitar ao usuário que encontre símbolos para um módulo.|
|Carregar eventos completos|Enviado somente quando a carga inicial do programa for concluída e o primeiro código estiver prestes a ser executado no programa.|
|Eventos de mensagem|Enviado quando as mensagens são enviadas aos usuários.|
|Eventos de carregamento de módulo|Enviado quando um novo módulo é carregado ou descarregado.|
|Eventos de cadeia de caracteres de saída|Enviado quando o programa grava a saída de depuração.|
|Criar e destruir eventos|Enviado para anunciar a criação ou destruição de processos, programas, propriedades, sessões e threads para que o IDE do Visual Studio possa acompanhar o estado dos programas que estão sendo depurados.|
|Eventos de conclusão de etapa|Enviado quando uma etapa é concluída.|
|Eventos de alteração de nome de thread|Enviado quando o usuário altera o nome de um thread.|
|Eventos de alteração do nome do programa|Enviado quando o usuário altera o nome de um programa.|

## <a name="see-also"></a>Confira também
- [Enviando eventos](../../extensibility/debugger/sending-events.md)
