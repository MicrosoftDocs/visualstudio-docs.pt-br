---
title: 'Criar um Windows Forms com C #'
description: Saiba como criar um Windows Forms em Visual Studio com C#, passo a passo.
ms.date: 09/26/2019
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.devlang: CSharp
author: j-martens
ms.author: jmartens
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- multiple
ms.openlocfilehash: 0efdb7d35549a32e1151a134ce3a665337bb27ce
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112308305"
---
# <a name="create-a-windows-forms-app-in-visual-studio-with-c"></a>Criar um Windows Forms aplicativo em Visual Studio com C\#

Nesta breve introdução ao IDE (ambiente de desenvolvimento integrado) do Visual Studio, você criará um aplicativo C# simples que tem uma interface do usuário baseada no Windows.

::: moniker range="vs-2017"

Se você ainda não tiver instalado o Visual Studio, acesse a página [Visual Studio downloads](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) para instalá-lo gratuitamente.

::: moniker-end

::: moniker range="vs-2019"

Se você ainda não tiver instalado o Visual Studio, acesse a página [Visual Studio downloads](https://visualstudio.microsoft.com/downloads) para instalá-lo gratuitamente.

> [!NOTE]
> Algumas das capturas de tela neste tutorial usam o tema escuro. Se você não estiver usando o tema escuro, mas quiser usá-lo, confira a página [Personalizar o IDE e o Editor do Visual Studio](../ide/quickstart-personalize-the-ide.md) para saber como.

::: moniker-end

::: moniker range="vs-2022"

Se você ainda não tiver instalado o Visual Studio, acesse a página de downloads do [Visual Studio 2022 Preview](https://visualstudio.microsoft.com/vs/preview/vs2022) para instalá-lo gratuitamente.

> [!NOTE]
> Algumas das capturas de tela neste tutorial usam o tema escuro. Se você não estiver usando o tema escuro, mas quiser usá-lo, confira a página [Personalizar o IDE e o Editor do Visual Studio](../ide/quickstart-personalize-the-ide.md) para saber como.

::: moniker-end

## <a name="create-a-project"></a>Criar um projeto

Primeiro, você criará um projeto de aplicativo em C#. O tipo de projeto inclui todos os arquivos de modelo que você precisará, mesmo sem adicionar nada.

::: moniker range="vs-2017"

1. Abra o Visual Studio 2017.

1. Na barra de menus superior, escolha **Arquivo** > **Novo** > **Projeto**.

1. Na caixa **de diálogo** Novo Projeto no painel esquerdo, expanda **Visual C#** e escolha **Área de Trabalho do Windows.** No painel central, selecione **Aplicativo do Windows Forms (.NET Framework)**. Em seguida, dê o nome `HelloWorld` para o arquivo.

     Se o modelo de projeto **Aplicativo do Windows Forms (.NET Framework)** não for exibido, cancele a caixa de diálogo **Novo Projeto** e, na barra de menus superior, escolha **Ferramentas** > **Obter Ferramentas e Recursos**. O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho **Desenvolvimento de área de trabalho do .NET** e, em seguida, selecione **Modificar**.

     ![Carga de trabalho do .NET Core no Instalador do Visual Studio](../ide/media/install-dot-net-desktop-env.png)

::: moniker-end

::: moniker range=">=vs-2019"

1. Abra o Visual Studio.

1. Na janela inicial, escolha **Criar um novo projeto.**

   ![Exibir a janela 'Criar um novo projeto'](../get-started/media/vs-2019/create-new-project-dark-theme.png)

1. Na janela **Criar um novo projeto,** escolha o **modelo Windows Forms aplicativo (.NET Framework)** para C#.

   (Se preferir, refine sua pesquisa para obter rapidamente o modelo que deseja. Por exemplo, insira ou digite *Windows Forms App* na caixa de pesquisa. Em seguida, **escolha C#** na lista Idioma e, em seguida, **escolha Windows** na lista Plataforma.)  

   ![Escolha o modelo C# para o aplicativo Windows Forms (.NET Framework)](../get-started/csharp/media/vs-2019/csharp-create-new-winforms-project-nonfiltered.png)

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

   ![Na janela "Configurar seu novo projeto", dê ao projeto o nome 'OláMundo'](../get-started/csharp/media/vs-2019/csharp-name-your-winform-project-helloworld.png)

   O Visual Studio abre seu novo projeto.

::: moniker-end

## <a name="create-the-application"></a>Criar o aplicativo

Depois de selecionar o modelo de projeto C# e nomear o arquivo, Visual Studio abrirá um formulário para você. Um formulário é uma interface do usuário do Windows. Criaremos um aplicativo "Olá, Mundo" adicionando controles ao formulário e, em seguida, executaremos o aplicativo.

### <a name="add-a-button-to-the-form"></a>Adicionar um botão no formulário

1. Escolha **Caixa de ferramentas** para abrir a janela de submenu Caixa de Ferramentas.

     ![Escolha a Caixa de Ferramentas para abrir a janela Caixa de Ferramentas](../ide/media/csharp-toolbox-toolwindow.png)

     (Se você não encontrar a opção suspensa **Caixa de Ferramentas**, ela poderá ser aberta da barra de menus. Para fazer isso, **Veja Caixa**  >  **de Ferramentas**. Ou pressione **Ctrl** + **Alt** + **X**.)

1. Escolha o **ícone Fixar** para encaixar a janela **Caixa de** Ferramentas.

     ![Escolha o ícone Fixar para fixar a janela Caixa de Ferramentas no IDE](../ide/media/vb-pin-the-toolbox-window.png)

1. Escolha o **controle Botão** e arraste-o para o formulário.

     ![Adicionar um botão no formulário](../ide/media/csharp-add-button-form1.png)

1. Na janela **Propriedades,** **localize Texto**, altere o nome de **Button1** para `Click this` e pressione **Enter**.

     ![Adicionar texto no botão do formulário](../ide/media/vb-button-control-text.png)

     (Se você não encontrar a janela **Propriedades**, ela poderá ser aberta da barra de menus. Para fazer isso, escolha **Exibir**  >  **Janela Propriedades**. Ou pressione **F4**.)

1. Na seção **Design** da janela **Propriedades**, altere o nome de **Button1** para `btnClickThis` e, em seguida, pressione **Enter**.

     ![Adicionar uma função ao botão no formulário](../ide/media/vb-button-control-function.png)

   > [!NOTE]
   > Se você tiver alfabético a lista na **janela** Propriedades, **Button1** será exibido na seção **(DataBindings).**

### <a name="add-a-label-to-the-form"></a>Adicionar um rótulo ao formulário

Agora que adicionamos um controle de botão para criar uma ação, vamos adicionar um controle de rótulo para enviar o texto.

1. Selecione o controle **Rótulo** da janela **Caixa de Ferramentas** e, então, arraste-a para o formulário e solte-a abaixo do botão **Clique aqui**.

1. Na seção **Design** ou **na seção (DataBindings)** da janela Propriedades, altere o nome de **Label1** para e pressione  `lblHelloWorld` **Enter**.

### <a name="add-code-to-the-form"></a>Adicionar código ao formulário

1. Na janela &#91;Design&#93;**Form1.cs,** clique duas vezes  no botão Clique neste botão para abrir a janela **Form1.cs.**

      (Como alternativa, você pode expandir **Form1.cs** **no Gerenciador de Soluções** e, em seguida, **escolher Form1**.)

1. Na janela **Form1.cs,** após a linha **privada void,** digite ou insira conforme `lblHelloWorld.Text = "Hello World!";` mostrado na seguinte captura de tela:

     ![Adicionar código ao formulário](../get-started/csharp/media/csharp-winforms-add-code.png)

## <a name="run-the-application"></a>Executar o aplicativo

1. Escolha o **botão Iniciar** para executar o aplicativo.

     ![Escolha Iniciar para depurar e executar o aplicativo](../ide/media/vb-click-start-hello-world.png)

   Várias coisas acontecerão. No IDE do Visual Studio, a janela **Ferramentas de Diagnóstico** será aberta, e uma janela de **saída** também. Porém, fora do IDE, uma caixa de diálogo **Form1** será exibida. Ela incluirá o botão **Clique aqui** e o texto **Label1**.

1. Escolha o **botão Clique neste** na caixa de diálogo **Form1.** Observe que o texto **Label1** é alterado para **Olá, Mundo!**.

    ![Uma caixa de diálogo Form1 que inclui o texto Label1 ](../ide/media/vb-form1-dialog-hello-world.png)

1. Feche a **caixa de diálogo Form1** para interromper a execução do aplicativo.

## <a name="next-steps"></a>Próximas etapas

Para saber mais, continue com o tutorial a seguir:

> [!div class="nextstepaction"]
> [Tutorial: Criar um visualizador de imagens](tutorial-1-create-a-picture-viewer.md)

## <a name="see-also"></a>Confira também

* [Mais tutoriais do C#](../get-started/csharp/index.yml)
* [Visual Basic tutoriais](../get-started/visual-basic/index.yml)
* [Tutoriais do C++](/cpp/get-started/tutorial-console-cpp)