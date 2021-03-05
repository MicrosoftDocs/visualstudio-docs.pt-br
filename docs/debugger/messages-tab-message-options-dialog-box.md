---
description: Use a guia mensagens para selecionar os tipos de mensagem a serem listados no modo de exibição de mensagens) e para especificar os critérios de pesquisa de mensagens.
title: Guia mensagens, caixa de diálogo opções de mensagem | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- message options, Messages
ms.assetid: fb9fa211-e82c-40a5-9e4b-ba8de07313c0
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 66c1abcedbf48e8cd80aeafe0c4a5def1ddbb9eb
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102160362"
---
# <a name="messages-tab-message-options-dialog-box"></a>Guia Mensagens, Caixa de diálogo Opções da Mensagem
Use a guia **mensagens** para selecionar os tipos de mensagem a serem listados no [modo de exibição de mensagens](../debugger/messages-view.md)e para especificar os critérios de pesquisa de mensagens. Para exibir a [caixa de diálogo opções de mensagem](../debugger/message-options-dialog-box.md), escolha **registrar mensagens** no menu do **Spy** .

 Normalmente, primeiro você seleciona **grupos de mensagens** e, em seguida, ajusta a seleção selecionando **as mensagens individuais a serem exibidas**. O botão **tudo** seleciona todos os tipos de mensagem e o botão **nenhum** limpa todos os tipos.

 As configurações a seguir estão disponíveis na guia **mensagens** :

 **Mensagens a serem exibidas** Selecione mensagens específicas para exibição. Quando você cria uma nova janela de mensagens, ela pode exibir todas as mensagens. Quando você filtra mensagens da guia **mensagens** , esse filtro se aplica somente a novas mensagens, não a mensagens que já foram exibidas no modo de exibição do Windows.

 **Grupos de mensagens** Selecione grupos de mensagens para exibição. Os grupos disponíveis incluem:

- WM_USER: com um código maior ou igual a WM_USER

- Registrado: registrado com a chamada **RegisterWindowMessage**

- Desconhecido: mensagens desconhecidas no intervalo de 0 a (WM_USER-1)

  Observe que esses **grupos de mensagens** não são mapeados para entradas específicas em **mensagens a serem exibidas**. Quando você seleciona um grupo, a seleção é aplicada diretamente ao fluxo de mensagens.

  Uma caixa de seleção cinza em **grupos de mensagens** indica que a caixa de listagem **mensagens a serem exibidas** foi modificada para mensagens nesse grupo; Nem todos os tipos de mensagem nesse grupo são selecionados.

  **Salvar configurações como padrão** Salve as configurações atuais para uso posterior como opções de pesquisa de mensagens. Essas configurações também são salvas ao sair do Spy + +.
