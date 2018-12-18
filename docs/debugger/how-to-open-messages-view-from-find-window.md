---
title: 'Como: abrir o modo de exibição de mensagens da janela Localizar | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Messages View in Spy++, opening
- opening Messages View in Spy++
ms.assetid: 601a193e-432a-417b-9406-6fec9e401264
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 08f832e61bdb39bc87b59fdd64deab8cd86382a1
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49839213"
---
# <a name="how-to-open-messages-view-from-find-window"></a>Como abrir a exibição de mensagens na janela Localizar
Talvez seja conveniente usar o **localizar janela** caixa de diálogo para selecionar uma janela de destino e, em seguida, abrir um modo de exibição de mensagens dessa janela.  

### <a name="to-open-a-messages-view-window-using-the-find-window-dialog-box"></a>Para abrir uma janela de exibição de mensagens usando a caixa de diálogo Localizar janela  

1. Organize as janelas para que o Spy + + e a janela de destino estão visíveis.  

2. Dos **Spy** menu, escolha **localizar janela**.  

    O [caixa de diálogo Localizar janela](../debugger/find-window-dialog-box.md) é aberta.  

3. Dos **Windows** guia, arraste a **ferramenta Descobridora** sobre a janela de destino. À medida que você arrasta a ferramenta, o **localizar janela** caixa de diálogo exibe detalhes sobre a janela selecionada.  

   - ou –  

     Se você tiver o identificador da janela que você deseja examinar (por exemplo, copiado do depurador), você pode digitá-lo na **manipular** caixa de texto.  

4. Sob **mostram**, selecione **mensagens**.  

5. Pressione **Okey**.  

    Um espaço em branco [exibição de mensagens](../debugger/messages-view.md) janela é aberta e um **mensagens** menu é adicionado à barra de ferramentas Spy + +.  

6. Dos **mensagens** menu, escolha **opções de log**.  

    O [caixa de diálogo de opções de mensagem](../debugger/message-options-dialog-box.md) é aberta.  

7. Selecione as opções para as mensagens que você deseja exibir.  

8. Pressione **Okey** para começar a mensagens de log.  

    Dependendo das opções selecionadas, as mensagens inicia o streaming para a janela de exibição de mensagens ativa.  

9. Quando você ter mensagens suficientes, escolha **parar log** da **mensagens** menu.
