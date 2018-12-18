---
title: 'Etapa 1: Criar um projeto de aplicativo do Windows Forms'
ms.custom: ''
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-acquisition
ms.topic: conceptual
ms.assetid: 16ac2422-e720-4e3a-b511-bc2a54201a86
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: d9bcb82622a7ea303a632865b0c3f964de4b4dc3
ms.sourcegitcommit: 58052c29fc61c9a1ca55a64a63a7fdcde34668a4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34747649"
---
# <a name="step-1-create-a-windows-forms-application-project"></a>Etapa 1: Criar um projeto de aplicativo do Windows Forms
Ao criar um visualizador de imagens, a primeira etapa é criar um projeto de aplicativo do Windows Forms.

 ![link para vídeo](../data-tools/media/playvideo.gif)Para ver uma versão em vídeo deste tópico, confira [Tutorial 1: Criar um visualizador de imagens no Visual Basic – Vídeo 1](http://go.microsoft.com/fwlink/?LinkId=205209) ou [Tutorial 1: Criar um visualizador de imagens em C# – Vídeo 1](http://go.microsoft.com/fwlink/?LinkId=205199). Esses vídeos usam uma versão anterior do Visual Studio, portanto, existem pequenas diferenças em alguns comandos de menu e em outros elementos da interface do usuário. No entanto, os conceitos e procedimentos funcionam de maneiras semelhantes na versão atual do Visual Studio.

## <a name="to-create-a-windows-forms-application-project"></a>Para criar um projeto de aplicativo do Windows Forms

1.  Na barra de menus, selecione **Arquivo** > **Novo** > **Projeto**. A caixa de diálogo deve ser assim.

     ![Caixa de diálogo Novo projeto](../ide/media/newprojectdialogcallouts.png)
Caixa de diálogo **Novo projeto**

2.  Escolha **Visual C#** ou **Visual Basic** na lista de **Modelos Instalados**.

3.  Na lista de modelos, escolha o ícone **Aplicativo do Windows Forms**. Dê o nome de **PictureViewer** ao novo formulário e escolha o botão **OK**.

     O Visual Studio cria uma solução para seu programa. Uma solução atua como um recipiente para todos os projetos e arquivos necessários pelo seu programa. Esses termos serão explicados em mais detalhes posteriormente neste tutorial.

4.  A ilustração a seguir mostra o que você deve ver agora na interface do Visual Studio.

    > [!NOTE]
    >  O layout da janela pode não ser exatamente como esta ilustração. O layout preciso da janela depende da versão do Visual Studio, da linguagem de programação usada e de outros fatores. Entretanto, você deve verificar que todas as três janelas aparecem.

     ![Janela IDE](../ide/media/express_ideoverview_visio.png)
Janela **IDE**

     A interface contém três janelas: uma janela principal, o **Gerenciador de Soluções** e a janela **Propriedades**.

     Se qualquer uma das janelas estiver faltando, restaure o layout de janela padrão ao escolher, na barra de menus, **Janela** > **Redefinir Layout da Janela**. Você também pode exibir janelas usando os comandos de menu. Na barra de menus, escolha **Modo de Exibição** > **Janela Propriedades** ou **Gerenciador de Soluções**. Se qualquer outra janela está aberta, feche-a escolhendo o botão **Fechar** (x) no canto superior direito.

5.  A ilustração a seguir mostra as seguintes janelas (no sentido horário a partir do canto superior esquerdo):

    -   **Janela principal** Nesta janela você fará a maior parte de seu trabalho, como trabalhar com formulários e editar códigos. Na ilustração, a janela mostra um formulário no **Editor de Formulários**. Na parte superior da janela, a guia **Página Inicial** e a guia **Form1.cs [Design]** aparecem. (No Visual Basic, o nome da guia termina com *.vb*, em vez de *.cs*).

    -   **Janela do Gerenciador de Soluções** Nesta janela, você pode exibir e navegar em todos os itens na solução. Se você escolher um arquivo, o conteúdo da janela **Propriedades** será alterado. Se você abrir um arquivo de código (que termine com *.cs* no Visual C# e com *.vb* no Visual Basic), o arquivo de código ou um designer para o arquivo de código será exibido. Um designer é uma superfície visual na qual você pode adicionar controles, como botões e listas. Para formulários do Visual Studio, o designer é chamado no **Designer de Formulários do Windows**.

    -   **Janela Propriedades** Nessa janela, você pode alterar as propriedades dos itens escolhidos nas outras janelas. Por exemplo, se você escolher o Form1, você poderá alterar o título configurando a propriedade **Text** e você poderá alterar a cor da tela de fundo configurando a propriedade **Backcolor**.

    > [!NOTE]
    >  A linha superior no **Gerenciador de Soluções** mostra **Solução "PictureViewer" (1 projeto)**, o que significa que o Visual Studio criou uma solução para você. Uma solução pode conter mais de um projeto, mas por enquanto, você trabalhará com soluções que contêm somente um projeto.

6.  Na barra de menus, escolha **Arquivo** > **Salvar Todos**.

     Como alternativa, escolha o botão **Salvar Todos** na barra de ferramentas, demostrado na ilustração a seguir.

     ![Botão de barra de ferramentas Salvar Tudo](../ide/media/express_iconsaveall.png)
Botão de barra de ferramentas **Salvar Tudo**

     O Visual Studio preenche automaticamente o nome da pasta e o nome do projeto e, em seguida, salva o projeto na sua pasta de projeto.

## <a name="to-continue-or-review"></a>Para continuar ou revisar

-   Para ir para a próxima etapa do tutorial, veja [Etapa 2: Executar o programa](../ide/step-2-run-your-program.md).

-   Para retornar ao tópico de visão geral, veja [Tutorial 1: Criar um visualizador de imagens](../ide/tutorial-1-create-a-picture-viewer.md).
