---
title: Conectar-se a projetos no Team Explorer
description: Saiba como usar o Team Explorer no Visual Studio para trabalhar com membros da equipe para desenvolver e gerenciar projetos.
ms.custom: SEO-VS-2020
ms.date: 06/11/2021
ms.topic: conceptual
ms.author: tglee
author: TerryGLee
ms.manager: jillfra
monikerRange: <=vs-2019
ms.openlocfilehash: b45399f7a4115ce5946a67caca22ca92148e7434
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112308240"
---
# <a name="connect-to-projects-in-team-explorer"></a>Conectar-se a projetos no Team Explorer

::: moniker range="vs-2017"

Use a janela de ferramentas **Team Explorer** para coordenar seus esforços de codificação com outros membros da equipe para desenvolver um projeto e gerenciar o trabalho atribuído a você, sua equipe ou seus projetos. O **Team Explorer** conecta o Visual Studio a repositórios Git e GitHub, repositórios do TFVC (Controle de Versão do Team Foundation) e projetos hospedados no [Azure DevOps Services](/azure/devops/user-guide/what-is-azure-devops-services) ou em um [Azure DevOps Server](/azure/devops/index-all) local (anteriormente conhecido como TFS). Você pode gerenciar o código-fonte, itens de trabalho e builds.

::: moniker-end

::: moniker range="vs-2019"

Team Explorer conecta Visual Studio repositórios de controle de versão do Team Foundation (TFVC) e a projetos hospedados no [Azure DevOps Services](/azure/devops/user-guide/what-is-azure-devops-services) ou em um [Azure DevOps Server](/azure/devops/user-guide/about-azure-devops-services-tfs?view=azure-devops&preserve-view=true) local (anteriormente conhecido como TFS). Você pode gerenciar o código-fonte, itens de trabalho e builds.

> [!IMPORTANT]
> Com o lançamento do Visual Studio 2019 [**versão 16.8,**](/visualstudio/releases/2019/release-notes-history)a experiência de controle de versão do Git está em por padrão. Se você quiser saber mais sobre como ele se compara ao Team Explorer, confira a página Comparação lado a lado do [**Git e**](../version-control/git-team-explorer-feature-comparison.md) Team Explorer.
>
> No entanto, se você preferir continuar a usar  o Team Explorer, vá para Ferramentas Opções Recursos de Visualização do Ambiente e, em seguida, alterne a caixa de seleção Nova experiência do usuário >  >  >  **do Git.**

A maneira como Team Explorer para se conectar a um projeto depende da versão Visual Studio 2019 que você está usando.

## <a name="in-version-168-and-later"></a>Na versão 16.8 e posterior

1. Abra o Visual Studio 2019.

1. Na janela inicial, selecione **Clonar um repositório**.

   ![Captura de tela da caixa de diálogo Clonar um Repositório no Visual Studio 2019 versão 16.8 e posterior, para Azure DevOps](../ide/media/vs-2019/clone-repository.png)

1. Na seção **Procurar um repositório,** selecione **Azure DevOps**.

    ![Captura de tela da seção "Procurar um repositório" da caixa de diálogo "Conectar-se a um Projeto" no Visual Studio 2019 versão 16.8 e posterior](../ide/media/vs-2019/browse-repository-azure-devops.png)

1. Se você vir uma janela de entrada, entre em sua conta.

1. Na caixa **de diálogo Conectar-se a** um Projeto, escolha o repo ao qual você deseja se conectar e, em seguida, selecione **Clonar**.

      ![Captura de tela da caixa de diálogo 'Conectar-se a um Projeto' gerada Visual Studio 2019 versão 16.8 e posterior](../ide/media/vs-2019/connect-project-azure-devops.png)

      > [!TIP]
      > Se você não vir uma lista preenchida previamente de repos para se conectar, selecione **Adicionar** Azure DevOps Server para inserir uma URL do servidor. (Como alternativa, você pode ver um prompt "Nenhum servidor encontrado" que inclui links para adicionar um Azure DevOps Server existente ou para criar uma conta Azure DevOps.)

   Em seguida, Visual Studio **abre Gerenciador de Soluções** que mostra as pastas e os arquivos.

1. Selecione a **Team Explorer** para exibir as ações Azure DevOps segurança.

      ![Captura de tela Team Explorer caixa de diálogo "Team Explorer" gerada Visual Studio 2019 versão 16.8 e posterior](../ide/media/vs-2019/team-explorer-azure-devops.png)

## <a name="in-version-167-and-earlier"></a>Na versão 16.7 e anteriores

1. Abra o Visual Studio 2019.

1. Na janela inicial, selecione **Clonar ou confira o código**.

   ![Captura de tela da janela "Criar um novo projeto" no Visual Studio 2019 versão 16.7 e anteriores](../get-started/media/vs-2019/clone-checkout-code-dark.png)

1. Na seção **Procurar um repositório,** selecione **Azure DevOps**.

   ![Captura de tela da janela "Clonar ou fazer check-out do código" com a seção "Procurar um repositório" que lista Azure DevOps no Visual Studio 2019 versão 16.7 e anteriores](../get-started/media/vs-2019/clone-checkout-code-git-repo-dark.png)

   Se você vir uma janela de entrada, entre em sua conta.

1. Na caixa **de diálogo Conectar-se a** um Projeto, escolha o repo ao qual você deseja se conectar e, em seguida, selecione **Clonar**.

      ![Captura de tela da caixa de diálogo 'Conectar-se a um Projeto' gerada Visual Studio 2019 versão 16.7 e anteriores](../get-started/media/open-proj-azure-devops-connect-cloud-clone.png)

    > [!NOTE]
    > O que é exibido na caixa de listagem depende dos repositórios Azure DevOps a que você tem acesso.

   O Visual Studio abrirá o **Team Explorer** e uma notificação será exibida quando a clonagem for concluída.

     ![Captura de tela da Team Explorer no Visual Studio 2019 versão 16.7 e anteriores, após a conclusão do clone](../get-started/media/vs-2019/clone-complete-azure-devops.png)

1. Para exibir suas pastas e arquivos, selecione o link **Mostrar Exibição de** Pasta.

     ![Captura de tela da seção Soluções da janela Team Explorer no Visual Studio 2019 versão 16.7 e anteriores, após a conclusão do clone](../get-started/media/vs-2019/show-folder-view-azure-devops.png)

     O Visual Studio abre o **Gerenciador de Soluções**.

1. Escolha o link **Soluções e Pastas** para pesquisar um arquivo de solução (especificamente, um arquivo .sln) a ser aberto.

      ![Captura de tela da notificação de "Soluções e Pastas" Team Explorer no Visual Studio 2019 versão 16.7 e anteriores](../get-started/media/open-proj-repo-solutions-folders.png)

   Se você não tiver um arquivo de solução no seu repo, será exibida uma mensagem "Sem Soluções Encontradas&quot;. No entanto, você pode clicar duas vezes em qualquer arquivo no menu de pastas para abri-lo no editor de códigos do Visual Studio.

::: moniker-end

::: moniker range=&quot;vs-2017&quot;

![Home page do Team Explorer no Visual Studio](media/team-explorer/team-explorer.png &quot;A Team Explorer - Home page no Visual Studio.")

> [!TIP]
> Se você abrir Visual Studio e **Team Explorer** não aparecer, abra-o escolhendo Exibir Team Explorer na barra de menus ou pressionando  >   **Ctrl** + **&#92;**, **Ctrl** + **M**.

## <a name="connect-to-a-project-or-repository"></a>Conectar-se a um projeto ou um repositório

Conecte-se a um projeto ou um repositório na página **Conectar**.

![Página Conectar no Team Explorer](media/team-explorer/connect.png "A Team Explorer - Conectar no Visual Studio")

Para se conectar a um projeto:

1. Abra a página **Conectar** escolhendo o ícone **Gerenciar Conexões**.

   ![Botão Gerenciar Conexões no Team Explorer](media/team-explorer/manage-connections.png "O Team Explorer - Gerenciar Conexões no Visual Studio.")

1. Na página **Conectar,** escolha Gerenciar  > **Conexões Conectar-se a um projeto**.

   ![Conectar-se a um projeto no Team Explorer](media/team-explorer/connect-project.png "A Team Explorer - Conectar-se a um projeto no Visual Studio.")

> [!TIP]
> Se você quiser abrir um projeto de um repo, consulte [Abrir um projeto de um repo](../get-started/tutorial-open-project-from-repo-visual-studio-2017.md). Se você quiser criar um novo projeto ou adicionar usuários a um projeto, consulte Criar um projeto [(Azure DevOps)](/azure/devops/organizations/projects/create-project) e Adicionar usuários a um projeto ou equipe [(Azure DevOps)](/azure/devops/organizations/security/add-users-team-project).

::: moniker-end

## <a name="see-also"></a>Confira também

- [Comparar Git e Team Explorer lado a lado](git-team-explorer-feature-comparison.md)
- [A nova experiência do Git no Visual Studio](git-with-visual-studio.md)
- [Referência do Team Explorer](reference/team-explorer-reference.md)
- [Conectar-se a um projeto (Azure DevOps)](/azure/devops/organizations/projects/connect-to-projects)
- [Solucionar problemas de conexão com um projeto](/azure/devops/user-guide/troubleshoot-connection?view=azure-devops&preserve-view=true)
