---
title: 'Criar um aplicativo Windows Forms com C #'
description: Saiba como criar um aplicativo Windows Forms no Visual Studio com C#, passo a passo.
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
ms.openlocfilehash: 26f13d12324beb0e414761ce2d79297767c5d708
ms.sourcegitcommit: 6d88913a8b5a9e5eda01d3f95205b4d138f440f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/13/2021
ms.locfileid: "107297113"
---
# <a name="create-a-windows-forms-app-in-visual-studio-with-c"></a>Criar um aplicativo Windows Forms no Visual Studio com C\#

Nesta breve introdução ao IDE (ambiente de desenvolvimento integrado) do Visual Studio, você criará um aplicativo C# simples que tem uma interface do usuário baseada no Windows (IU).

::: moniker range="vs-2017"

Se você ainda não instalou o Visual Studio, vá para a página de [downloads do Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) para instalá-lo gratuitamente.

::: moniker-end

::: moniker range="vs-2019"

Se você ainda não instalou o Visual Studio, vá para a página de [downloads do Visual Studio](https://visualstudio.microsoft.com/downloads) para instalá-lo gratuitamente.

> [!NOTE]
> Algumas das capturas de tela neste tutorial usam o tema escuro. Se você não estiver usando o tema escuro, mas quiser usá-lo, confira a página [Personalizar o IDE e o Editor do Visual Studio](../ide/quickstart-personalize-the-ide.md) para saber como.

::: moniker-end

## <a name="create-a-project"></a>Criar um projeto

Primeiro, você criará um projeto de aplicativo em C#. O tipo de projeto inclui todos os arquivos de modelo que você precisará, mesmo sem adicionar nada.

::: moniker range="vs-2017"

1. Abra o Visual Studio 2017.

1. Na barra de menus superior, escolha **arquivo** > **novo** > **projeto**.

1. Na caixa de diálogo **novo projeto** no painel esquerdo, expanda **Visual C#** e escolha área de **trabalho do Windows**. No painel central, selecione **Aplicativo do Windows Forms (.NET Framework)**. Em seguida, dê o nome `HelloWorld` para o arquivo.

     Se o modelo de projeto **Aplicativo do Windows Forms (.NET Framework)** não for exibido, cancele a caixa de diálogo **Novo Projeto** e, na barra de menus superior, escolha **Ferramentas** > **Obter Ferramentas e Recursos**. O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho **Desenvolvimento de área de trabalho do .NET** e, em seguida, selecione **Modificar**.

     ![Carga de trabalho do .NET Core no Instalador do Visual Studio](../ide/media/install-dot-net-desktop-env.png)

::: moniker-end

::: moniker range="vs-2019"

1. Abra o Visual Studio 2019.

1. Na janela iniciar, escolha **criar um novo projeto**.

   ![Exibir a janela 'Criar um novo projeto'](../get-started/media/vs-2019/create-new-project-dark-theme.png)

1. Na janela **criar um novo projeto** , escolha o modelo **aplicativo de Windows Forms (.NET Framework)** para C#.

   (Se preferir, você pode refinar sua pesquisa para obter rapidamente o modelo desejado. Por exemplo, digite ou digite *Windows Forms aplicativo* na caixa de pesquisa. Em seguida, escolha **C#** na lista idioma e, em seguida, escolha **Windows** na lista plataforma.)  

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

1. Na janela **Configurar seu novo projeto**, digite ou insira *OláMundo* na caixa **Nome do projeto**. Em seguida, escolha **criar**.

   ![Na janela "Configurar seu novo projeto", dê ao projeto o nome 'OláMundo'](../get-started/csharp/media/vs-2019/csharp-name-your-winform-project-helloworld.png)

   O Visual Studio abre seu novo projeto.

::: moniker-end

## <a name="create-the-application"></a>Criar o aplicativo

Depois de selecionar o modelo de projeto C# e nomear o arquivo, o Visual Studio abre um formulário para você. Um formulário é uma interface do usuário do Windows. Vamos criar um aplicativo "Olá, Mundo" adicionando controles ao formulário e, em seguida, executaremos o aplicativo.

### <a name="add-a-button-to-the-form"></a>Adicionar um botão no formulário

1. Escolha **Caixa de ferramentas** para abrir a janela de submenu Caixa de Ferramentas.

     ![Escolha a caixa de ferramentas para abrir a janela caixa de ferramentas](../ide/media/csharp-toolbox-toolwindow.png)

     (Se você não encontrar a opção suspensa **Caixa de Ferramentas**, ela poderá ser aberta da barra de menus. Para fazer isso, **exiba** a  >  **caixa de ferramentas**. Ou pressione **Ctrl** + **ALT** + **X**.)

1. Escolha o ícone de **pino** para encaixar a janela caixa de **ferramentas** .

     ![Escolha o ícone de pino para fixar a janela caixa de ferramentas no IDE](../ide/media/vb-pin-the-toolbox-window.png)

1. Escolha o controle **botão** e arraste-o para o formulário.

     ![Adicionar um botão no formulário](../ide/media/csharp-add-button-form1.png)

1. Na janela **Propriedades** , localize o **texto**, altere o nome de **Button1** para `Click this` e pressione **Enter**.

     ![Adicionar texto no botão do formulário](../ide/media/vb-button-control-text.png)

     (Se você não encontrar a janela **Propriedades**, ela poderá ser aberta da barra de menus. Para fazer isso, escolha **Exibir**  >  **janela de propriedades**. Ou pressione **F4**.)

1. Na seção **Design** da janela **Propriedades**, altere o nome de **Button1** para `btnClickThis` e, em seguida, pressione **Enter**.

     ![Adicionar uma função ao botão no formulário](../ide/media/vb-button-control-function.png)

   > [!NOTE]
   > Se você tiver em ordem alfabética a lista na janela **Propriedades** , o **Button1** aparecerá na seção **(DataBindings)** , em vez disso.

### <a name="add-a-label-to-the-form"></a>Adicionar um rótulo ao formulário

Agora que adicionamos um controle de botão para criar uma ação, vamos adicionar um controle de rótulo para enviar o texto.

1. Selecione o controle **Rótulo** da janela **Caixa de Ferramentas** e, então, arraste-a para o formulário e solte-a abaixo do botão **Clique aqui**.

1. Na seção **design** ou na seção **(DataBindings)** da janela **Propriedades** , altere o nome de **Label1** para `lblHelloWorld` e pressione **Enter**.

### <a name="add-code-to-the-form"></a>Adicionar código ao formulário

1. Na janela **Form1. cs &#91;Design&#93;** **, clique duas vezes no botão para** abrir a janela **Form1. cs** .

      (Como alternativa, você pode expandir **Form1. cs** em **Gerenciador de soluções** e, em seguida, escolher **Form1**.)

1. Na janela **Form1. cs** , após a linha **void particular** , digite ou insira, `lblHelloWorld.Text = "Hello World!";` conforme mostrado na seguinte captura de tela:

     ![Adicionar código ao formulário](../get-started/csharp/media/csharp-winforms-add-code.png)

## <a name="run-the-application"></a>Executar o aplicativo

1. Escolha o botão **Iniciar** para executar o aplicativo.

     ![Escolha Iniciar para depurar e executar o aplicativo](../ide/media/vb-click-start-hello-world.png)

   Várias coisas acontecerão. No IDE do Visual Studio, a janela **Ferramentas de Diagnóstico** será aberta, e uma janela de **saída** também. Porém, fora do IDE, uma caixa de diálogo **Form1** será exibida. Ela incluirá o botão **Clique aqui** e o texto **Label1**.

1. Escolha o **botão na caixa de** diálogo **Form1** . Observe que o texto **Label1** é alterado para **Olá, Mundo!**.

    ![Uma caixa de diálogo Form1 que inclui o texto Label1 ](../ide/media/vb-form1-dialog-hello-world.png)

1. Feche a caixa de diálogo **Form1** para interromper a execução do aplicativo.

## <a name="next-steps"></a>Próximas etapas

Para saber mais, continue com o tutorial a seguir:

> [!div class="nextstepaction"]
> [Tutorial: Criar um visualizador de imagens](tutorial-1-create-a-picture-viewer.md)

## <a name="see-also"></a>Confira também

* [Mais tutoriais sobre C#](../get-started/csharp/index.yml)
* [Tutoriais de Visual Basic](../get-started/visual-basic/index.yml)
* [Tutoriais do C++](/cpp/get-started/tutorial-console-cpp)