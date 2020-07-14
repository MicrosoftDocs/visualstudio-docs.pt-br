---
title: Como pesquisar uma mensagem no modo de exibição de mensagens | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Message Search dialog box
- Messages view
- messages, searching for
ms.assetid: 732b7ccc-54ea-41db-823b-2b96e3e4083e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7145732ef635d550aa883603b0f56090eb6d1278
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85349309"
---
# <a name="how-to-search-for-a-message-in-messages-view"></a>Como procurar uma mensagem na exibição de mensagens
Você pode pesquisar uma mensagem específica no modo de exibição de mensagens usando seu identificador, tipo ou ID de mensagem como critério de pesquisa. Qualquer um desses — ou uma combinação — será um critério de pesquisa válido. A direção inicial da pesquisa também pode ser especificada. Os campos na caixa de diálogo são pré-carregados com os atributos da mensagem selecionada no momento.

### <a name="to-search-for-a-message-in-messages-view"></a>Para procurar uma mensagem no modo de exibição de mensagens

1. Organize suas janelas para que o Spy + + e uma janela de [exibição de mensagens](../debugger/messages-view.md) ativas fiquem visíveis.

2. No menu **Pesquisar** , escolha **Localizar mensagem**.

    A [caixa de diálogo pesquisa de mensagem](../debugger/message-search-dialog-box.md) é aberta.

3. Arraste a **ferramenta localizador** sobre a janela desejada. À medida que você arrasta a ferramenta, a caixa de diálogo **pesquisa de mensagem** exibe detalhes na janela selecionada.

   - ou –

     Se você tiver o identificador da janela cujas mensagens deseja examinar, digite-a na caixa de texto **identificador** .

   - ou –

     Se você souber o tipo de mensagem e/ou a ID da mensagem que deseja, selecione-os nos menus suspensos **tipo** e **mensagem** e desmarque a caixa de texto **identificador** .

4. Desmarque os campos para os quais você não deseja especificar valores.

   > [!TIP]
   > Para reduzir a desordem na tela, selecione a opção **ocultar Spy** . Essa opção oculta a janela principal do Spy + +, deixando apenas a caixa de diálogo **localizar janela** visível sobre seus outros aplicativos. A janela principal Spy + + é restaurada quando você clica em **OK** ou em **Cancelar**, ou quando você desmarca a opção **ocultar Spy + +** .

5. Escolha para **cima** ou para **baixo** na direção inicial da pesquisa.

6. Clique em **OK**.

   Se uma mensagem correspondente for encontrada, ela será realçada na janela exibição de mensagens. Consulte a [exibição de mensagens](../debugger/messages-view.md).