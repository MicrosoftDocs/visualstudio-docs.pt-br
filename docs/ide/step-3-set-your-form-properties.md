---
title: 'Etapa 3: Definir as propriedades do formulário'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 634ef037-1525-48c8-ac7f-abf04be69376
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b8edb5fd4b7df44528461d5078e78fd315c0c40b
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2019
ms.locfileid: "55931449"
---
# <a name="step-3-set-your-form-properties"></a>Etapa 3: Definir as propriedades do formulário
Em seguida, use a janela **Propriedades** para alterar a aparência do seu formulário.

 ![link para vídeo](../data-tools/media/playvideo.gif) Para obter uma versão em vídeo deste tópico, confira [Tutorial 1: Criar um visualizador de imagens em Visual Basic – Vídeo 1](http://go.microsoft.com/fwlink/?LinkId=205209) ou [Tutorial 1: Criar um visualizador de imagens em C# – Vídeo 1](http://go.microsoft.com/fwlink/?LinkId=205199). Esses vídeos usam uma versão anterior do Visual Studio, portanto, existem pequenas diferenças em alguns comandos de menu e em outros elementos da interface do usuário. No entanto, os conceitos e procedimentos funcionam de maneiras semelhantes na versão atual do Visual Studio.

## <a name="to-set-your-form-properties"></a>Para definir suas propriedades de formulário

1. Certifique-se de que você esteja examinando o **Designer de Formulários do Windows**. No IDE (ambiente de desenvolvimento integrado) do Visual Studio, escolha a guia **Form1.cs [Design]** (ou a guia **Form1.vb [Design]** no Visual Basic).

2. Escolha qualquer outro lugar dentro do formulário **Form1** para selecioná-lo. Examine a janela **Propriedades**, que agora deve mostrar as propriedades do formulário. Os formulários têm várias propriedades. Por exemplo, você pode definir a cor de primeiro plano e do plano de fundo, o texto do título que aparece na parte superior do formulário, o tamanho do formulário e outras propriedades.

   > [!NOTE]
   >  Se a janela **Propriedades** não for exibida, interrompa seu programa escolhendo o botão quadrado **Parar Depuração** na barra de ferramentas ou apenas feche a janela. Se o programa for interrompido e você ainda não conseguir ver a janela **Propriedades**, na barra de menus, escolha **Exibir** > **Janela Propriedades**.

3. Depois que o formulário for selecionado, localize a propriedade de **Texto** na janela **Propriedades**. Dependendo de como a lista estiver classificada, talvez seja necessário rolar para baixo. Escolha **Texto**, digite **Visualizador de Imagens** e escolha **Enter**.  Agora seu formulário deve ter o texto **Visualizador de Imagens** em sua barra de título, e a aparência da janela **Propriedades** deveria ser semelhante à seguinte imagem.

    ![Janela propriedades](../ide/media/express_edittextproperty.png)
    Janela**Propriedades**

   > [!NOTE]
   >  As propriedades podem ser classificadas por um modo **Categorizado** ou **Alfabético**. É possível mude entre essas duas modos de exibição usando os botões na janela **Propriedades**. Neste tutorial, é mais fácil localizar propriedades por meio da exibição **Alfabética**.

4. Volte ao **Designer de Formulários do Windows**. Escolha a alça inferior direita do formulário, que é o pequeno quadrado branco no canto inferior direito do formulário e aparece da seguinte maneira.

    ![Arrastar a alça](../ide/media/express_bottomrt_drag.png) Arrastar a alça

    Arraste a alça para redimensionar o formulário para que o formulário fique mais amplo e um pouco mais alto.

5. Examine a janela **Propriedades** e observe que a propriedade **Tamanho** foi alterada. A propriedade **Tamanho** é alterada a cada vez que você redimensiona o formulário. Tente arrastar a alça do formulário para redimensioná-la para um tamanho de aproximadamente **550, 350** (não é preciso ser exato), o que deve funcionar bem para este projeto. Como alternativa, é possível inserir os valores diretamente na propriedade **Tamanho** e, em seguida, pressionar a tecla **Enter**.

6. Executar o programa novamente. Lembre-se de que você pode usar qualquer um dos métodos a seguir para executar seu programa.

   - Pressione a tecla **F5**.

   - Na barra de menus, escolha **Depurar** > **Iniciar Depuração**.

   - Na barra de ferramentas, clique no botão **Iniciar Depuração**, que aparece da seguinte maneira.

      ![Botão de barra de ferramentas Iniciar Depuração](../ide/media/express_icondebug.png)
     Botão de barra de ferramentas **Iniciar Depuração**

     Assim como antes, o IDE compila e executa o programa e uma janela aparece.

7. Antes de seguir para a próxima etapa, interrompa o programa, pois a IDE não permitirá que você altere seu programa quando executar. Lembre-se de que você pode usar qualquer um dos métodos a seguir para parar seu programa.

   -   Na barra de ferramentas, clique no botão **Parar Depuração**.

   -   Na barra de menus, escolha **Depurar** > **Parar Depuração**.

   -   Clique no botão **X** no canto superior da janela **Form1**.

## <a name="to-continue-or-review"></a>Para continuar ou revisar

-   Para ir para a próxima etapa do tutorial, confira [Etapa 4: Definir o layout do formulário com um controle TableLayoutPanel](../ide/step-4-lay-out-your-form-with-a-tablelayoutpanel-control.md).

-   Para retornar à etapa anterior do tutorial, confira [Etapa 2: Executar o programa](../ide/step-2-run-your-program.md).
