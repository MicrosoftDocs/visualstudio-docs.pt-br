---
title: 'Etapa 5: adicionar referências de rótulo | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d418350c-0396-494e-8149-71fa61b395c5
caps.latest.revision: 22
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 829911bc2f08010b9e0d3d9c710862097720d4df
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49285216"
---
# <a name="step-5-add-label-references"></a>Etapa 5: Adicionar referências de rótulo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O programa precisa rastrear quais controles de rótulo o jogador escolhe. Atualmente, o programa mostra todos os rótulos escolhidos pelo jogador. Mas isso será alterado. Depois que o primeiro rótulo é escolhido, o programa deve mostrar o ícone do rótulo. Depois que o segundo rótulo é escolhido, o programa deve exibir ambos os ícones por um breve momento e depois ocultá-los novamente. Agora seu programa rastreará qual controle de rótulo será escolhido primeiro e qual será escolhido em segundo usando *variáveis de referência*.  
  
### <a name="to-add-label-references"></a>Para adicionar referências de rótulo  
  
1.  Adicione referências de rótulo ao seu formulário usando o código a seguir.  
  
     [!code-csharp[VbExpressTutorial4Step5#5](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step5/cs/form1.cs#5)]
     [!code-vb[VbExpressTutorial4Step5#5](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step5/vb/form1.vb#5)]  
  
     Essas variáveis de referência parecem semelhantes às instruções que você usou anteriormente para adicionar objetos (como os objetos `Timer`, `List` e `Random`) ao formulário. No entanto, essas instruções não fazem com que os dois controles de rótulo extras apareçam no formulário, pois a palavra-chave `new` não foi usada em nenhuma das duas instruções. Sem a palavra-chave `new`, nenhum objeto é criado. Por esse motivo `firstClicked` e `secondClicked` são chamadas de variáveis de referência: elas rastreiam (ou fazem referência a) os objetos `Label`.  
  
     Quando uma variável não estiver rastreando um objeto, ela será definida para um valor reservado especial: `null` no Visual C# e `Nothing` no Visual Basic. Desse modo, quando o programa for iniciado, `firstClicked` e `secondClicked` serão definidas como `null` ou `Nothing`, o que significa que as variáveis não estão rastreando nada.  
  
2.  Modifique o manipulador de eventos Click para usar a nova variável de referência `firstClicked`. Remova a última instrução no método do manipulador de eventos `label_Click()` (`clickedLabel.ForeColor = Color.Black;`) e substitua-a pela instrução `if` que se segue. (Não se esqueça de incluir o comentário e a instrução `if` inteira.)  
  
     [!code-csharp[VbExpressTutorial4Step5#6](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step5/cs/form1.cs#6)]
     [!code-vb[VbExpressTutorial4Step5#6](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step5/vb/form1.vb#6)]  
  
3.  Salve e execute seu programa. Escolha um dos controles de rótulo e seu ícone é exibido.  
  
4.  Escolha o próximo controle de rótulo e observe que nada acontece. O programa já está rastreando o primeiro rótulo que o jogador escolheu, de modo que `firstClicked` não é igual a `null` no Visual C# ou `Nothing` no Visual Basic. Quando sua instrução `if` verifica `firstClicked` para determinar se ele é igual a `null` ou `Nothing`, ela descobre que não é e não executa as instruções na instrução `if`. Desse modo, somente o primeiro ícone que é escolhido torna-se preto e os outros ícones ficam invisíveis, conforme mostrado na imagem a seguir.  
  
     ![Jogo da memória mostrando um ícone](../ide/media/express-tut4step5.png "Express_Tut4Step5")  
Jogo da memória mostrando um ícone  
  
     Essa situação será corrigida na primeira etapa do tutorial adicionando um controle **Temporizador**.  
  
### <a name="to-continue-or-review"></a>Para continuar ou revisar  
  
-   Para acessar a próxima etapa do tutorial, consulte [Etapa 6: Adicionar um temporizador](../ide/step-6-add-a-timer.md).  
  
-   Para retornar à etapa anterior do tutorial, consulte [Etapa 4: Adicionar um manipulador de evento Click a cada rótulo](../ide/step-4-add-a-click-event-handler-to-each-label.md).



