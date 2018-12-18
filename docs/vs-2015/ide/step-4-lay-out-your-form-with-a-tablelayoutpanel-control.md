---
title: 'Etapa 4: definir o layout do formulário com um controle TableLayoutPanel | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 61acde79-e115-4bad-bb06-1fbe37717a3e
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 4a08359c11fa45c87c787a5a3a414eb8515e7473
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49210088"
---
# <a name="step-4-lay-out-your-form-with-a-tablelayoutpanel-control"></a>Etapa 4: Definir o layout do formulário com um controle TableLayoutPanel
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Nesta etapa, você adiciona um controle `TableLayoutPanel` ao formulário. O TableLayoutPanel ajuda a alinhar corretamente controles no formulário que você irá adicionar posteriormente.  
  
 ![link para vídeo](../data-tools/media/playvideo.gif "PlayVideo")Para uma versão em vídeo deste tópico, consulte o [Tutorial 1: criar um Visualizador de Imagens no Visual Basic – Vídeo 2](http://go.microsoft.com/fwlink/?LinkId=205211) ou o [Tutorial 1: criar um Visualizador de Imagens em C# – Vídeo 2](http://go.microsoft.com/fwlink/?LinkId=205200). Esses vídeos usam uma versão anterior do Visual Studio, portanto, existem pequenas diferenças em alguns comandos de menu e em outros elementos da interface do usuário. No entanto, os conceitos e procedimentos funcionam de maneiras semelhantes na versão atual do Visual Studio.  
  
### <a name="to-lay-out-your-form-with-a-tablelayoutpanel-control"></a>Para apresentar seu formulário com um controle TableLayoutPanel  
  
1.  No lado esquerdo do IDE do Visual Studio, localize a guia **Caixa de Ferramentas**. Escolha a guia **Caixa de Ferramentas** e a Caixa de Ferramentas aparecerá. (Ou, na barra de menus, escolha **Exibir**, **Caixa de Ferramentas**.)  
  
2.  Escolha o pequeno símbolo de triângulo ao lado do grupo **Contêineres** para abri-lo, como mostrado na imagem a seguir.  
  
     ![Grupo de contêineres](../ide/media/express-toolbox.png "Express_Toolbox")  
Grupo de contêineres  
  
3.  Você pode adicionar controles como botões, caixas de seleção e rótulos para seu formulário. Clique duas vezes no controle `TableLayoutPanel` na Caixa de Ferramentas. (Ou, você pode arrastar o controle da caixa de ferramentas para o formulário.) Quando você fizer isso, o IDE adicionará um controle `TableLayoutPanel` ao formulário, conforme mostrado na seguinte imagem.  
  
     ![Controle TableLayoutPanel](../ide/media/express-formtablelayout.png "Express_FormTableLayout")  
Controle TableLayoutPanel  
  
    > [!NOTE]
    >  Após adicionar seu TableLayoutPanel, se uma janela aparecer no formulário com o título **Tarefas de TableLayoutPanel**, clique em qualquer lugar dentro do formulário para fechá-la. Você aprenderá mais sobre essa janela mais tarde neste tutorial.  
  
     Observe como a caixa de ferramentas expande para cobrir o formulário quando você clica em sua guia, e fecha depois que você clica em qualquer lugar fora dela. Esse é o recurso de ocultação automática IDE. Você pode ligar ou desligar para qualquer uma das janelas, escolhendo o ícone de anotações no canto superior direito da janela para alternar entre ocultar automaticamente e fixar no lugar. O ícone de anotações aparece da seguinte maneira.  
  
     ![Ícone de pino](../ide/media/express-pushpintoolbox.png "Express_PushpinToolbox")  
Ícone de pino  
  
4.  Escolha **TableLayoutPanel** para garantir que esteja selecionado. Você pode verificar qual controle está selecionado examinando a lista suspensa na parte superior da janela **Propriedades**, conforme mostrado na imagem a seguir.  
  
     ![Janela Propriedades mostrando o controle TableLayoutPanel](../ide/media/express-controlspropwin.png "Express_ControlsPropWin")  
A janela Propriedades que mostra o controle TableLayoutPanel  
  
5.  Escolha o botão **Alfabético** na barra de ferramentas na janela **Propriedades**. Isso faz com que a lista de propriedades na janela **Propriedades** seja exibida em ordem alfabética, o que facilitará a localização de propriedades neste tutorial.  
  
6.  O seletor de controle é uma lista suspensa na parte superior da janela **Propriedades**. Neste exemplo, ela mostra que um controle chamado `tableLayoutPanel1` está selecionado. Você pode selecionar controles escolhendo uma área no designer do Windows Forms ou escolhendo no seletor de controle. Agora que `TableLayoutPanel` está selecionado, localize a propriedade **Encaixar** e escolha **Encaixar**, que deve estar definido como **Nenhum**. Observe que uma seta suspensa aparece ao lado do valor. Escolha a seta e selecione o botão **Preenchimento** (o botão grande no meio), como mostrado na imagem a seguir.  
  
     ![Janela Propriedades com preenchimento selecionado](../ide/media/express-docktable.png "Express_DockTable")  
A janela Propriedades com o preenchimento selecionado  
  
     *Encaixe* no Visual Studio refere-se a quando uma janela é anexada a outra janela ou área no IDE. Por exemplo, a janela Propriedades pode ser desencaixada – isto é, ser desanexada e ter flutuação livre no Visual Studio – ou pode ser encaixada no **Gerenciador de Soluções**.  
  
7.  Após você definir a propriedade **Encaixar** de TableLayoutPanel como **Preenchimento**, o painel preenche o formulário inteiro. Se você redimensionar o formulário novamente, o TableLayoutPanel permanecerá anexado e se redimensionará para caber.  
  
    > [!NOTE]
    >  Um TableLayoutPanel funciona como uma tabela no Microsoft Office Word: tem linhas e colunas, e uma célula individual pode abranger várias linhas e colunas. Cada célula pode conter um controle (como um botão, uma caixa de seleção ou um rótulo). O TableLayoutPanel terá um controle `PictureBox` que abrange a primeira linha inteira, um controle `CheckBox` na célula do canto inferior esquerdo e quatro controles `Button` na célula inferior direita.  
  
8.  Atualmente, o TableLayoutPanel tem duas linhas de igual tamanho e duas colunas de igual tamanho. Você precisa redimensionar para que a primeira linha e a coluna da direita sejam bem maiores. No designer do Windows Forms, selecione o TableLayoutPanel. No canto superior direito, há um pequeno botão de triângulo preto, que aparece da seguinte maneira.  
  
     ![Botão de triângulo](../ide/media/express-iconblacktriangle.gif "Express_IconBlackTriangle")  
Botão de triângulo  
  
     Este botão indica que o controle tem as tarefas que ajudam você definir suas propriedades automaticamente.  
  
9. Escolha o triângulo para exibir a lista de tarefas do controle, como mostrado na imagem a seguir.  
  
     ![Tarefas de TableLayoutPanel](../ide/media/express-tablepanel.png "Express_TablePanel")  
Tarefas TableLayoutPanel  
  
10. Escolha a tarefa **Editar Linhas e Colunas** para exibir a janela **Estilos de Coluna e Linha**. Escolha **Column1** e defina o tamanho como 15%, certificando-se de que o botão **Porcentagem** esteja selecionado e inserindo `15` na caixa **Porcentagem**. (Trata-se de um controle `NumericUpDown`, que você usará em um tutorial posterior.) Escolha **Column2** e defina-a como 85%. Não escolha o botão **OK** ainda, pois a janela fechará. (Mas se você fizer isso, você pode reabri-la usando a lista de tarefas.)  
  
     ![Estilos de linha e coluna de TableLayoutPanel](../ide/media/vs-tablelayoutpanel-setup.png "VS_TableLayoutPanel_Setup")  
Estilos de coluna e linha TableLayoutPanel  
  
11. Na lista suspensa **Mostrar** na parte superior da janela, escolha **Linhas**. Defina **Row1** como 90% e **Row2** como 10%.  
  
12. Escolha o botão **OK**. O TableLayoutPanel agora deve ter uma grande primeira linha, uma pequena linha inferior, uma pequena coluna esquerda, e uma grande coluna direita. Você pode redimensionar linhas e colunas em TableLayoutPanel selecionando tableLayoutPanel1 no formulário e então arrastando as bordas de linha e coluna.  
  
     ![Form1 com o painel TableLayoutPanel redimensionado](../ide/media/vs-formafterlayoutpanel.png "VS_FormAfterLayoutPanel")  
Form1 com TableLayoutPanel redimensionado  
  
### <a name="to-continue-or-review"></a>Para continuar ou revisar  
  
-   Para ir à próxima etapa do tutorial, consulte [Etapa 5: adicionar controles ao formulário](../ide/step-5-add-controls-to-your-form.md).  
  
-   Para retornar à etapa anterior do tutorial, consulte [Etapa 3: definir as propriedades do formulário](../ide/step-3-set-your-form-properties.md).



