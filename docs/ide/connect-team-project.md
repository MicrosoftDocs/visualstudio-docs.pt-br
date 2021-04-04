---
title: Conectar-se a projetos no Team Explorer
description: Saiba como usar Team Explorer no Visual Studio para trabalhar com membros da equipe para desenvolver e gerenciar projetos.
ms.custom: SEO-VS-2020
ms.date: 03/31/2021
ms.topic: conceptual
ms.author: tglee
author: TerryGLee
ms.manager: jillfra
ms.openlocfilehash: 78a71911bb4334e04a085d91ff51238d34981beb
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216599"
---
# <a name="connect-to-projects-in-team-explorer"></a>Conectar-se a projetos no Team Explorer

::: moniker range="vs-2017"

Use a janela de ferramentas **Team Explorer** para coordenar seus esforços de codificação com outros membros da equipe para desenvolver um projeto e gerenciar o trabalho atribuído a você, sua equipe ou seus projetos. O **Team Explorer** conecta o Visual Studio a repositórios Git e GitHub, repositórios do TFVC (Controle de Versão do Team Foundation) e projetos hospedados no [Azure DevOps Services](/azure/devops/user-guide/what-is-azure-devops-services) ou em um [Azure DevOps Server](/azure/devops/index-all) local (anteriormente conhecido como TFS). Você pode gerenciar o código-fonte, itens de trabalho e builds.

::: moniker-end

::: moniker range="vs-2019"

Team Explorer conecta o Visual Studio aos repositórios do TFVC (controle de versão do Team Foundation) e aos projetos hospedados em [Azure DevOps Services](/azure/devops/user-guide/what-is-azure-devops-services) ou em um [Azure DevOps Server](/azure/devops/user-guide/about-azure-devops-services-tfs?view=azure-devops&preserve-view=true) local (anteriormente conhecido como TFS). Você pode gerenciar o código-fonte, itens de trabalho e builds.

> [!IMPORTANT]
> Com o lançamento recente do Visual Studio 2019 [**versão 16,8**](/visualstudio/releases/2019/release-notes/), a nova experiência de controle de versão do git agora está ativada por padrão. Se você quiser saber mais sobre como ele é comparado com Team Explorer, consulte a comparação lado a [**lado do git e da página de Team Explorer**](git-team-explorer-feature-comparison.md) .
>
> No entanto, se você preferir continuar a usar Team Explorer, vá para **ferramentas** > **Opções** >  > **Visualização** do ambiente recursos e, em seguida, alterne a caixa de seleção **nova experiência do usuário do git** .

A maneira como você usa Team Explorer para se conectar a um projeto depende da versão do Visual Studio 2019 que você está usando.

## <a name="in-version-168-and-later"></a>Na versão 16,8 e posteriores

1. Abra o Visual Studio 2019.

1. Na janela iniciar, selecione **clonar um repositório**.

   ![Captura de tela da caixa de diálogo clonar um repositório no Visual Studio 2019 versão 16,8 e posterior, para Azure DevOps](../ide/media/vs-2019/clone-repository.png)

1. Na seção **procurar um repositório** , selecione **Azure DevOps**.

    ![Captura de tela da seção ' procurar um repositório ' da caixa de diálogo ' conectar-se a um projeto ' no Visual Studio 2019 versão 16,8 e posterior](../ide/media/vs-2019/browse-repository-azure-devops.png)

1. Se você vir uma janela de entrada, entre em sua conta.

1. Na caixa de diálogo **conectar a um projeto** , escolha o repositório ao qual você deseja se conectar e, em seguida, selecione **clonar**.

      ![Captura de tela da caixa de diálogo ' conectar-se a um projeto ' gerada no Visual Studio 2019 versão 16,8 e posterior](../ide/media/vs-2019/connect-project-azure-devops.png)

      > [!TIP]
      > Se você não vir uma lista preenchida previamente de repositórios para se conectar ao, selecione **adicionar Azure DevOps Server** para inserir uma URL de servidor. (Como alternativa, você pode ver um prompt "nenhum servidor encontrado" que inclui links para adicionar um Azure DevOps Server existente ou para criar uma conta do DevOps do Azure.)

   Em seguida, o Visual Studio abre **Gerenciador de soluções** que mostra as pastas e os arquivos.

1. Selecione a guia **Team Explorer** para exibir as ações de DevOps do Azure.

      ![Captura de tela da caixa de diálogo ' Team Explorer ' gerada no Visual Studio 2019 versão 16,8 e posterior](../ide/media/vs-2019/team-explorer-azure-devops.png)

## <a name="in-version-167-and-earlier"></a>Na versão 16,7 e anteriores

1. Abra o Visual Studio 2019.

1. Na janela iniciar, selecione **clonar ou fazer check-out do código**.

   ![Captura de tela da janela ' criar um novo projeto ' no Visual Studio 2019 versão 16,7 e anterior](../get-started/media/vs-2019/clone-checkout-code-dark.png)

1. Na seção **procurar um repositório** , selecione **Azure DevOps**.

   ![Captura de tela da janela "clonar ou verificar código" com a seção "procurar um repositório" que lista o Azure DevOps no Visual Studio 2019 versão 16,7 e anterior](../get-started/media/vs-2019/clone-checkout-code-git-repo-dark.png)

   Se você vir uma janela de entrada, entre em sua conta.

1. Na caixa de diálogo **conectar a um projeto** , escolha o repositório ao qual você deseja se conectar e, em seguida, selecione **clonar**.

      ![Captura de tela da caixa de diálogo ' conectar-se a um projeto ' gerada no Visual Studio 2019 versão 16,7 e anterior](../get-started/media/open-proj-azure-devops-connect-cloud-clone.png)

    > [!NOTE]
    > O que é exibido na caixa de listagem depende dos repositórios Azure DevOps a que você tem acesso.

   O Visual Studio abrirá o **Team Explorer** e uma notificação será exibida quando a clonagem for concluída.

     ![Captura de tela da janela de Team Explorer no Visual Studio 2019 versão 16,7 e anterior, após a conclusão do clone](../get-started/media/vs-2019/clone-complete-azure-devops.png)

1. Para exibir suas pastas e arquivos, selecione o link **Mostrar exibição de pasta** .

     ![Captura de tela da seção soluções da janela Team Explorer no Visual Studio 2019 versão 16,7 e anterior, após a conclusão do clone](../get-started/media/vs-2019/show-folder-view-azure-devops.png)

     O Visual Studio abre o **Gerenciador de Soluções**.

1. Escolha o link **soluções e pastas** para pesquisar um arquivo de solução (especificamente, um arquivo. sln) a ser aberto.

      ![Captura de tela da notificação de ' soluções e pastas ' de Team Explorer no Visual Studio 2019 versão 16,7 e anterior](../get-started/media/open-proj-repo-solutions-folders.png)

   Se você não tiver um arquivo de solução em seu repositório, uma mensagem "nenhuma solução encontrada" será exibida. No entanto, você pode clicar duas vezes em qualquer arquivo no menu de pastas para abri-lo no editor de códigos do Visual Studio.

::: moniker-end

::: moniker range="vs-2017"

![Home page do Team Explorer no Visual Studio](media/team-explorer/team-explorer.png "A home page do Team Explorer no Visual Studio.")

> [!TIP]
> Se você abrir o Visual Studio e **Team Explorer** não aparecer, abra-o escolhendo **Exibir**  >  **Team Explorer** na barra de menus ou pressionando **Ctrl** + **&#92;**, **Ctrl** + **M**.

## <a name="connect-to-a-project-or-repository"></a>Conectar-se a um projeto ou um repositório

Conecte-se a um projeto ou um repositório na página **Conectar**.

![Página Conectar no Team Explorer](media/team-explorer/connect.png "A página Team Explorer-Connect no Visual Studio")

Para se conectar a um projeto:

1. Abra a página **Conectar** escolhendo o ícone **Gerenciar Conexões**.

   ![Botão Gerenciar Conexões no Team Explorer](media/team-explorer/manage-connections.png "O botão Team Explorer-gerenciar conexões no Visual Studio.")

1. Na página **Conectar**, escolha **Gerenciar Conexões** > **Conectar-se a um projeto**.

   ![Conectar-se a um projeto no Team Explorer](media/team-explorer/connect-project.png "A opção Team Explorer-conectar a um projeto no Visual Studio.")

> [!TIP]
> Se você quiser abrir um projeto de um repositório, consulte [abrir um projeto de um repositório](../get-started/tutorial-open-project-from-repo-visual-studio-2017.md). Se você quiser criar um novo projeto ou adicionar usuários a um projeto, consulte [criar um projeto (Azure DevOps)](/azure/devops/organizations/projects/create-project) e [Adicionar usuários a um projeto ou equipe (Azure DevOps)](/azure/devops/organizations/security/add-users-team-project).

::: moniker-end

## <a name="see-also"></a>Confira também

- [Compare o git e o Team Explorer lado a lado](git-team-explorer-feature-comparison.md)
- [A nova experiência de git no Visual Studio](git-with-visual-studio.md)
- [Referência do Team Explorer](reference/team-explorer-reference.md)
- [Conectar-se a um projeto (Azure DevOps)](/azure/devops/organizations/projects/connect-to-projects)
- [Solucionar problemas de conexão com um projeto](/azure/devops/user-guide/troubleshoot-connection?view=azure-devops&preserve-view=true)
