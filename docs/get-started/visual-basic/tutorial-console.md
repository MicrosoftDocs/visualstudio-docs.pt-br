---
title: 'Tutorial: Introdução ao Visual Basic'
description: Saiba como criar aplicativos de console do Visual Basic no Visual Studio, passo a passo.
ms.custom: seodec18, get-started
ms.date: 03/23/2019
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: tutorial
ms.devlang: vb
author: TerryGLee
ms.author: tglee
manager: jillfra
dev_langs:
- vb
ms.workload:
- multiple
ms.openlocfilehash: f394ea2775eede3424e4d6995a8e2065c5d986ef
ms.sourcegitcommit: 509fc3a324b7748f96a072d0023572f8a645bffc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2019
ms.locfileid: "58857587"
---
# <a name="tutorial-get-started-with-visual-basic-in-visual-studio"></a>Tutorial: Introdução ao Visual Basic no Visual Studio

Neste tutorial do VB (Visual Basic), você usará o Visual Studio para criar e executar alguns aplicativos de console diferentes e explorar alguns recursos do [IDE (ambiente de desenvolvimento integrado) do Visual Studio](visual-studio-ide.md) durante esse processo.

::: moniker range="vs-2017"

Se você ainda não tiver instalado o Visual Studio, acesse a página [Downloads do Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2017) para instalá-lo gratuitamente.

::: moniker-end

::: moniker range="vs-2019"

Se você ainda não tiver instalado o Visual Studio, acesse a página [Downloads do Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) para instalá-lo gratuitamente.

::: moniker-end

## <a name="create-a-project"></a>Criar um projeto

Primeiro, criaremos um projeto de aplicativo do Visual Basic. O tipo de projeto inclui todos os arquivos de modelo que você precisará, mesmo sem adicionar nada!

::: moniker range="vs-2017"

1. Abra o Visual Studio 2017.

2. Na barra de menus superior, escolha **Arquivo** > **Novo** > **Projeto**.

3. Na caixa de diálogo **Novo Projeto**, no painel esquerdo, expanda **Visual Basic** e, em seguida, escolha **.NET Core**. No painel central, escolha **Aplicativo de Console (.NET Core)**. Em seguida, nomeie o arquivo como *HelloWorld*.

   ![Modelo de projeto do aplicativo do console (.NET Core) na caixa de diálogo Novo projeto no IDE do Visual Studio](media/new-project-vb-dotnetcore-whatisyourname-console-app.png)

### <a name="add-a-workload-optional"></a>Adicionar uma carga de trabalho (opcional)

Se o modelo de projeto **Aplicativo do Console (.NET Core)** não for exibido, você poderá obtê-lo adicionando a carga de trabalho **Desenvolvimento .NET Core de multiplataforma**. Você pode adicionar essa carga de trabalho de uma das duas maneiras, dependendo de quais atualizações do Visual Studio 2017 estão instaladas no seu computador.

#### <a name="option-1-use-the-new-project-dialog-box"></a>Opção 1: Usar a caixa de diálogo Novo Projeto

1. Clique no link **Abrir o Instalador do Visual Studio** no painel esquerdo da caixa de diálogo **Novo Projeto**.

   ![Clique no link Abrir o Instalador do Visual Studio na caixa de diálogo Novo Projeto](../media/vs-open-visual-studio-installer-generic.png)

1. O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho **Desenvolvimento multiplaforma do .NET Core** e, em seguida, selecione **Modificar**.

   ![Carga de trabalho de desenvolvimento multiplataforma do .NET Core no Instalador do Visual Studio](../media/tutorial-aspnet-workload.png)

#### <a name="option-2-use-the-tools-menu-bar"></a>Opção 2: Usar a barra de menus Ferramentas

1. Cancele a caixa de diálogo **Novo Projeto**; em seguida, vá até a barra de menus superior e escolha **Ferramentas** > **Obter Ferramentas e Recursos**.

1. O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho **Desenvolvimento multiplaforma do .NET Core** e, em seguida, selecione **Modificar**.

::: moniker-end

::: moniker range="vs-2019"

> [!NOTE]
> Algumas das capturas de tela neste tutorial usam o tema escuro. Se você não estiver usando o tema escuro, mas quiser usá-lo, confira a página [Personalizar o IDE e o Editor do Visual Studio](../../ide/quickstart-personalize-the-ide.md) para saber como.

1. Abra o Visual Studio 2019.

1. Na tela Iniciar, selecione **Criar um novo projeto**.

   ![Exibir a janela 'Criar um novo projeto'](../../get-started/media/vs-2019/create-new-project-dark-theme.png)

1. Na janela **Criar um novo projeto**, insira ou digite *console* na caixa de pesquisa. Em seguida, escolha **Visual Basic** na lista Linguagem de programação e, em seguida, escolha **Windows** na lista Plataforma. 

   Depois de aplicar os filtros de linguagem de programação e plataforma, escolha o modelo **Aplicativo de Console (.NET Core)** e, em seguida, escolha **Avançar**.

   ![Escolha o modelo de Visual Basic para o Aplicativo de Console (.NET Framework)](./media/vs-2019/vb-create-new-project-search-console-net-core-filtered.png)

   > [!NOTE]
   > Se não vir o modelo **Aplicativo de Console (.NET Core)**, você poderá instalá-lo da janela **Criar um novo projeto**. Na mensagem **Não encontrou o que precisa?**, escolha o link **Instalar mais ferramentas e recursos**.
   >
   > ![O link 'Instalar mais ferramentas e recursos' da mensagem 'Não encontrou o que precisa?' na janela 'Criar novo projeto'](../../get-started/media/vs-2019/not-finding-what-looking-for.png) 
   > 
   > Em seguida, no Instalador do Visual Studio, escolha a carga de trabalho de **desenvolvimento multiplataforma do .NET Core**.
   >
   > ![Carga de trabalho de desenvolvimento multiplataforma do .NET Core no Instalador do Visual Studio](../../get-started/media/dot-net-core-xplat-dev-workload.png)
   >
   > Depois disso, escolha o botão **Modificar** no Instalador do Visual Studio. Pode ser solicitado que você salve seu trabalho; nesse caso, faça isso. Em seguida, escolha **Continuar** para instalar a carga de trabalho. Em seguida, retorne para a etapa 2 deste procedimento para "[Criar um projeto](#create-a-project)".

1. Na janela **Configurar seu novo projeto**, digite ou insira *WhatIsYourName* na caixa **Nome do projeto**. Em seguida, escolha **Criar**.

   ![Na janela "Configurar seu novo projeto", dê ao projeto o nome 'WhatIsYourName'](./media/vs-2019/vb-name-your-project-whatname.png)

   O Visual Studio abre seu novo projeto.

::: moniker-end

## <a name="create-a-what-is-your-name-application"></a>Criar um aplicativo de “Qual é o seu nome”

Vamos criar um aplicativo que solicita o nome e o exibe juntamente com a data e a hora. Veja como:

 ::: moniker range="vs-2017"

1. Se ainda não estiver aberto, abra seu projeto *WhatIsYourName*.

1. Insira o código do Visual Basic a seguir imediatamente após o colchete de abertura que segue a linha `Sub Main(args As String())` e antes da linha `End Sub`:

     ```vb
     Console.WriteLine(vbCrLf + "What is your name? ")
     Dim name = Console.ReadLine()
     Dim currentDate = DateTime.Now
     Console.WriteLine($"{vbCrLf}Hello, {name}, on {currentDate:d} at {currentDate:t}")
     Console.Write(vbCrLf + "Press any key to exit... ")
     Console.ReadKey(True)
    ```

    Esse código substitui as instruções <xref:System.Console.WriteLine%2A>, <xref:System.Console.Write%2A> e <xref:System.Console.ReadKey%2A> existentes.

   ![Janela de código mostrando o código Qual é o seu nome](./media/vs-2019/vb-codewindow-what-name-dark.png)

1. Quando a janela do console é aberta, digite seu nome. A janela do console deve ser semelhante à captura de tela a seguir:

   ![Janela do console mostrando Qual é o seu nome, a data e hora, e Pressione qualquer tecla para continuar a mensagem](media/vb-console-what-name.png)

1. Pressione qualquer tecla para fechar a janela de console.

::: moniker-end

::: moniker range="vs-2019"

1. No projeto *WhatIsYourName*, insira o código do Visual Basic a seguir imediatamente após o colchete de abertura que segue a linha `Sub Main(args As String())` e antes da linha `End Sub`:

     ```vb
     Console.WriteLine(vbCrLf + "What is your name? ")
     Dim name = Console.ReadLine()
     Dim currentDate = DateTime.Now
     Console.WriteLine($"{vbCrLf}Hello, {name}, on {currentDate:d} at {currentDate:t}")
     Console.Write(vbCrLf + "Press any key to exit... ")
     Console.ReadKey(True)
    ```

    Esse código substitui as instruções <xref:System.Console.WriteLine%2A>, <xref:System.Console.Write%2A> e <xref:System.Console.ReadKey%2A> existentes.

   ![Janela de código mostrando o código Qual é o seu nome](./media/vs-2019/vb-codewindow-what-name-dark.png)

1. Quando a janela do console é aberta, digite seu nome. A janela do console deve ser semelhante à captura de tela a seguir:

   ![Janela do console mostrando Qual é o seu nome, a data e hora, e Pressione qualquer tecla para continuar a mensagem](media/vb-console-what-name.png)

1. Pressione qualquer tecla para fechar a janela de console.

 ::: moniker-end

## <a name="create-a-calculate-this-application"></a>Criar um aplicativo “Calcular isso”

::: moniker range="vs-2017"

1. Abra o Visual Studio 2017 e, na barra de menus superior, escolha **Arquivo** > **Novo** > **Projeto**.

1. Na caixa de diálogo **Novo Projeto**, no painel esquerdo, expanda **Visual Basic** e, em seguida, escolha **.NET Core**. No painel central, escolha **Aplicativo de Console (.NET Core)**. Em seguida, nomeie o arquivo como *CalculateThis*.

1. Insira o código a seguir entre as linhas `Module Program` e `End Module`:

   ```vb
   Public num1 As Integer
   Public num2 As Integer
   Public answer As Integer
   Sub Main()
       Console.WriteLine("Type a number and press Enter")
       num1 = Console.ReadLine()
       Console.WriteLine("Type another number to add to it and press Enter")
       num2 = Console.ReadLine()
       answer = num1 + num2
       Console.WriteLine("The answer is " & answer)
       Console.ReadLine()
   End Sub
   ```

   Sua janela de código deve se parecer com a captura de tela a seguir:

   ![Janela de código mostrando o código CalculateThis](media/vb-codewindow-calculate-this.png)

1. Clique em **CalculateThis** para executar o programa. A janela do console deve ser semelhante à captura de tela a seguir:

    ![Janela do console mostrando o aplicativo CalculateThis, que inclui solicitações de ações a serem tomadas.](media/vb-console-calculate-this.png)

::: moniker-end 

::: moniker range="vs-2019"

1. Na tela Iniciar, selecione **Criar um novo projeto**. 

1. Na janela **Criar um novo projeto**, insira ou digite *console* na caixa de pesquisa. Em seguida, escolha **Visual Basic** na lista Linguagem de programação e, em seguida, escolha **Windows** na lista Plataforma. 

1. Depois de aplicar os filtros de linguagem de programação e plataforma, escolha o modelo **Aplicativo de Console (.NET Core)** e, em seguida, escolha **Avançar**.

   Em seguida, na janela **Configurar seu novo projeto**, digite ou insira *WhatIsYourName* na caixa **Nome do projeto**. Em seguida, escolha **Criar**.

1. Insira o código a seguir entre as linhas `Module Program` e `End Module`:

   ```vb
   Public num1 As Integer
   Public num2 As Integer
   Public answer As Integer
   Sub Main()
       Console.WriteLine("Type a number and press Enter")
       num1 = Console.ReadLine()
       Console.WriteLine("Type another number to add to it and press Enter")
       num2 = Console.ReadLine()
       answer = num1 + num2
       Console.WriteLine("The answer is " & answer)
       Console.ReadLine()
   End Sub
   ```

   Sua janela de código deve se parecer com a captura de tela a seguir:

   ![Janela de código mostrando o código CalculateThis](media/vb-codewindow-calculate-this.png)

1. Clique em **CalculateThis** para executar o programa. A janela do console deve ser semelhante à captura de tela a seguir:

    ![Janela do console mostrando o aplicativo CalculateThis, que inclui solicitações de ações a serem tomadas.](media/vb-console-calculate-this.png)

::: moniker-end

## <a name="quick-answers-faq"></a>Perguntas frequentes com respostas rápidas

Aqui estão algumas perguntas frequentes rápidas para destacar alguns conceitos principais.

### <a name="what-is-visual-basic"></a>O que é o Visual Basic?

Visual Basic é uma linguagem de programação fortemente tipada projetada para ser fácil de aprender. Ele é derivado do BASIC, cuja abreviação significa “Código de instrução simbólico com várias finalidades para iniciantes”.

### <a name="what-is-visual-studio"></a>O que é o Visual Studio?

Visual Studio é um pacote de desenvolvimento integrado de ferramentas de produtividade para desenvolvedores. Pense nele como um programa que você pode usar para criar programas e aplicativos.

### <a name="what-is-a-console-app"></a>O que é um aplicativo do console?

Um aplicativo de console obtém a entrada e exibe a saída em uma janela de linha de comando, também conhecida como um console.

### <a name="what-is-net-core"></a>O que é o .NET Core?

O .NET Core é o próximo passo na evolução do .NET Framework. Enquanto o .NET Framework pode compartilhar o código entre linguagens de programação, o .NET Core agrega a capacidade de compartilhar o código entre plataformas. Melhor ainda, ele é um software livre. (Tanto o .NET Framework quanto o .NET Core incluem bibliotecas de funcionalidade predefinidas, bem como um CLR (Common Language Runtime), que atua como uma máquina virtual na qual o código será executado.)

## <a name="next-steps"></a>Próximas etapas

Parabéns por concluir este tutorial. Para saber ainda mais, confira o tutorial a seguir.

> [!div class="nextstepaction"]
> [Criar uma biblioteca com o Visual Basic e o SDK do .NET Core no Visual Studio](/dotnet/core/tutorials/vb-library-with-visual-studio)

## <a name="see-also"></a>Consulte também

* [Instruções passo a passo sobre a linguagem do Visual Basic](/dotnet/visual-basic/walkthroughs)
* [Referência da linguagem Visual Basic](/dotnet/visual-basic/language-reference/index)
* [IntelliSense para arquivos de código do Visual Basic](../../ide/visual-basic-specific-intellisense.md)
