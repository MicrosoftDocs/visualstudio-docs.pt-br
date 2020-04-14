---
title: Criar um aplicativo do Windows Forms com o Visual Basic
description: Aprenda o passo a passo de como criar um aplicativo do Windows Forms no Visual Studio com o Visual Basic.
ms.date: 09/27/2019
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.devlang: vb
author: ornellaalt
ms.author: ornella
manager: jillfra
dev_langs:
- VB
ms.workload:
- multiple
ms.openlocfilehash: 89effbfd31e0194a88067a340c9332d888ef23df
ms.sourcegitcommit: b4e0cc76d94fe8cf6d238c4cc09512d17131a195
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/13/2020
ms.locfileid: "81224544"
---
# <a name="create-a-windows-forms-app-in-visual-studio-with-visual-basic"></a>Criar um aplicativo do Windows Forms no Visual Studio com o Visual Basic

Nesta introdução curta ao IDE (Ambiente de Desenvolvimento Integrado) do Visual Studio, você criará um aplicativo simples do Visual Basic que tem uma UI (interface do usuário) baseada no Windows.

::: moniker range="vs-2017"

Se você ainda não instalou o Visual Studio, vá para a página [de downloads](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) do Visual Studio para instalá-lo gratuitamente.

::: moniker-end

::: moniker range="vs-2019"

Se você ainda não instalou o Visual Studio, vá para a página [de downloads](https://visualstudio.microsoft.com/downloads) do Visual Studio para instalá-lo gratuitamente.

> [!NOTE]
> Algumas das capturas de tela neste tutorial usam o tema escuro. Se você não estiver usando o tema escuro, mas quiser usá-lo, confira a página [Personalizar o IDE e o Editor do Visual Studio](../ide/quickstart-personalize-the-ide.md) para saber como.

::: moniker-end

## <a name="create-a-project"></a>Criar um projeto

Primeiro, você criará um projeto de aplicativo do Visual Basic. O tipo de projeto inclui todos os arquivos de modelo que você precisará, mesmo sem adicionar nada.

::: moniker range="vs-2017"

1. Abra o Visual Studio 2017.

1. Na barra de menu superior, escolha **Arquivo** > **Novo** > **Projeto**.

1. Na caixa de diálogo **Novo Projeto**, no painel esquerdo, expanda a opção **Visual Basic** e, em seguida, escolha **Área de Trabalho do Windows**. No painel central, selecione **Aplicativo do Windows Forms (.NET Framework)**. Em seguida, dê o nome `HelloWorld` para o arquivo.

     Se o modelo de projeto **Aplicativo do Windows Forms (.NET Framework)** não for exibido, cancele a caixa de diálogo **Novo Projeto** e, na barra de menus superior, escolha **Ferramentas** > **Obter Ferramentas e Recursos**. O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho **Desenvolvimento de área de trabalho do .NET** e, em seguida, selecione **Modificar**.

     ![Carga de trabalho do .NET Core no Instalador do Visual Studio](../ide/media/install-dot-net-desktop-env.png)

::: moniker-end

::: moniker range="vs-2019"

1. Abra o Visual Studio 2019.

1. Na janela inicial, escolha **Criar um novo projeto**.

   ![Exibir a janela 'Criar um novo projeto'](../get-started/media/vs-2019/create-new-project-dark-theme.png)

1. Na **criação de uma nova** janela de projeto, escolha o modelo do Aplicativo de **formulários do Windows (.NET Framework)** para o Visual Basic.

   (Se preferir, você pode refinar sua pesquisa para chegar rapidamente ao modelo que deseja. Por exemplo, digite ou digite o *Aplicativo de Formulários do Windows* na caixa de pesquisa. Em seguida, escolha **Visual Basic** na lista de idiomas e escolha **o Windows** na lista Plataforma.)  

   ![Escolher o modelo do Visual Basic para o Aplicativo do Windows Forms (.NET Framework)](../get-started/visual-basic/media/vs-2019/vb-create-new-project-search-winforms-filtered.png)

   > [!NOTE]
   > Se você não encontrar o modelo do **Aplicativo do Windows Forms (.NET Framework)**, poderá instalá-lo a partir da janela **Criar um novo projeto**. Na mensagem **Não encontrou o que precisa?**, escolha o link **Instalar mais ferramentas e recursos**.
   >
   > ![O link 'Instalar mais ferramentas e recursos' da mensagem 'Não encontrou o que precisa?' na janela 'Criar novo projeto'](../get-started/media/vs-2019/not-finding-what-looking-for.png)
   >
   > Em seguida, no Instalador do Visual Studio, escolha Escolher a carga de trabalho de **desenvolvimento de área de trabalho do .NET**.
   >
   > ![Carga de trabalho do .NET Core no Instalador do Visual Studio](../ide/media/install-dot-net-desktop-env.png)
   >
   > Depois disso, escolha o botão **Modificar** no Instalador do Visual Studio. Pode ser solicitado que você salve seu trabalho; nesse caso, faça isso. Em seguida, escolha **Continuar** para instalar a carga de trabalho. Em seguida, retorne para a etapa 2 deste procedimento para "[Criar um projeto](#create-a-project)".

1. Na janela **Configurar seu novo projeto**, digite ou insira *OláMundo* na caixa **Nome do projeto**. Em seguida, escolha **Criar**.

   ![Na janela "Configurar seu novo projeto", dê ao projeto o nome 'OláMundo'](../get-started/visual-basic/media/vs-2019/vb-name-your-winform-project-helloworld.png)

   O Visual Studio abre seu novo projeto.

::: moniker-end

## <a name="create-the-application"></a>Criar o aplicativo

Depois de selecionar o modelo de projeto do Visual Basic e nomear seu arquivo, o Visual Studio abrirá um formulário para você. Um formulário é uma interface do usuário do Windows. Criaremos um aplicativo "Hello World" adicionando controles ao formulário e, em seguida, executaremos o aplicativo.

### <a name="add-a-button-to-the-form"></a>Adicionar um botão no formulário

1. Clique na **Caixa de Ferramentas** para abrir a janela suspensa da Caixa de Ferramentas.

     ![Clique na Caixa de Ferramentas para abrir a janela da Caixa de Ferramentas](../ide/media/vb-toolbox-toolwindow.png)

     (Se você não encontrar a opção suspensa **Caixa de Ferramentas**, ela poderá ser aberta da barra de menus. Para isso, **exibir** > **caixa de ferramentas**. Ou pressione **Ctrl**+**Alt**+**X**.)

1. Clique no ícone **Fixar** para encaixar a janela **Caixa de Ferramentas**.

     ![Clique no ícone Fixar para fixar a janela Caixa de Ferramentas no IDE](../ide/media/vb-pin-the-toolbox-window.png)

1. Clique no controle **Botão** e, em seguida, arraste-o para o formulário.

     ![Adicionar um botão no formulário](../ide/media/vb-add-a-button-to-form1.png)

1. Na seção **Aparência** (ou na seção **Fontes**) da janela **Propriedades**, digite `Click this`, depois pressione **Enter**.

     ![Adicionar texto no botão do formulário](../ide/media/vb-button-control-text.png)

     (Se você não encontrar a janela **Propriedades**, ela poderá ser aberta da barra de menus. Para isso, clique **em Exibir** > **janela propriedades**. Ou, pressione **F4**.)

1. Na seção **Design** da janela **Propriedades**, altere o nome de **Button1** para `btnClickThis` e, em seguida, pressione **Enter**.

     ![Adicionar uma função ao botão no formulário](../ide/media/vb-button-control-function.png)

   > [!NOTE]
   > Se você tiver alfabetizado a lista na janela **Propriedades,** **Button1** aparecerá na seção **(Databindings)** em vez disso.

### <a name="add-a-label-to-the-form"></a>Adicionar um rótulo ao formulário

Agora que adicionamos um controle de botão para criar uma ação, vamos adicionar um controle de rótulo para enviar o texto.

1. Selecione o controle **Rótulo** da janela **Caixa de Ferramentas** e, então, arraste-a para o formulário e solte-a abaixo do botão **Clique aqui**.

1. Na seção **Design** ou na seção **(DataBindings)** da janela **Propriedades,** altere o nome de **Label1** para `lblHelloWorld`e, em seguida, **pressione Enter**.

### <a name="add-code-to-the-form"></a>Adicionar código ao formulário

1. Na janela **Form1.vb &#91;Design&#93;**, clique duas vezes no botão **Clique aqui** para abrir a janela **Form1.vb**.

      (Como alternativa, você pode expandir **Form1.vb** no **Gerenciador de Soluções** e, em seguida, clicar em **Form1**.)

1. Na janela **Formulário1.vb,** entre as linhas **Sub privado** e **Sub final,** digite ou digite `lblHelloWorld.Text = "Hello World!"` conforme mostrado na captura de tela a seguir:

     ![Adicionar código ao formulário](../ide/media/vb-add-code-to-the-form.png)

## <a name="run-the-application"></a>Executar o aplicativo

1. Clique no botão **Iniciar** para executar o aplicativo.

     ![Clique em Iniciar para depurar e executar o aplicativo](../ide/media/vb-click-start-hello-world.png)

   Várias coisas acontecerão. No IDE do Visual Studio, a janela **Ferramentas de Diagnóstico** será aberta, e uma janela de **saída** também. Porém, fora do IDE, uma caixa de diálogo **Form1** será exibida. Ela incluirá o botão **Clique aqui** e o texto **Label1**.

1. Clique no botão **Clique aqui** na caixa de diálogo **Form1**. Observe que o texto **Label1** é alterado para **Olá, Mundo!**.

    ![Uma caixa de diálogo Form1 que inclui o texto Label1 ](../ide/media/vb-form1-dialog-hello-world.png)

1. Feche a caixa de diálogo **Form1** para parar de executar o aplicativo.

## <a name="next-steps"></a>Próximas etapas

Para saber mais, continue com o tutorial a seguir:

> [!div class="nextstepaction"]
> [Tutorial: Crie um visualizador de imagens](tutorial-1-create-a-picture-viewer.md)

## <a name="see-also"></a>Confira também

* [Mais tutoriais do Visual Basic](/visualstudio/get-started/visual-basic/)
* [Tutoriais sobre C#](/visualstudio/get-started/csharp/)
* [Tutoriais c++](/cpp/get-started/tutorial-console-cpp)
