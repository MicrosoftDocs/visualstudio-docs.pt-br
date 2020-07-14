---
title: Como abrir a exibição de mensagens em localizar janela | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Messages View in Spy++, opening
- opening Messages View in Spy++
ms.assetid: 601a193e-432a-417b-9406-6fec9e401264
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3258e45e47c263912957ff5066ea9d02ad03e57e
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85349478"
---
# <a name="how-to-open-messages-view-from-find-window"></a>Como abrir a exibição de mensagens na janela Localizar
Talvez você ache conveniente usar a caixa de diálogo **localizar janela** para selecionar uma janela de destino e, em seguida, abrir uma exibição de mensagens dessa janela.

### <a name="to-open-a-messages-view-window-using-the-find-window-dialog-box"></a>Para abrir uma janela de exibição de mensagens usando a caixa de diálogo localizar janela

1. Organize suas janelas para que o Spy + + e a janela de destino fiquem visíveis.

2. No menu do **Spy** , escolha **localizar janela**.

    A [caixa de diálogo localizar janela](../debugger/find-window-dialog-box.md) é aberta.

3. Na guia **Windows** , arraste a **ferramenta localizador** sobre a janela de destino. À medida que você arrasta a ferramenta, a caixa de diálogo **localizar janela** exibe detalhes na janela selecionada.

   - ou –

     Se você tiver o identificador da janela que deseja examinar (por exemplo, copiado do depurador), você poderá digitá-lo na caixa de texto **identificador** .

4. Em **Mostrar**, selecione **mensagens**.

5. Pressione **OK**.

    Uma janela [Exibir mensagens](../debugger/messages-view.md) em branco é aberta e um menu **mensagens** é adicionado à barra de ferramentas do Spy + +.

6. No menu **mensagens** , escolha **Opções de log**.

    A [caixa de diálogo opções de mensagem](../debugger/message-options-dialog-box.md) é aberta.

7. Selecione as opções para as mensagens que você deseja exibir.

8. Pressione **OK** para iniciar o log de mensagens.

    Dependendo das opções selecionadas, as mensagens começam a ser transmitidas para a janela de exibição de mensagens ativas.

9. Quando você tiver mensagens suficientes, escolha **parar o registro em log** no menu **mensagens** .
