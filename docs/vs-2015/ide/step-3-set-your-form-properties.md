---
title: 'Etapa 3: definir as propriedades do formulário | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 634ef037-1525-48c8-ac7f-abf04be69376
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 90fab2724c3d392db7824222da2450a8a4d585c3
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2019
ms.locfileid: "74295749"
---
# <a name="step-3-set-your-form-properties"></a>Etapa 3: Definir as propriedades do formulário
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Em seguida, use a janela **Propriedades** para alterar a aparência do seu formulário.

 ![link para vídeo](../data-tools/media/playvideo.gif "PlayVideo") Para obter uma versão de vídeo deste tópico, consulte [tutorial 1: criar um visualizador de imagens no Visual Basic-Video 1](https://go.microsoft.com/fwlink/?LinkId=205209) ou [tutorial 1: criar um visualizador C# de imagens em-vídeo 1](https://go.microsoft.com/fwlink/?LinkId=205199). Esses vídeos usam uma versão anterior do Visual Studio, portanto, existem pequenas diferenças em alguns comandos de menu e em outros elementos da interface do usuário. No entanto, os conceitos e procedimentos funcionam de maneiras semelhantes na versão atual do Visual Studio.

### <a name="to-set-your-form-properties"></a>Para definir suas propriedades de formulário

1. Certifique-se de que você esteja examinando o designer do Windows Forms. No IDE (ambiente de desenvolvimento integrado) do Visual Studio, escolha a guia **Form1.cs [Design]** (ou a guia **Form1.vb [Design]** no Visual Basic).

2. Escolha qualquer outro lugar dentro do formulário **Form1** para selecioná-lo. Examine a janela **Propriedades**, que agora deve mostrar as propriedades do formulário. Os formulários têm várias propriedades. Por exemplo, você pode definir a cor de primeiro plano e do plano de fundo, o texto do título que aparece na parte superior do formulário, o tamanho do formulário e outras propriedades.

   > [!NOTE]
   > Se a janela **Propriedades** não for exibida, interrompa seu programa escolhendo o botão quadrado **Parar Depuração** na barra de ferramentas ou apenas feche a janela. Se o programa for interrompido e você ainda não conseguir ver a janela **Propriedades**, na barra de menus, escolha **Exibir**, **Janela Propriedades**.

3. Depois que o formulário for selecionado, localize a propriedade de **Texto** na janela **Propriedades**. Dependendo de como a lista estiver classificada, talvez seja necessário rolar para baixo. Escolha **Texto**, digite **Visualizador de Imagens** e escolha ENTER.  Agora seu formulário deve ter o texto **Visualizador de Imagens** em sua barra de título, e a aparência da janela **Propriedades** deveria ser semelhante à seguinte imagem.

    ![Janela Propriedades](../ide/media/express-edittextproperty.png "Express_EditTextProperty") janela Propriedades

   > [!NOTE]
   > As propriedades podem ser classificadas por um modo Categorizado ou Alfabético. É possível mude entre essas duas modos de exibição usando os botões na janela **Propriedades**. Neste tutorial, é mais fácil localizar propriedades por meio da exibição Alfabética.

4. Volte ao Windows Forms Designer. Escolha a alça inferior direita do formulário, que é o pequeno quadrado branco no canto inferior direito do formulário e aparece da seguinte maneira.

    ![Arrastar a alça](../ide/media/express-bottomrt-drag.png "Express_BottomRT_Drag") Arrastar a alça

    Arraste a alça para redimensionar o formulário para que o formulário fique mais amplo e um pouco mais alto.

5. Examine a janela **Propriedades** e observe que a propriedade **Tamanho** foi alterada. A propriedade **Tamanho** é alterada a cada vez que você redimensiona o formulário. Tente arrastar a alça do formulário para redimensioná-la para um tamanho de aproximadamente 550, 350 (não é preciso ser exato), o que deve funcionar bem para este projeto. Como alternativa, é possível inserir os valores diretamente na propriedade **Tamanho** e, em seguida, pressionar a tecla ENTER.

6. Executar o programa novamente. Lembre-se de que você pode usar qualquer um dos métodos a seguir para executar seu programa.

   - Pressione a tecla **F5**.

   - Na barra de menus, escolha **Depurar**, **Iniciar Depuração**.

   - Na barra de ferramentas, clique no botão **Iniciar Depuração**, que aparece da seguinte maneira.

      ![Botão de barra de ferramentas iniciar depuração](../ide/media/express-icondebug.png "Express_IconDebug") Botão de barra de ferramentas iniciar depuração

     Assim como antes, o IDE compila e executa o programa e uma janela aparece.

7. Antes de seguir para a próxima etapa, interrompa o programa, pois a IDE não permitirá que você altere seu programa quando executar. Lembre-se de que você pode usar qualquer um dos métodos a seguir para parar seu programa.

   - Na barra de ferramentas, clique no botão **Parar Depuração**.

   - Na barra de menus, escolha **Depurar**, **Parar Depuração**.

   - Clique no botão X no canto superior da janela **Form1**.

### <a name="to-continue-or-review"></a>Para continuar ou revisar

- Para acessar a próxima etapa do tutorial, consulte [Etapa 4: Definir o layout do formulário com um controle TableLayoutPanel](../ide/step-4-lay-out-your-form-with-a-tablelayoutpanel-control.md).

- Para retornar à etapa anterior do tutorial, consulte [Etapa 2: Executar o programa](../ide/step-2-run-your-program.md).
