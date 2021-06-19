---
title: 'Tutorial: Abrir um projeto de um Visual Studio 2019'
description: Saiba como abrir um projeto em um repositório Git ou Azure DevOps usando o Visual Studio 2019.
ms.custom: vs-acquisition, get-started
ms.date: 03/18/2021
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: tutorial
author: TerryGLee
ms.author: tglee
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- dotnet
- dotnetcore
monikerRange: vs-2019
ms.openlocfilehash: b6f7cd57a1753ca5926ac73a9bb4c8c918d1bd10
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389937"
---
# <a name="tutorial-open-a-project-from-a-repo"></a>Tutorial: Abrir um projeto de umpo

Neste tutorial, você usará o Visual Studio para se conectar a um repositório pela primeira vez e, em seguida, abrir um projeto nele.

Se você ainda não tiver instalado o Visual Studio, acesse a página [Visual Studio downloads](https://visualstudio.microsoft.com/downloads) para instalá-lo gratuitamente.

## <a name="open-a-project-from-a-github-repo"></a>Abrir um projeto de um repositório GitHub

A maneira como você abre um projeto de um repositório GitHub usando Visual Studio 2019 depende de qual versão você tem. Especificamente, se você instalou a versão [**16.8**](/visualstudio/releases/2019/release-notes/) ou posterior, há uma nova e mais integrada experiência [do Git Visual Studio](../ide/git-with-visual-studio.md) disponível para você.

Mas não importa qual versão você instalou, você sempre pode abrir um projeto de um repositório gitHub com Visual Studio.

#### <a name="168-and-later"></a>[16.8 e posterior](#tab/vs168later)

#### <a name="clone-a-github-repo-and-then-open-a-project"></a>Clonar um repositório GitHub e, em seguida, abrir um projeto

1. Abra o Visual Studio 2019.

1. Na janela inicial, selecione **Clonar um repositório**.

   ![Captura de tela da caixa de diálogo Clonar um Repositório no Visual Studio 2019 versão 16.8 e posterior](../ide/media/vs-2019/clone-repository.png)

1. Insira ou digite o local do repositório e, em seguida, **selecione Clonar**.

   ![Captura de tela da caixa de diálogo Clonar um Repositório em que você inspeção uma URL do repositório Git no Visual Studio 2019 versão 16.8 e posterior](../ide/media/vs-2019/clone-repository-enter-location.png)

1. Você pode ser solicitado a obter as informações de login do usuário na caixa **de diálogo Informações do Usuário do Git.** Você pode adicionar suas informações ou editar as informações padrão que ela fornece.

   ![Captura de tela da caixa de diálogo Informações do Usuário do Git em que você ins muita informação da sua conta Visual Studio 2019 versão 16.8 e posteriores](../ide/media/vs-2019/git-user-information-dialog.png)

    Selecione **Salvar** para adicionar as informações ao arquivo .gitconfig global. (Ou você pode optar por fazer isso mais tarde selecionando **Cancelar**.)

    > [!TIP]
    > Para obter mais informações sobre como entrar Visual Studio, consulte a página [Entrar Visual Studio](../ide/signing-in-to-visual-studio.md) dados. E para obter informações específicas sobre como usar sua conta do GitHub para entrar, consulte a página Trabalhar com contas do [GitHub Visual Studio](../ide/work-with-github-accounts.md) dados.

    Em seguida, Visual Studio carrega automaticamente e abre a solução do repositório.

   ![Captura de tela de um projeto no Git que está aberto no Gerenciador de Soluções no Visual Studio 2019 versão 16.8 e posterior](../ide/media/vs-2019/git-solution-explorer.png )

1. Se o repositório contiver várias soluções, você as verá Gerenciador de Soluções. Você pode exibir a lista de soluções selecionando o **botão Alternar Exibições** Gerenciador de Soluções.

   ![Captura de tela de um projeto no Git que está aberto no Gerenciador de Soluções, com o botão Alternar Exibições realçada no Visual Studio 2019 versão 16.8 e posterior](../ide/media/vs-2019/git-solution-explorer-switch-views.png)

   Gerenciador de Soluções oferece a opção de abrir a pasta  raiz na Exibição de Pasta ou selecionar um arquivo de solução a ser aberto.

   ![Captura de tela do arquivo .sln no Git que está aberto no Gerenciador de Soluções, depois de selecionar o botão Alternar Exibições no Visual Studio 2019 versão 16.8 e posterior](../ide/media/vs-2019/git-solution-explorer-view-solution.png)

    Para alternar a exibição, selecione o **botão Alternar Exibições** novamente.

    > [!TIP]
    > Você também pode usar o menu **Git** no Visual Studio IDE para clonar um repositório e abrir um projeto.
    >
    > ![Captura de tela do menu Git no Visual Studio 2019 versão 16.8 e posterior](../ide/media/vs-2019/git-menu-clone-create-git-repository.png)

#### <a name="open-a-project-locally-from-a-previously-cloned-github-repo"></a>Abrir um projeto localmente de um repositório GitHub clonado anteriormente

1. Abra o Visual Studio 2019.

1. Na janela inicial, selecione **Abrir um projeto ou solução**.

    Visual Studio abre uma instância do Explorador de Arquivos, na qual você pode navegar até sua solução ou projeto e, em seguida, selecioná-la para abri-la.

   ![Captura de tela da janela "Abrir um projeto ou solução" no Visual Studio 2019 versão 16.8 e posterior](../ide/media/vs-2019/open-local-project-from-cloned-repo.png)

    Se você abriu o projeto ou a solução  recentemente, selecione-o na seção Abrir recente para abri-lo rapidamente novamente.

    > [!TIP]
    > Você também pode usar o menu **Git** no Visual Studio IDE para abrir pastas e arquivos locais de um repositório clonado anteriormente.
    >
    > ![Captura de tela do menu Git no Visual Studio 2019 versão 16.8 e posterior, com a opção Repositórios Locais expandida](../ide/media/vs-2019/git-menu-local-repositories.png)

    Inicie a codificação!

#### <a name="167-and-earlier"></a>[16.7 e versões anteriores](#tab/vs167earlier)

#### <a name="clone-a-github-repo-and-then-open-a-project"></a>Clonar um repositório GitHub e, em seguida, abrir um projeto

1. Abra o Visual Studio 2019.

1. Na janela inicial, selecione **Clonar ou confira o código**.

   ![Captura de tela da janela "Criar um novo projeto" no Visual Studio 2019 versão 16.7 e anteriores](../get-started/media/vs-2019/clone-checkout-code-dark.png)

1. Insira ou digite o local do repositório e, em seguida, **selecione Clonar**.

   ![Captura de tela da janela "Clonar ou fazer check-in do código" no Visual Studio 2019 versão 16.7 e anteriores](../get-started/media/vs-2019/clone-checkout-code-git-repo-dark.png)

   O Visual Studio abre o projeto do repositório.

1. Se houver um arquivo de solução disponível, ele será exibido no menu suspenso "Soluções e Pastas". Selecione-o e Visual Studio abrir sua solução.

   ![Captura de tela da Gerenciador de Soluções lista Visual Studio 2019 versão 16.7 e anteriores](./media/open-proj-repo-github-solutions-folders-picker.png)

   Se você não tiver um arquivo de solução (especificamente, um arquivo .sln) no seu repo, o menu suspenso diz "Nenhuma solução encontrada". No entanto, você pode clicar duas vezes em qualquer arquivo no menu de pastas para abri-lo no editor de códigos do Visual Studio.

    Inicie a codificação!

---

> [!NOTE]
> Para obter informações específicas do Visual Studio 2017, consulte a página Abrir um projeto de um Visual Studio [2017.](tutorial-open-project-from-repo-visual-studio-2017.md)

## <a name="connect-to-an-azure-devops-server"></a>Conectar-se a um Azure DevOps servidor

O que você vê ao se conectar a um servidor Azure DevOps usando o Visual Studio 2019 depende de qual versão você tem. Especificamente, se você instalou a versão [**16.8**](/visualstudio/releases/2019/release-notes/) ou posterior, mudamos a interface do usuário para acomodar uma nova experiência do [Git](../ide/git-with-visual-studio.md) mais integrada no Visual Studio no Visual Studio.

Mas não importa qual versão você instalou, você sempre pode se conectar a um servidor Azure DevOps com Visual Studio.

#### <a name="168-and-later"></a>[16.8 e posterior](#tab/vs168later)

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

#### <a name="167-and-earlier"></a>[16.7 e versões anteriores](#tab/vs167earlier)

1. Abra o Visual Studio 2019.

1. Na janela inicial, selecione **Clonar ou confira o código**.

   ![Captura de tela da janela "Criar um novo projeto" no Visual Studio 2019 versão 16.7 e anteriores](../get-started/media/vs-2019/clone-checkout-code-dark.png)

1. Na seção **Procurar um repositório,** selecione **Azure DevOps**.

   ![Captura de tela da janela "Clonar ou fazer check-out do código" com a seção "Procurar um repositório" que lista Azure DevOps no Visual Studio 2019 versão 16.7 e anteriores](../get-started/media/vs-2019/clone-checkout-code-git-repo-dark.png)

   Se você vir uma janela de entrada, entre em sua conta.

1. Na caixa **de diálogo Conectar-se a** um Projeto, escolha o repo ao qual você deseja se conectar e, em seguida, selecione **Clonar**.

      ![Captura de tela da caixa de diálogo 'Conectar-se a um Projeto' gerada Visual Studio 2019 versão 16.7 e anteriores](./media/open-proj-azure-devops-connect-cloud-clone.png)

    > [!NOTE]
    > O que é exibido na caixa de listagem depende dos repositórios Azure DevOps a que você tem acesso.

   O Visual Studio abrirá o **Team Explorer** e uma notificação será exibida quando a clonagem for concluída.

     ![Captura de tela da Team Explorer no Visual Studio 2019 versão 16.7 e anteriores, após a conclusão do clone](./media/vs-2019/clone-complete-azure-devops.png)

1. Para exibir suas pastas e arquivos, selecione o link **Mostrar Exibição de** Pasta.

     ![Captura de tela da seção Soluções da janela Team Explorer no Visual Studio 2019 versão 16.7 e anteriores, após a conclusão do clone](./media/vs-2019/show-folder-view-azure-devops.png)

     O Visual Studio abre o **Gerenciador de Soluções**.

1. Escolha o link **Soluções e Pastas** para pesquisar um arquivo de solução (especificamente, um arquivo .sln) a ser aberto.

      ![Captura de tela da notificação de "Soluções e Pastas" Team Explorer no Visual Studio 2019 versão 16.7 e anteriores](./media/open-proj-repo-solutions-folders.png)

   Se você não tiver um arquivo de solução no seu repo, será exibida uma mensagem "Sem Soluções Encontradas". No entanto, você pode clicar duas vezes em qualquer arquivo no menu de pastas para abri-lo no editor de códigos do Visual Studio.

---

## <a name="next-steps"></a>Próximas etapas

Se estiver pronto para codificar com o Visual Studio, aprofunde-se em qualquer um dos seguintes tutoriais específicos a um idioma:

- [Visual Studio tutoriais | **C#**](./csharp/index.yml)
- [Tutoriais do Visual Studio | **Visual Basic**](./visual-basic/index.yml)
- [Tutoriais do Visual Studio | **C++**](/cpp/get-started/tutorial-console-cpp)
- [Visual Studio tutoriais | **Python**](../python/index.yml)
- [Tutoriais do Visual Studio | **JavaScript**, **TypeScript** e **Node.js**](../javascript/index.yml)

## <a name="see-also"></a>Confira também

- [Abrir um projeto de um repositório no Visual Studio 2017](tutorial-open-project-from-repo-visual-studio-2017.md)
- [Nova experiência de git no Visual Studio 2019](../ide/git-with-visual-studio.md)
- [Compare o git e o Team Explorer lado a lado](../ide/git-team-explorer-feature-comparison.md)
- [Azure DevOps Services: introdução ao Azure Repos e ao Visual Studio](/azure/devops/repos/git/gitquickstart/)
- [Microsoft Learn: introdução ao Azure DevOps](/learn/modules/get-started-with-devops/)
