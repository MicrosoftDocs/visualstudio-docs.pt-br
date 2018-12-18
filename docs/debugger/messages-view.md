---
title: A exibição de mensagens | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.externaltools.spyplus.messagesview
helpviewer_keywords:
- Messages view
ms.assetid: 14c2a786-c23a-4b2d-acad-8c32a856c70d
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 31baccc88b25979dfc92fed6217bec3b0ef16a55
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31477073"
---
# <a name="messages-view"></a>Exibição de mensagens
Cada janela tem um fluxo de mensagem associado. Uma janela de exibição de mensagens exibe este fluxo de mensagem. O identificador de janela, o código de mensagem e a mensagem são mostrados. Você pode criar um modo de exibição de mensagens para um thread ou processo. Isso permite que você exiba as mensagens enviadas a todos os windows pertencentes a um processo específico ou thread, que é particularmente útil para a captura de mensagens de inicialização de janela.  
  
 Uma janela de exibição de mensagens típica é exibida abaixo. Observe que a primeira coluna contém o identificador de janela, e a segunda coluna contém um código de mensagem (explicado em [códigos de mensagem](../debugger/message-codes.md)). Mensagem decodificada parâmetros e valores de retorno são à direita.  
  
 ![Spy&#43; &#43; a exibição de mensagens](../debugger/media/spy--_messagesview.png "Spy + + _MessagesView")  
Exibição de mensagens do Spy + +  
  
## <a name="procedures"></a>Procedimentos  
  
#### <a name="to-open-a-messages-view-for-a-window-process-or-thread"></a>Para abrir um modo de exibição de mensagens de janela, processo ou thread  
  
1.  Mover o foco para um [exibição Windows](../debugger/windows-view.md), [exibição processos](../debugger/processes-view.md), ou [exibição de Threads](../debugger/threads-view.md) janela.  
  
2.  Localizar o nó para o item cujas mensagens que você deseja examinar e selecioná-lo.  
  
3.  Do **Spy** menu, escolha **mensagens de Log**.  
  
     O [caixa de diálogo de opções de mensagem](../debugger/message-options-dialog-box.md) é aberto.  
  
4.  Selecione as opções para a mensagem que você deseja exibir.  
  
5.  Pressione **Okey** para começar a mensagens de log.  
  
     Um mensagens de janela de exibição é aberto e um **mensagens** menu é adicionado à barra de ferramentas Spy + +. Dependendo das opções selecionadas, mensagens iniciar streaming na janela de exibição de mensagens ativa.  
  
6.  Quando você tem suficiente mensagens, escolha **parar log** do **mensagens** menu.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Controlando a exibição de mensagens](../debugger/how-to-control-messages-view.md)  
 Explica como gerenciar a exibição de mensagens.  
  
 [Abrir modo de exibição de mensagens na janela Localizar](../debugger/how-to-open-messages-view-from-find-window.md)  
 Explica como abrir a exibição de mensagens na caixa de diálogo Localizar janela.  
  
 [Procurando uma mensagem na exibição de mensagens](../debugger/how-to-search-for-a-message-in-messages-view.md)  
 Explica como localizar uma mensagem específica no modo de exibição de mensagens.  
  
 [Iniciar e interromper a exibição de mensagem de Log](../debugger/how-to-start-and-stop-the-message-log-display.md)  
 Explica como iniciar e parar o log de mensagem.  
  
 [Códigos de mensagem](../debugger/message-codes.md)  
 Define os códigos para as mensagens listadas na exibição de mensagens.  
  
 [Exibindo propriedades de mensagem](../debugger/how-to-display-message-properties.md)  
 Como mostrar mais informações sobre a mensagem.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Exibições do Spy++](../debugger/spy-increment-views.md)  
 Explica as exibições de árvore do Spy + + do windows, as mensagens, processos e threads.  
  
 [Usando Spy++](../debugger/using-spy-increment.md)  
 Apresenta a ferramenta Spy + + e explica como ele pode ser usado.  
  
 [Caixa de diálogo Opções de Mensagem](../debugger/message-options-dialog-box.md)  
 Usado para selecionar quais mensagens são listadas na exibição de mensagens ativa.  
  
 [Caixa de diálogo Pesquisa de Mensagens](../debugger/message-search-dialog-box.md)  
 Usado para localizar o nó de uma mensagem específica no modo de exibição de mensagens.  
  
 [Caixa de diálogo Propriedades da Mensagem](../debugger/message-properties-dialog-box.md)  
 Usado para exibir as propriedades de uma mensagem selecionada na exibição de mensagem.  
  
 [Referência a Spy++](../debugger/spy-increment-reference.md)  
 Inclui as seções que descrevem cada Spy + + menu e a caixa de diálogo caixa.