---
title: 'Etapa 5: Adicionar referências de rótulo'
description: Saiba como adicionar referências de rótulo ao formulário.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
ms.assetid: d418350c-0396-494e-8149-71fa61b395c5
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 393f71c3360371122e86dc078aaa97c6963db325
ms.sourcegitcommit: 6d88913a8b5a9e5eda01d3f95205b4d138f440f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/13/2021
ms.locfileid: "107296268"
---
# <a name="step-5-add-label-references"></a>Etapa 5: Adicionar referências de rótulo
O programa precisa rastrear quais controles de rótulo o jogador escolhe. Atualmente, o programa mostra todos os rótulos escolhidos pelo jogador. Mas isso será alterado. Depois que o primeiro rótulo é escolhido, o programa deve mostrar o ícone do rótulo. Depois que o segundo rótulo é escolhido, o programa deve exibir ambos os ícones por um breve momento e depois ocultá-los novamente. Agora seu programa rastreará qual controle de rótulo será escolhido primeiro e qual será escolhido em segundo usando *variáveis de referência*.

## <a name="to-add-label-references"></a>Para adicionar referências de rótulo

1. Adicione referências de rótulo ao seu formulário usando o código a seguir.

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step5/vb/form1.vb" id="Snippet5":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step5/cs/form1.cs" id="Snippet5":::

     > [!IMPORTANT]
     > Use o controle linguagem de programação no canto superior direito desta página para exibir o trecho de código C# ou o trecho de código de Visual Basic.<br><br>![Controle de linguagem de programação para Docs.Microsoft.com](../ide/media/docs-programming-language-control.png)

     Essas variáveis de referência parecem semelhantes às instruções que você usou anteriormente para adicionar objetos (como os objetos <xref:System.Windows.Forms.Timer>, <xref:System.Collections.Generic.List%601> e <xref:System.Random>) ao formulário. No entanto, essas instruções não fazem com que os dois controles de rótulo extras apareçam no formulário, pois a palavra-chave `new` não foi usada em nenhuma das duas instruções. Sem a palavra-chave `new`, nenhum objeto é criado. Por esse motivo `firstClicked` e `secondClicked` são chamadas de variáveis de referência: elas rastreiam (ou fazem referência a) os objetos Label.

     Quando uma variável não mantém o controle de um objeto, ela é definida como um valor reservado especial: `null` em C# e `Nothing` em Visual Basic. Desse modo, quando o programa for iniciado, `firstClicked` e `secondClicked` serão definidas como `null` ou `Nothing`, o que significa que as variáveis não estão rastreando nada.

2. Modifique o manipulador de eventos <xref:System.Windows.Forms.Control.Click> para usar a nova variável de referência `firstClicked`. Remova a última instrução no método do manipulador de eventos `label_Click()` (`clickedLabel.ForeColor = Color.Black;`) e substitua-a pela instrução `if` que se segue. (Não se esqueça de incluir o comentário e a instrução `if` inteira.)

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step5/vb/form1.vb" id="Snippet6":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step5/cs/form1.cs" id="Snippet6":::

3. Salve e execute seu programa. Escolha um dos controles de rótulo e seu ícone é exibido.

4. Escolha o próximo controle de rótulo e observe que nada acontece. O programa já está acompanhando o primeiro rótulo que o jogador escolheu, portanto, `firstClicked` não é igual a `null` em C# ou `Nothing` em Visual Basic. Quando sua instrução `if` verifica `firstClicked` para determinar se ele é igual a `null` ou `Nothing`, ela descobre que não é e não executa as instruções na instrução `if`. Portanto, somente o primeiro ícone escolhido fica preto e os outros ícones são invisíveis, conforme mostrado na imagem a seguir.

     ![Jogo da memória mostrando um ícone](../ide/media/express_tut4step5.png)<br/>
***Jogo de correspondência** _ _showing um ícone *

     Essa situação será corrigida na primeira etapa do tutorial adicionando um controle **Temporizador**.

## <a name="to-continue-or-review"></a>Para continuar ou revisar

- Para ir para a próxima etapa do tutorial, consulte **[etapa 6: adicionar um temporizador](../ide/step-6-add-a-timer.md)**.

- Para retornar à etapa anterior do tutorial, veja [Etapa 4: Adicionar um manipulador de eventos Click a cada rótulo](../ide/step-4-add-a-click-event-handler-to-each-label.md).
