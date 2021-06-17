---
title: 'Início rápido: tour pelo IDE do Visual Studio'
description: Saiba mais sobre algumas das janelas, menus e outros recursos de interface do usuário do IDE (ambiente de desenvolvimento integrado) do Visual Studio.
ms.custom: acquisition
titleSuffix: ''
ms.date: 03/02/2021
ms.topic: quickstart
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1f10c3fcca5d87f8371d1373314406cf4aa47ec3
ms.sourcegitcommit: 1f27f33852112702ee35fbc0c02fba37899e4cf5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2021
ms.locfileid: "112113223"
---
# <a name="quickstart-first-look-at-the-visual-studio-ide"></a>Início rápido: Introdução ao IDE do Visual Studio

Nesta introdução de 5 a 10 minutos ao IDE (Ambiente de Desenvolvimento Integrado) do Visual Studio, faremos um tour em algumas janelas, menus e em outros recursos de interface do usuário.

::: moniker range="vs-2017"

Se você ainda não instalou o Visual Studio, vá para a página de [downloads do Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) para instalá-lo gratuitamente.

::: moniker-end

::: moniker range=">=vs-2019"

Se você ainda não instalou o Visual Studio, vá para a página de [downloads do Visual Studio](https://visualstudio.microsoft.com/downloads) para instalá-lo gratuitamente.

::: moniker-end

::: moniker range="vs-2017"

## <a name="start-page"></a>Start Page

A primeira coisa que você verá depois de abrir o Visual Studio provavelmente será a **Página Inicial**. A **Página Inicial** foi projetada como um "hub" para ajudá-lo a localizar os comandos e os arquivos de projeto necessários com mais rapidez. A seção **Recentes** exibe projetos e pastas em que você trabalhou recentemente. Em **Novo projeto**, clique em um link para abrir a caixa de diálogo **Novo Projeto** ou, em **Abrir**, abra uma pasta ou um projeto de código existente. À direita está um feed das notícias mais recentes do desenvolvedor.

![Página Inicial no Visual Studio](media/start-page.png)

Se você fechar a **Página Inicial** e desejar vê-la novamente, será possível reabri-la no menu **Arquivo**.

![Menu Arquivo no Visual Studio](media/quickstart-IDE-file-menu-large.png)

::: moniker-end

::: moniker range=">=vs-2019"

## <a name="start-window"></a>Janela de início

A primeira coisa que você verá depois de abrir o Visual Studio é a janela de início. A janela de início foi projetada para ajudar você a "acessar o código" mais rapidamente. Ela tem opções para clonar o código ou fazer check-out dele, abrir um projeto ou uma solução existente, criar um projeto ou simplesmente abrir uma pasta que contenha alguns arquivos de código.

[![Iniciar janela no Visual Studio 2019](media/vs-2019/start-window-labeled.png)](media/vs-2019/start-window-labeled.png#lightbox)

Se essa for a primeira vez que você estiver usando o Visual Studio, sua lista de projetos recentes estará vazia.

Se você trabalhar com bases de código não baseadas no MSBuild, você usará a opção **Abrir uma pasta local** para abrir o código no Visual Studio. Para obter mais informações, consulte [Desenvolver código no Visual Studio sem projetos nem soluções](develop-code-in-visual-studio-without-projects-or-solutions.md). Caso contrário, você poderá criar um projeto ou clonar um projeto de um provedor de origem como o GitHub ou o Azure DevOps.

A opção **Continuar sem código** apenas abre o ambiente de desenvolvimento do Visual Studio sem nenhum projeto ou código específico carregado. Escolha essa opção para ingressar em uma sessão do [Live Share](/visualstudio/liveshare/) ou anexar a um processo para depuração. Pressione também **Esc** para fechar a janela de início e abrir o IDE.

::: moniker-end

## <a name="create-a-project"></a>Criar um projeto

Para continuar explorando os recursos do Visual Studio, vamos criar um projeto.

::: moniker range="vs-2017"

1. Na **Página Inicial**, na caixa de pesquisa de **Novo projeto**, digite **console** para filtrar da lista de tipos de projeto aqueles que contêm "console" no nome.

   ![Pesquisar modelos de projeto na Página Inicial do Visual Studio](media/start-page-search-templates.png)

   O Visual Studio fornece vários tipos de modelos de projeto que ajudam você a começar a codificar rapidamente. Escolha um modelo de projeto de **Aplicativo de console (.NET Core)** do C#. (Como alternativa, se você for um desenvolvedor de Visual Basic, C++, JavaScript ou outra linguagem, fique à vontade para criar um projeto em uma dessas linguagens. A interface do usuário que veremos é semelhante em todas as linguagens de programação.)

1. Na caixa de diálogo **Novo Projeto** exibida, aceite o nome de projeto padrão e escolha **OK**.

::: moniker-end

::: moniker range=">=vs-2019"

1. Na janela iniciar, escolha **criar um novo projeto**.

    :::image type="content" source="../get-started/media/vs-2019/start-window-create-new-project.png" alt-text="Captura de tela da janela ' criar um novo projeto ' no Visual Studio 2019.":::

   A janela **Criar um novo projeto** é aberta e mostra diversos *modelos* de projeto. Um modelo contém os arquivos básicos e as configurações necessárias para um determinado tipo de projeto.

   Aqui, você pode pesquisar, filtrar e, em seguida, escolher um modelo de projeto. Ela também mostra uma lista dos modelos de projeto usados recentemente por você.

1. Na caixa de pesquisa na parte superior, digite **console** para filtrar a lista de tipos de projeto àqueles que contêm "console" no nome. Refine ainda mais os resultados da pesquisa selecionando **C#** (ou outro idioma de sua escolha) na lista suspensa **todos os idiomas** .

    :::image type="content" source="media/vs-2019/create-new-project.png" alt-text="Captura de tela da janela ' criar um novo projeto ' no Visual Studio 2019, em que você seleciona o modelo desejado.":::

1. Se você selecionou C#, Visual Basic ou F # como seu idioma, selecione o modelo de **aplicativo de console** e, em seguida, escolha **Avançar**. (Se você tiver selecionado uma linguagem diferente, escolha qualquer modelo. A interface do usuário que veremos é semelhante em todas as linguagens de programação.)

1. Na janela **configurar seu novo projeto** , aceite o nome e o local do projeto padrão e escolha **Avançar**.

    :::image type="content" source="media/vs-2019/configure-new-project-console.png" alt-text="Captura de tela da janela ' configurar um novo projeto ' no Visual Studio 2019, em que você insere o nome do projeto.":::

1. Na janela **informações adicionais** , verifique se **.NET Core 3,1** aparece no menu suspenso **estrutura de destino** e, em seguida, clique em **criar**.

    :::image type="content" source="../get-started/media/vs-2019/create-project-additional-info.png" alt-text="Captura de tela da janela ' informações adicionais ' no Visual Studio 2019, onde você seleciona a versão do .NET Core Framework que deseja.":::

::: moniker-end

   O projeto é criado e um arquivo chamado *Program.cs* é aberto na janela **Editor**. O **Editor** mostra o conteúdo dos arquivos e é nele que você fará a maior parte do trabalho de codificação no Visual Studio.

   ![Editor no Visual Studio](media/editor.png)

## <a name="solution-explorer"></a>Gerenciador de Soluções

O **Gerenciador de Soluções**, que, normalmente, está do lado direito do Visual Studio, mostra uma representação gráfica da hierarquia de arquivos e pastas no projeto, na solução ou na pasta de código. Você pode procurar na hierarquia e navegar até algum arquivo no **Gerenciador de Soluções**.

![Gerenciador de Soluções no Visual Studio](media/quickstart-IDE-solution-explorer.png)

## <a name="menus"></a>Menus

A barra de menus na parte superior do Visual Studio agrupa os comandos em categorias. Por exemplo, o menu **Projeto** contém comandos relacionados ao projeto em que você está trabalhando. No menu **Ferramentas**, personalize o comportamento do Visual Studio selecionando **Opções** ou adicione recursos à instalação selecionando **Obter Ferramentas e Recursos**.

::: moniker range="vs-2017"

![Barra de menus no Visual Studio 2017](media/quickstart-IDE-menu-bar.png)

::: moniker-end

::: moniker range=">=vs-2019"

![Barra de menus no Visual Studio 2019](media/vs-2019/menu-bar.png)

::: moniker-end

## <a name="error-list"></a>Lista de Erros

Abra a janela **Lista de Erros** escolhendo o menu **Exibir** e, em seguida, **Lista de Erros**.

A **Lista de Erros** mostra erros, avisos e mensagens sobre o estado atual do código. Se houver erros (como uma chave ou um ponto e vírgula ausente) no arquivo ou em qualquer lugar do projeto, eles serão listados aqui.

![Lista de Erros no Visual Studio](media/quickstart-IDE-error-list.png)

## <a name="output-window"></a>janela Saída

A janela de **Saída** mostra as mensagens de saída do build do projeto e do provedor de controle do código-fonte.

Vamos criar o projeto para ver uma saída de build. No menu **Compilar** , escolha **Compilar solução**. A janela **Saída** obtém o foco automaticamente e exibe uma mensagem de build bem-sucedido.

![Janela de Saída no Visual Studio](media/build-output-minimal.png)

## <a name="search-box"></a>Caixa de pesquisa

A caixa de pesquisa é uma maneira rápida e fácil de navegar em praticamente tudo no Visual Studio. Você pode inserir um texto relacionado ao que você deseja fazer e ele mostrará uma lista de opções que pertencem ao texto. Por exemplo, imagine que você deseje aumentar o detalhamento da saída de build para que ela exiba mais detalhes sobre o que o build está fazendo exatamente. Veja como você pode fazer isso:

::: moniker range="vs-2017"

1. Localize a caixa de pesquisa **Início Rápido** no canto superior direito do IDE. (Como alternativa, pressione **Ctrl** + **P** para acessá-lo.)

2. Digite **detalhamento** na caixa de pesquisa. Nos resultados exibidos, escolha **Projetos e Soluções -> Compilar e Executar** na categoria **Opções**.

   ![Caixa de pesquisa Início Rápido no Visual Studio 2017](media/quickstart-IDE-quick-launch.png)

   A caixa de diálogo **Opções** é aberta na página de opções **Compilar e Executar**.

::: moniker-end

::: moniker range=">=vs-2019"

1. Pressione **Ctrl** + **Q** para ativar a caixa de pesquisa na parte superior do IDE.

2. Digite **detalhamento** na caixa de pesquisa. A partir dos resultados exibidos, escolha **Alterar detalhamento do MSBuild**.

   ![Caixa de pesquisa no Visual Studio 2019](media/vs-2019/quick-launch-verbosity.png)

   A caixa de diálogo **Opções** é aberta na página de opções **Compilar e Executar**.

::: moniker-end

3. Em **Detalhes da saída de build do projeto do MSBuild**, escolha **Normal** e clique em **OK**.

4. Crie o projeto novamente clicando com o botão direito do mouse no projeto **ConsoleApp1** no **Gerenciador de Soluções** e escolhendo **Recompilar** no menu de contexto.

   Desta vez, a janela **Saída** mostra o log detalhado do processo de build, incluindo quais arquivos foram copiados e onde.

   ![Saída de build detalhada no Visual Studio](media/build-output-verbose.png)

## <a name="send-feedback-menu"></a>Menu Enviar Comentários

Caso encontre problemas enquanto estiver usando o Visual Studio ou se tiver sugestões de como melhorar o produto, use o menu **Enviar Comentários** próximo da parte superior da janela do Visual Studio.

::: moniker range="vs-2017"

![Menu Enviar Comentários no Visual Studio 2017](media/quickstart-IDE-send-feedback.png)

::: moniker-end

::: moniker range=">=vs-2019"

![Menu Enviar Comentários no Visual Studio 2019](media/vs-2019/send-feedback-menu.png)

::: moniker-end

## <a name="next-steps"></a>Próximas etapas

Examinamos apenas alguns dos recursos do Visual Studio para nos familiarizarmos com a interface do usuário. Para explorar mais:

> [!div class="nextstepaction"]
> [Saiba mais sobre o editor de códigos](../get-started/tutorial-editor.md)

> [!div class="nextstepaction"]
> [Saiba mais sobre projetos e soluções](../get-started/tutorial-projects-solutions.md)

## <a name="see-also"></a>Confira também

- [Visão geral do IDE do Visual Studio](../get-started/visual-studio-ide.md)
- [Mais funcionalidades do Visual Studio](../ide/advanced-feature-overview.md)
- [Alterar as cores do tema e da fonte](../ide/quickstart-personalize-the-ide.md)
