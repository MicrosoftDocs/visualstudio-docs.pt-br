---
title: Criar seu primeiro aplicativo de console com o Visual Basic
description: Saiba como criar um aplicativo de console Olá, Mundo simples no Visual Studio com o Visual Basic, passo a passo.
ms.custom: seodec18
ms.date: 03/23/2019
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: quickstart
ms.devlang: vb
author: ornellaalt
ms.author: ornella
manager: jmartens
dev_langs:
- vb
ms.workload:
- multiple
ms.openlocfilehash: 34b412d254d0775b57f2c9befaae71ce25c6ae75
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/03/2021
ms.locfileid: "101683854"
---
# <a name="quickstart-create-your-first-console-app-in-visual-studio-with-visual-basic"></a>Guia de início rápido: criar seu primeiro aplicativo de console no Visual Studio com o Visual Basic

Nesta introdução de 5 a 10 minutos ao IDE (ambiente de desenvolvimento integrado) do Visual Studio, você criará um aplicativo simples do Visual Basic que é executado no console.

::: moniker range="vs-2017"

Se você ainda não instalou o Visual Studio, vá para a página de [downloads do Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) para instalá-lo gratuitamente.

::: moniker-end

::: moniker range="vs-2019"

Se você ainda não instalou o Visual Studio, vá para a página de [downloads do Visual Studio](https://visualstudio.microsoft.com/downloads) para instalá-lo gratuitamente.

::: moniker-end

## <a name="create-a-project"></a>Criar um projeto

Primeiro, você criará um projeto de aplicativo do Visual Basic. O tipo de projeto inclui todos os arquivos de modelo que você precisará, mesmo sem adicionar nada!

::: moniker range="vs-2017"

1. Abra o Visual Studio 2017.

2. Na barra de menus superior, escolha **arquivo** > **novo** > **projeto**.

3. Na caixa de diálogo **Novo Projeto**, no painel esquerdo, expanda **Visual Basic** e, em seguida, escolha **.NET Core**. No painel central, escolha **Aplicativo de Console (.NET Core)**. Em seguida, nomeie o projeto como *HelloWorld*.

   ![Modelo de projeto do aplicativo do console (.NET Core) na caixa de diálogo Novo projeto no IDE do Visual Studio](../ide/media/new-project-vb-dotnetcore-helloworld-console-app.png)

     Se você não vir o modelo de projeto do **Aplicativo de Console (.NET Core)**, clique no link **Abrir Instalador do Visual Studio** no painel esquerdo da caixa de diálogo **Novo Projeto**.

   ![Clique no link Abrir o Instalador do Visual Studio na caixa de diálogo Novo Projeto](../ide/media/vb-open-visual-studio-installer-hello-world.png)

     O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho **Desenvolvimento multiplaforma do .NET Core** e, em seguida, selecione **Modificar**.

     ![Carga de trabalho de desenvolvimento multiplaforma do .NET Core no Instalador do Visual Studio](../ide/media/dot-net-core-xplat-dev-workload.png)

::: moniker-end

::: moniker range="vs-2019"

> [!NOTE]
> Algumas das capturas de tela neste Início Rápido usam o tema escuro. Se você não estiver usando o tema escuro, mas quiser usá-lo, confira a página [Personalizar o IDE e o Editor do Visual Studio](quickstart-personalize-the-ide.md) para saber como.

1. Abra o Visual Studio 2019.

1. Na janela iniciar, escolha **criar um novo projeto**.

   ![Exibir a janela 'Criar um novo projeto'](../get-started/media/vs-2019/create-new-project-dark-theme.png)

1. Na janela **criar um novo projeto** , escolha **Visual Basic** na lista idioma. Em seguida, escolha **Windows** na lista de plataformas e **console** na lista de tipos de projeto.

   Depois de aplicar o idioma, a plataforma e os filtros de tipo de projeto, escolha o modelo de **aplicativo de console** e, em seguida, escolha **Avançar**.

   :::image type="content" source="../get-started/visual-basic/media/vs-2019/vb-create-new-project-console-net-core.png" alt-text="Escolha o modelo de Visual Basic para o aplicativo de console":::

   > [!NOTE]
   > Se você não vir o modelo de **aplicativo de console** , poderá instalá-lo na janela **criar um novo projeto** . Na mensagem **Não encontrou o que precisa?**, escolha o link **Instalar mais ferramentas e recursos**.
   >
   > ![O link 'Instalar mais ferramentas e recursos' da mensagem 'Não encontrou o que precisa?' na janela 'Criar novo projeto'](../get-started/media/vs-2019/not-finding-what-looking-for.png) 
   > 
   > Em seguida, no Instalador do Visual Studio, escolha a carga de trabalho de **desenvolvimento multiplataforma do .NET Core**.
   >
   > ![Carga de trabalho de desenvolvimento multiplaforma do .NET Core no Instalador do Visual Studio](../get-started/media/dot-net-core-xplat-dev-workload.png)
   >
   > Depois disso, escolha o botão **Modificar** no Instalador do Visual Studio. Pode ser solicitado que você salve seu trabalho; nesse caso, faça isso. Em seguida, escolha **Continuar** para instalar a carga de trabalho. Em seguida, retorne para a etapa 2 deste procedimento para "[Criar um projeto](#create-a-project)".

1. Na janela **Configurar seu novo projeto**, digite ou insira *WhatIsYourName* na caixa **Nome do projeto**. Em seguida, escolha **Avançar**.

   :::image type="content" source="../get-started/visual-basic/media/vs-2019/vb-name-your-project-whatname.png" alt-text="Na janela &quot;Configurar seu novo projeto&quot;, dê ao projeto o nome 'WhatIsYourName'":::

1. Na janela **informações adicionais** , o **.NET Core 3,1** já deve estar selecionado para sua estrutura de destino. Caso contrário, selecione **.NET Core 3,1**. Em seguida, escolha **criar**.

   :::image type="content" source="../get-started/visual-basic/media/vs-2019/vb-target-framework.png" alt-text="Na janela ' informações adicionais ', verifique se o .NET Core 3,1 está selecionado":::

   O Visual Studio abre seu novo projeto.

::: moniker-end

## <a name="create-the-application"></a>Criar o aplicativo

Depois de selecionar o modelo de projeto do Visual Basic e nomear o projeto, o Visual Studio criará um aplicativo “Olá, Mundo” simples para você. Ele chama o método <xref:System.Console.WriteLine%2A> para exibir a cadeia de caracteres literal "Hello World!" na janela do console.

![Exibir o código Olá, Mundo padrão do modelo](../ide/media/vb-console-helloworld-template.png)

Se clicar no botão **HelloWorld** no IDE, você poderá executar o programa no modo de depuração.

  ![Clique no botão Olá, Mundo para executar o programa no modo de depuração](../ide/media/vb-console-hello-world-button.png)

Quando você faz isso, a janela do console se torna visível somente por um momento antes de ser fechada. Isso acontece porque o método `Main` é encerrado após a execução de sua instrução única e, portanto, o aplicativo é encerrado.

### <a name="add-some-code"></a>Adicionar código

Vamos adicionar alguns códigos para pausar o aplicativo e, em seguida, solicitar a entrada do usuário.

1. Adicione o seguinte código imediatamente após a chamada ao método <xref:System.Console.WriteLine%2A>:

   ```vb
   Console.Write("Press any key to continue...")
   Console.ReadKey(true)
   ```

    Isso pausa o programa até que você pressione uma tecla.

2. Na barra de menus, selecione **Compilar** compilar  >  **solução**.

   Isso compila seu programa em uma IL (linguagem intermediária) que é convertida em um código binário por um compilador JIT (Just-In-Time).

## <a name="run-the-application"></a>Executar o aplicativo

1. Clique no botão **HelloWorld** na barra de ferramentas.

   ![Clique no botão Olá, Mundo para executar o programa da barra de ferramentas](../ide/media/vb-console-hello-world-button.png)

2. Pressione qualquer tecla para fechar a janela do console.

   ![Janela de console mostrando Olá, Mundo e Pressione qualquer tecla para continuar](../ide/media/vb-console-hello-world-press-any-key.png)

## <a name="next-steps"></a>Próximas etapas

Parabéns por concluir este Guia de Início Rápido! Esperamos que você tenha aprendido um pouco sobre o Visual Basic e sobre o IDE do Visual Studio. Para saber mais, continue com o tutorial a seguir.

> [!div class="nextstepaction"]
> [Introdução ao Visual Basic no Visual Studio](../get-started/visual-basic/tutorial-console.md)
