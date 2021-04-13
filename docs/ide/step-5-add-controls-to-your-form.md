---
title: 'Etapa 5: Adicionar controles ao formulário'
description: Saiba como adicionar controles, como um <xref:System.Windows.Forms.PictureBox> controle e um <xref:System.Windows.Forms.CheckBox> controle, ao seu formulário.
ms.custom: SEO-VS-2020
ms.date: 08/30/2019
ms.assetid: dc2746f4-0b5c-4674-9ef7-f40f94150f52
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d2c05dbaa70585fb1a15f4f7378ea85c2c0a33b9
ms.sourcegitcommit: 6d88913a8b5a9e5eda01d3f95205b4d138f440f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/13/2021
ms.locfileid: "107296294"
---
# <a name="step-5-add-controls-to-your-form"></a>Etapa 5: Adicionar controles ao formulário

Nessa etapa, você adiciona controles como um controle <xref:System.Windows.Forms.PictureBox> e um controle <xref:System.Windows.Forms.CheckBox> em seu formulário. Para adicionar controles <xref:System.Windows.Forms.Button> ao seu formulário.

## <a name="how-to-add-controls-to-your-form"></a>Como adicionar controles ao formulário

1. Escolha a guia **caixa de ferramentas** no lado esquerdo do IDE do Visual Studio (ou pressione **Ctrl** + **ALT** + **X**) e, em seguida, expanda o grupo **controles comuns** . Isso mostra os controles mais comuns que você vê em formulários.

1. Clique duas vezes no item **PictureBox** para adicionar um controle PictureBox ao seu formulário. Como o TableLayoutPanel é encaixado para preencher o formulário, a IDE adiciona o controle da PictureBox à primeira célula vazia (canto superior esquerdo).

1. Escolha o novo controle **PictureBox** para selecioná-lo e, em seguida, escolha o triângulo preto no novo controle PictureBox para exibir sua lista de tarefas, conforme mostrado na captura de tela a seguir.

    ![Tarefas PictureBox](../ide/media/express_pictureboxtasks.png)<br/>PictureBox **_ _tasks**

    > [!NOTE]
    > Se você adicionar acidentalmente o tipo errado de controle a seu TableLayoutPanel, poderá excluí-lo. Clique com o botão direito do mouse no controle e escolha **Excluir** no menu de contexto. Você pode também remover os controles de formulário usando a barra de menus. Na barra de menus, escolha **Editar**  >  **desfazer** ou **Editar**  >  **excluir**.

1. No menu **tarefas de PictureBox** do controle **PictureBox** , escolha o link **encaixar no contêiner pai** . Isso define automaticamente a propriedade **Dock** de PictureBox como **Fill**. Para ver isso, escolha o controle **PictureBox** para selecioná-lo, vá para a janela **Propriedades** e verifique se a propriedade **Dock** está definida como **Fill**.

1. Faça a PictureBox se estender por ambas as colunas alterando sua propriedade **ColumnSpan**. Na **PictureBox**, escolha o controle **PictureBox** e defina sua propriedade **ColumnSpan** como **2**. Além disso, quando a PictureBox está vazia, você deseja mostrar uma estrutura vazia. Defina sua propriedade **BorderStyle** para **Fixed3D**.

    > [!NOTE]
    > Se você não vir uma propriedade **ColumnSpan** para sua PictureBox, então será provável que a PictureBox tenha sido adicionada ao formulário em vez de ao TableLayoutPanel. Para corrigir isso, escolha **PictureBox**, Delete, escolha o **TableLayoutPanel** e, em seguida, adicione uma nova PictureBox.

1. Escolha o **TableLayoutPanel** no formulário e, em seguida, adicione um controle de caixa de seleção ao formulário. Clique duas vezes no item de **caixa de seleção** na caixa de **ferramentas** para adicionar um novo controle de caixa de seleção à próxima célula gratuita da tabela. Como um PictureBox ocupa as duas primeiras células em TableLayoutPanel, o controle de caixa de seleção é adicionado à célula do canto inferior esquerdo. Escolha a propriedade **texto** e digite a **ampliação** da palavra, conforme mostrado na imagem a seguir.

    ![Controle TextBox com a propriedade Stretch](../ide/media/express_pictureviewercheckbox.png)<br/>***TextBox** _ _Control com * ***Stretch**_ _property *

1. Escolha o **TableLayoutPanel** no formulário e, em seguida, vá para o grupo **contêineres** na **caixa de ferramentas** (onde você obteve o controle TableLayoutPanel) e clique duas vezes no item **FlowLayoutPanel** para adicionar um novo controle à última célula (canto inferior direito). Em seguida, encaixe o FlowLayoutPanel no TableLayoutPanel. Você pode fazer isso escolhendo **encaixar no contêiner pai** na lista de tarefas do triângulo preto do FlowLayoutPanel ou definindo a propriedade **Dock** do FlowLayoutPanel como **Fill**.

    > [!NOTE]
    > Um <xref:System.Windows.Forms.FlowLayoutPanel> é um contêiner que organiza outros controles em uma linha, um após o outro. Quando você redimensiona um FlowLayoutPanel, ele dispõe de todos os seus controles em uma única linha, se tiver espaço para fazer isso. Caso contrário, organize-os em linhas, um sobre o outro. <br/><br/>Aqui, você usará um FlowLayoutPanel para manter quatro botões. Se os botões organizam um no topo do outro ao adicioná-los, certifique-se de selecionar o FlowLayoutPanel antes de adicionar os botões. <br/><br/>(Normalmente, cada célula contém apenas um controle. Neste exemplo, a célula inferior direita do TableLayoutPanel contém quatro controles Button. Por que?  Como o FlowLayoutPanel é um controle de contêiner, que é um controle em uma célula que contém outros controles.)

## <a name="to-add-buttons"></a>Para adicionar botões

1. Escolha o novo FlowLayoutPanel que você adicionou. Vá para **controles comuns** na **caixa de ferramentas** e clique duas vezes no item de **botão** para adicionar um controle de botão chamado **Button1** ao seu FlowLayoutPanel. Repita para adicionar outro botão. O IDE determina que já há um botão chamado **button1** e chama o próximo de **button2**.

1. Normalmente, você adiciona os outros botões usando a **caixa de ferramentas**. Desta vez, escolha **Button2** e, em seguida, na barra de menus, escolha **Editar**  >  **cópia** (ou pressione **Ctrl** + **C**). Em seguida, escolha **Editar**  >  **colar** na barra de menus (ou pressione **Ctrl** + **V**) para colar uma cópia do botão. Agora cole-o novamente. Observe que o IDE adiciona **button3** e **Button4** ao FlowLayoutPanel.

    > [!NOTE]
    > Você pode copiar e colar qualquer controle. O IDE nomeia e coloca os novos controles de uma maneira lógica. Se você colar um controle em um contêiner, o IDE escolherá o próximo espaço lógico para posicionamento.

1. Escolha o primeiro botão e defina sua propriedade **Text** como **Show a picture**. Em seguida, defina as propriedades **Text** dos próximos três botões como **Limpar a imagem**, **Definir a cor da tela de fundo** e **Fechar**.

1. Vamos dimensionar os botões e organizá-los para que fiquem alinhados ao lado direito do painel. Escolha o **FlowLayoutPanel** e examine sua propriedade **FlowDirection** . Altere-a para que ela seja definida como **RightToLeft**.

   Os botões devem se alinhar ao lado direito da célula e reverter a ordem para que o botão **mostrar uma imagem** esteja à direita.

    > [!NOTE]
    > Se os botões ainda estiverem na ordem errada, você poderá arrastar os botões em torno do FlowLayoutPanel para reorganizá-los em qualquer ordem. Você pode escolher um botão e o arrastar para a esquerda ou direita.

1. Escolha o botão **Fechar** para selecioná-lo. Em seguida, para escolher o restante dos botões ao mesmo tempo, pressione e segure a tecla **Ctrl** e escolha-as também.

   Depois de selecionar todos os botões, vá para a janela **Propriedades** e role para cima até a propriedade **AutoSize** . Essa propriedade informa o botão para redimensionar automaticamente para ajustar todo o texto correspondente. Defina-o como **true**.

   Os botões agora devem ser dimensionados corretamente e estar na ordem correta. (Desde que todos os quatro botões sejam selecionados, você pode alterar todas as quatro propriedades de **dimensionamento** ao mesmo tempo.) A imagem a seguir mostra os quatro botões.

    ![Visualizador de imagens com quatro botões](../ide/media/express_autosize.png)<br/>***Visualizador de imagem** _ _with quatro botões *

1. Agora, execute o programa novamente para ver suas alterações.

   Observe que os botões e a caixa de seleção não fazem nada ainda &mdash; , mas serão, em breve.

## <a name="to-continue-or-review"></a>Para continuar ou revisar

* Para ir para a próxima etapa do tutorial, consulte **[etapa 6: nomear os controles de botão](../ide/step-6-name-your-button-controls.md)**.

* Para retornar à etapa anterior do tutorial, consulte [etapa 4: dispor o formulário com um controle TableLayoutPanel](../ide/step-4-lay-out-your-form-with-a-tablelayoutpanel-control.md).

## <a name="see-also"></a>Confira também

* [Tutorial 2: criar um teste de matemática cronometrado](tutorial-2-create-a-timed-math-quiz.md)
* [Tutorial 3: criar um jogo de correspondência](tutorial-3-create-a-matching-game.md)
