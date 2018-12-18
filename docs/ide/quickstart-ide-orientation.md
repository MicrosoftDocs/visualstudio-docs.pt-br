---
title: Tour do IDE do Visual Studio
ms.date: 07/12/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: quickstart
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: dbf969e6e9a37179621cad52243418a2d0536f1a
ms.sourcegitcommit: 2597236a481afbaf1ad4915743898ee1aee49760
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/10/2018
ms.locfileid: "42627026"
---
# <a name="quickstart-first-look-at-the-visual-studio-ide"></a>Início rápido: Introdução ao IDE do Visual Studio

Nesta introdução de 5 a 10 minutos ao IDE (Ambiente de Desenvolvimento Integrado) do Visual Studio, faremos um tour em algumas janelas, menus e em outros recursos de interface do usuário.

Se você ainda não tiver instalado o Visual Studio, acesse a página [Downloads do Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) para instalá-lo gratuitamente.

## <a name="start-page"></a>Start Page

A primeira coisa que você verá depois de iniciar o Visual Studio provavelmente será a **Página Inicial**. A **Página Inicial** foi projetada como um "hub" para ajudá-lo a localizar os comandos e os arquivos de projeto necessários com mais rapidez. A seção **Recentes** exibe projetos e pastas em que você trabalhou recentemente. Em **Novo projeto**, clique em um link para abrir a caixa de diálogo **Novo Projeto** ou, em **Abrir**, abra uma pasta ou um projeto de código existente. À direita está um feed das notícias mais recentes do desenvolvedor.

![Página Inicial no Visual Studio](media/start-page.png)

Se você fechar a **Página Inicial** e desejar vê-la novamente, será possível reabri-la no menu **Arquivo**.

![Menu Arquivo no Visual Studio](media/quickstart-IDE-file-menu-large.png)

## <a name="create-a-project"></a>Criar um projeto

Para continuar explorando os recursos do Visual Studio, vamos criar um projeto.

1. Na **Página Inicial**, na caixa de pesquisa de **Novo projeto**, digite **console** para filtrar da lista de tipos de projeto aqueles que contêm "console" no nome.

   ![Pesquisar modelos de projeto na Página Inicial do Visual Studio](media/start-page-search-templates.png)

   O Visual Studio fornece vários tipos de modelos de projeto que ajudam você a começar a codificar rapidamente. Escolha um modelo de projeto **Aplicativo de Console (.NET Framework)** C#. (Como alternativa, se você for um desenvolvedor de Visual Basic, C++, JavaScript ou outra linguagem, fique à vontade para criar um projeto em uma dessas linguagens. A interface do usuário que veremos é semelhante em todas as linguagens de programação.)

1. Na caixa de diálogo **Novo Projeto** exibida, aceite o nome de projeto padrão e escolha **OK**.

   O projeto é criado e um arquivo chamado *Program.cs* é aberto na janela **Editor**. O **Editor** mostra o conteúdo dos arquivos e é onde você fará a maior parte do trabalho de codificação no Visual Studio.

   ![Editor no Visual Studio](media/editor.png)

## <a name="solution-explorer"></a>Gerenciador de Soluções

O **Gerenciador de Soluções**, que, normalmente, está do lado direito do Visual Studio, mostra uma representação gráfica da hierarquia de arquivos e pastas no projeto, na solução ou na pasta de código. Você pode procurar na hierarquia e navegar até algum arquivo no **Gerenciador de Soluções**.

![Gerenciador de Soluções no Visual Studio](media/quickstart-IDE-solution-explorer.png)

## <a name="menus"></a>Menus

A barra de menus na parte superior do Visual Studio agrupa os comandos em categorias. Por exemplo, o menu **Projeto** contém comandos relacionados ao projeto em que você está trabalhando. No menu **Ferramentas**, personalize o comportamento do Visual Studio selecionando **Opções** ou adicione recursos à instalação selecionando **Obter Ferramentas e Recursos**.

![Barra de menus no Visual Studio](media/quickstart-IDE-menu-bar.png)

Vamos abrir a janela **Lista de Erros** escolhendo o menu **Exibir** e, em seguida, **Lista de Erros**.

## <a name="error-list"></a>Lista de Erros

A **Lista de Erros** mostra erros, avisos e mensagens sobre o estado atual do código. Se houver erros (como uma chave ou um ponto e vírgula ausente) no arquivo ou em qualquer lugar do projeto, eles serão listados aqui.

![Lista de Erros no Visual Studio](media/quickstart-IDE-error-list.png)

## <a name="output-window"></a>janela Saída

A janela de **Saída** mostra as mensagens de saída do build do projeto e do provedor de controle do código-fonte.

Vamos criar o projeto para ver uma saída de build. No menu **Compilação**, escolha **Compilar Solução**. A janela **Saída** obtém o foco automaticamente e exibe uma mensagem de build bem-sucedido.

![Janela de Saída no Visual Studio](media/build-output-minimal.png)

## <a name="quick-launch"></a>Início Rápido

A caixa **Início Rápido** é uma maneira rápida e fácil de fazer praticamente tudo no Visual Studio. Você pode inserir um texto relacionado ao que você deseja fazer e ele mostrará uma lista de opções que pertencem ao texto. Por exemplo, imagine que você deseje aumentar o detalhamento da saída de build para que ela exiba mais detalhes sobre o que o build está fazendo exatamente. Veja como você pode fazer isso:

1. Digite **detalhamento** na caixa **Início Rápido**. Nos resultados exibidos, escolha **Projetos e Soluções -> Compilar e Executar** na categoria **Opções**.

   ![Caixa Início Rápido no Visual Studio](media/quickstart-IDE-quick-launch.png)

   A caixa de diálogo **Opções**é aberta na página de opções **Compilar e Executar**.

1. Em **Detalhes da saída de build do projeto do MSBuild**, escolha **Normal** e clique em **OK**.

1. Crie o projeto novamente clicando com o botão direito do mouse no projeto **ConsoleApp1** no **Gerenciador de Soluções** e escolhendo **Recompilar** no menu de contexto.

   Desta vez, a janela **Saída** mostra o log detalhado do processo de build, incluindo quais arquivos foram copiados e onde.

   ![Saída de build detalhada no Visual Studio](media/build-output-verbose.png)

## <a name="send-feedback-menu"></a>Menu Enviar Comentários

Caso encontre problemas enquanto estiver usando o Visual Studio ou tenha sugestões de como melhorar o produto, use o menu **Enviar Comentários** na parte superior da janela do Visual Studio, ao lado da caixa **Início Rápido**.

![Menu Enviar Comentários no Visual Studio](media/quickstart-IDE-send-feedback.png)

## <a name="next-steps"></a>Próximas etapas

Examinamos apenas alguns dos recursos do Visual Studio para nos familiarizarmos com a interface do usuário. Para explorar mais:

> [!div class="nextstepaction"]
> [Saiba mais sobre o editor de códigos](../ide/quickstart-editor.md)

> [!div class="nextstepaction"]
> [Saiba mais sobre projetos e soluções](../ide/quickstart-projects-solutions.md)

## <a name="see-also"></a>Consulte também

- [Visão geral do IDE do Visual Studio](../ide/visual-studio-ide.md)
- [Mais recursos do Visual Studio 2017](../ide/advanced-feature-overview.md)
- [Alterar as cores do tema e da fonte](../ide/quickstart-personalize-the-ide.md)
