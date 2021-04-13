---
title: 'Etapa 4: Adicionar um manipulador de eventos de clique a cada rótulo'
description: Saiba como adicionar um manipulador de eventos de clique a cada rótulo.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- vb
ms.assetid: 16bdbc7c-4129-411d-bace-f4a3e5375975
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ffaa3986ee5ef23f007d6e66a30b75eb8b06bff4
ms.sourcegitcommit: 6d88913a8b5a9e5eda01d3f95205b4d138f440f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/13/2021
ms.locfileid: "107296255"
---
# <a name="step-4-add-a-click-event-handler-to-each-label"></a>Etapa 4: Adicionar um manipulador de eventos de clique a cada rótulo

O jogo da memória funciona desta forma:

1. Quando um jogador escolhe um dos quadrados com um ícone oculto, o programa mostra o ícone ao jogador alterando a cor do ícone para preto.

2. Em seguida, o jogador escolhe outro ícone oculto.

3. Se os ícones corresponderem, eles permanecerão visíveis. Caso contrário, os ícones serão ocultados novamente.

   Para que seu programa funcione dessa forma, adicione um manipulador de eventos <xref:System.Windows.Forms.Control.Click> que altera a cor do rótulo escolhido.

## <a name="to-add-a-click-event-handler-to-each-label"></a>Para adicionar um manipulador de eventos Click a cada rótulo

1. Abra o formulário no **Designer de Formulários do Windows**. No **Gerenciador de Soluções**, escolha *Form1.cs* ou *Form1.vb*. Na barra de menus, escolha   >  **Designer** de exibição.

2. Escolha o primeiro controle de rótulo para selecioná-lo. Em seguida, mantenha pressionada a tecla **Ctrl** enquanto escolhe cada um dos outros rótulos para selecioná-los. Verifique se cada um dos rótulos foi selecionado.

3. Escolha o botão **Eventos** na barra de ferramentas da janela **Propriedades** para exibir a página **Eventos** na janela **Propriedades**. Role para baixo até o evento de **clique** e insira **label_Click** na caixa, conforme mostrado na captura de tela a seguir.

     ![Janela Propriedades mostrando o evento Click](../ide/media/express_labelclick.png)

4. Escolha a tecla **Enter** . O IDE adiciona um manipulador de eventos `Click` chamado `label_Click()` ao código e o vincula a cada um dos rótulos no formulário.

5. Preencha o restante do código, como se segue:

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs" id="Snippet4":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/vb/form1.vb" id="Snippet4":::

    > [!IMPORTANT]
    > Use o controle linguagem de programação no canto superior direito desta página para exibir o trecho de código C# ou o trecho de código de Visual Basic.<br><br>![Controle de linguagem de programação para Docs.Microsoft.com](../ide/media/docs-programming-language-control.png)

    > [!NOTE]
    > Se você copiar e colar o bloco de código `label_Click()` em vez de inserir o código manualmente, não se esqueça de substituir o código `label_Click()` existente. Caso contrário, você terá um bloco de código duplicado.

    > [!NOTE]
    > Você pode reconhecer `object sender` na parte superior do manipulador de eventos como o mesmo usado no [Tutorial 2: Criar um teste de matemática cronometrado](../ide/tutorial-2-create-a-timed-math-quiz.md). Como você vinculou diferentes eventos Click de controle de rótulo a um único método do manipulador de eventos, o mesmo método será chamado, independentemente de qual rótulo foi escolhido pelo usuário. O método do manipulador de eventos precisa saber qual rótulo foi escolhido, de modo que ele usa o nome `sender` para identificar o controle de rótulo. A primeira linha do método informa o programa que ele não é apenas um objeto genérico, mas especificamente um controle de rótulo e que usa o nome `clickedLabel` para acessar as propriedades e os métodos do rótulo.

     Esse método primeiro verifica se `clickedLabel` foi convertido com sucesso de um objeto em um controle de rótulo. Se a conversão não foi bem-sucedida, ele terá um valor `null` (C#) ou `Nothing` (Visual Basic), e não será conveniente executar o restante do código no método. Em seguida, o método verifica a cor do texto do rótulo escolhido usando a propriedade **ForeColor** do rótulo. Se a cor do texto do rótulo for preto, isso significa que o ícone já foi escolhido e o método já executado. (É isso que a `return` instrução faz: diz ao programa para parar de executar o método.) Caso contrário, o ícone não foi escolhido, portanto, o programa altera a cor do texto do rótulo para preto.

6. Na barra de menus, escolha **arquivo**  >  **salvar tudo** para salvar seu progresso e, na barra de menus, escolha **depurar**  >  **Iniciar Depuração** para executar o programa. Você deverá ver um formulário vazio com um plano de fundo azul. Escolha qualquer uma das células no formulário e um dos ícones deverá se tornar visível. Continue escolhendo diferentes locais no formulário. À medida que você escolhe os ícones, eles devem aparecer.

## <a name="to-continue-or-review"></a>Para continuar ou revisar

- Para ir para a próxima etapa do tutorial, consulte **[etapa 5: adicionar referências de rótulo](../ide/step-5-add-label-references.md)**.

- Para retornar à etapa anterior do tutorial, veja [Etapa 3: Atribuir um ícone aleatório a cada rótulo](../ide/step-3-assign-a-random-icon-to-each-label.md).
