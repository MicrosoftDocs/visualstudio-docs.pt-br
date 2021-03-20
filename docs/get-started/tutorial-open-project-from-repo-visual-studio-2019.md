---
title: 'Tutorial: abrir um projeto de um repositório no Visual Studio 2019'
description: Saiba como abrir um projeto em um repositório do git ou DevOps do Azure usando o Visual Studio 2019.
ms.custom: get-started
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
ms.openlocfilehash: 76dcd5061e2e12688f5119598071c3235e620967
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2021
ms.locfileid: "104671707"
---
# <a name="tutorial-open-a-project-from-a-repo"></a>Tutorial: abrir um projeto de um repositório

Neste tutorial, você usará o Visual Studio para se conectar a um repositório pela primeira vez e, em seguida, abrir um projeto nele.

Se você ainda não instalou o Visual Studio, vá para a página de [downloads do Visual Studio](https://visualstudio.microsoft.com/downloads) para instalá-lo gratuitamente.

## <a name="open-a-project-from-a-github-repo"></a>Abrir um projeto de um repositório GitHub

A maneira como você abre um projeto de um repositório GitHub usando o Visual Studio 2019 depende de qual versão você tem. Especificamente, se você tiver instalado a versão [**16,8**](/visualstudio/releases/2019/release-notes/) ou posterior, há uma experiência nova e mais totalmente integrada [do git no Visual Studio](../ide/git-with-visual-studio.md) disponível para você.

Mas não importa qual versão você instalou, você sempre pode abrir um projeto de um repositório GitHub com o Visual Studio.

#### <a name="168-and-later"></a>[16,8 e posterior](#tab/vs168later)

#### <a name="clone-a-github-repo-and-then-open-a-project"></a>Clonar um repositório do GitHub e, em seguida, abrir um projeto

1. Abra o Visual Studio 2019.

1. Na janela iniciar, selecione **clonar um repositório**.

   ![Captura de tela da caixa de diálogo clonar um repositório no Visual Studio 2019 versão 16,8 e posterior](../ide/media/vs-2019/clone-repository.png)

1. Insira ou digite o local do repositório e, em seguida, selecione **clonar**.

   ![Captura de tela da caixa de diálogo clonar um repositório em que você insere uma URL do repositório git no Visual Studio 2019 versão 16,8 e posterior](../ide/media/vs-2019/clone-repository-enter-location.png)

1. Você pode ser solicitado a fornecer as informações de entrada do usuário na caixa de diálogo **informações do usuário do git** . Você pode adicionar suas informações ou editar as informações padrão que ele fornece.

   ![Captura de tela da caixa de diálogo informações do usuário do git em que você insere ou edita suas informações de conta no Visual Studio 2019 versão 16,8 e posterior](../ide/media/vs-2019/git-user-information-dialog.png)

    Selecione **salvar** para adicionar as informações ao arquivo global. gitconfig. (Ou, você pode optar por fazer isso mais tarde selecionando **Cancelar**.)

    > [!TIP]
    > Para obter mais informações sobre como entrar no Visual Studio, consulte a página [entrar no Visual Studio](../ide/signing-in-to-visual-studio.md) . E para obter informações específicas sobre como usar sua conta do GitHub para entrar, consulte a página [trabalhar com contas do GitHub no Visual Studio](../ide/work-with-github-accounts.md) .

    Em seguida, o Visual Studio carrega e abre automaticamente a solução no repositório.

   ![Captura de tela de um projeto no git que está aberto no Gerenciador de Soluções no Visual Studio 2019 versão 16,8 e posterior](../ide/media/vs-2019/git-solution-explorer.png )

1. Se o repositório contiver várias soluções, você as verá em Gerenciador de Soluções. Você pode exibir a lista de soluções selecionando o botão **alternar modos de exibição** em Gerenciador de soluções.

   ![Captura de tela de um projeto no git que está aberto no Gerenciador de Soluções, com o botão alternar modos de exibição realçado no Visual Studio 2019 versão 16,8 e posterior](../ide/media/vs-2019/git-solution-explorer-switch-views.png)

   Gerenciador de Soluções, em seguida, oferece a opção de abrir a pasta raiz na **exibição de pasta** ou selecionar um arquivo de solução para abrir.

   ![Captura de tela do arquivo. sln no git que está aberto no Gerenciador de Soluções, depois de selecionar o botão alternar modos de exibição no Visual Studio 2019 versão 16,8 e posterior](../ide/media/vs-2019/git-solution-explorer-view-solution.png)

    Para alternar a exibição, selecione o botão **alternar modos de exibição** novamente.

    > [!TIP]
    > Você também pode usar o menu **git** no IDE do Visual Studio para clonar um repositório e abrir um projeto.
    >
    > ![Captura de tela do menu git no Visual Studio 2019 versão 16,8 e posterior](../ide/media/vs-2019/git-menu-clone-create-git-repository.png)

#### <a name="open-a-project-locally-from-a-previously-cloned-github-repo"></a>Abrir um projeto localmente de um repositório GitHub clonado anteriormente

1. Abra o Visual Studio 2019.

1. Na janela iniciar, selecione **abrir um projeto ou solução**.

    O Visual Studio abre uma instância do explorador de arquivos, onde você pode navegar até sua solução ou projeto e, em seguida, selecioná-lo para abri-lo.

   ![Captura de tela da janela ' abrir um projeto ou solução ' no Visual Studio 2019 versão 16,8 e posterior](../ide/media/vs-2019/open-local-project-from-cloned-repo.png)

    Se você tiver aberto o projeto ou solução recentemente, selecione-o na seção **abrir recente** para abri-lo rapidamente.

    > [!TIP]
    > Você também pode usar o menu **git** no IDE do Visual Studio para abrir arquivos e pastas locais de um repositório que você clonou anteriormente.
    >
    > ![Captura de tela do menu git no Visual Studio 2019 versão 16,8 e posterior, com a opção de repositórios locais expandida](../ide/media/vs-2019/git-menu-local-repositories.png)

    Comece a codificar!

#### <a name="167-and-earlier"></a>[16,7 e anterior](#tab/vs167earlier)

#### <a name="clone-a-github-repo-and-then-open-a-project"></a>Clonar um repositório do GitHub e, em seguida, abrir um projeto

1. Abra o Visual Studio 2019.

1. Na janela iniciar, selecione **clonar ou fazer check-out do código**.

   ![Captura de tela da janela ' criar um novo projeto ' no Visual Studio 2019 versão 16,7 e anterior](../get-started/media/vs-2019/clone-checkout-code-dark.png)

1. Insira ou digite o local do repositório e, em seguida, selecione **clonar**.

   ![Captura de tela da janela "código de clonagem ou de check-out" no Visual Studio 2019 versão 16,7 e anterior](../get-started/media/vs-2019/clone-checkout-code-git-repo-dark.png)

   O Visual Studio abre o projeto do repositório.

1. Se houver um arquivo de solução disponível, ele será exibido no menu suspenso "Soluções e Pastas". Selecione-o e o Visual Studio abre sua solução.

   ![Captura de tela da lista suspensa Gerenciador de Soluções no Visual Studio 2019 versão 16,7 e anterior](./media/open-proj-repo-github-solutions-folders-picker.png)

   Se você não tiver um arquivo de solução (especificamente, um arquivo. sln) em seu repositório, o menu suspenso indica "nenhuma solução encontrada". No entanto, você pode clicar duas vezes em qualquer arquivo no menu de pastas para abri-lo no editor de códigos do Visual Studio.

    Comece a codificar!

---

> [!NOTE]
> Para obter informações específicas para o Visual Studio 2017, consulte a página [abrir um projeto de um repositório no visual studio 2017](tutorial-open-project-from-repo-visual-studio-2017.md) .

## <a name="connect-to-an-azure-devops-server"></a>Conectar-se a um servidor DevOps do Azure

O que você vê ao se conectar a um servidor DevOps do Azure usando o Visual Studio 2019 depende de qual versão você tem. Especificamente, se você tiver instalado a versão [**16,8**](/visualstudio/releases/2019/release-notes/) ou posterior, alteramos a interface do usuário para acomodar uma experiência de git nova e mais totalmente integrada [no Visual Studio](../ide/git-with-visual-studio.md) no Visual Studio.

Mas não importa qual versão você instalou, você sempre pode se conectar a um servidor DevOps do Azure com o Visual Studio.

#### <a name="168-and-later"></a>[16,8 e posterior](#tab/vs168later)

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

#### <a name="167-and-earlier"></a>[16,7 e anterior](#tab/vs167earlier)

1. Abra o Visual Studio 2019.

1. Na janela iniciar, selecione **clonar ou fazer check-out do código**.

   ![Captura de tela da janela ' criar um novo projeto ' no Visual Studio 2019 versão 16,7 e anterior](../get-started/media/vs-2019/clone-checkout-code-dark.png)

1. Na seção **procurar um repositório** , selecione **Azure DevOps**.

   ![Captura de tela da janela "clonar ou verificar código" com a seção "procurar um repositório" que lista o Azure DevOps no Visual Studio 2019 versão 16,7 e anterior](../get-started/media/vs-2019/clone-checkout-code-git-repo-dark.png)

   Se você vir uma janela de entrada, entre em sua conta.

1. Na caixa de diálogo **conectar a um projeto** , escolha o repositório ao qual você deseja se conectar e, em seguida, selecione **clonar**.

      ![Captura de tela da caixa de diálogo ' conectar-se a um projeto ' gerada no Visual Studio 2019 versão 16,7 e anterior](./media/open-proj-azure-devops-connect-cloud-clone.png)

    > [!NOTE]
    > O que é exibido na caixa de listagem depende dos repositórios Azure DevOps a que você tem acesso.

   O Visual Studio abrirá o **Team Explorer** e uma notificação será exibida quando a clonagem for concluída.

     ![Captura de tela da janela de Team Explorer no Visual Studio 2019 versão 16,7 e anterior, após a conclusão do clone](./media/vs-2019/clone-complete-azure-devops.png)

1. Para exibir suas pastas e arquivos, selecione o link **Mostrar exibição de pasta** .

     ![Captura de tela da seção soluções da janela Team Explorer no Visual Studio 2019 versão 16,7 e anterior, após a conclusão do clone](./media/vs-2019/show-folder-view-azure-devops.png)

     O Visual Studio abre o **Gerenciador de Soluções**.

1. Escolha o link **soluções e pastas** para pesquisar um arquivo de solução (especificamente, um arquivo. sln) a ser aberto.

      ![Captura de tela da notificação de ' soluções e pastas ' de Team Explorer no Visual Studio 2019 versão 16,7 e anterior](./media/open-proj-repo-solutions-folders.png)

   Se você não tiver um arquivo de solução em seu repositório, uma mensagem "nenhuma solução encontrada" será exibida. No entanto, você pode clicar duas vezes em qualquer arquivo no menu de pastas para abri-lo no editor de códigos do Visual Studio.

---

## <a name="next-steps"></a>Próximas etapas

Se estiver pronto para codificar com o Visual Studio, aprofunde-se em qualquer um dos seguintes tutoriais específicos a um idioma:

- [Tutoriais do Visual Studio | **C#**](./csharp/index.yml)
- [Tutoriais do Visual Studio | **Visual Basic**](./visual-basic/index.yml)
- [Tutoriais do Visual Studio | **C++**](/cpp/get-started/tutorial-console-cpp)
- [Tutoriais do Visual Studio | **Python**](../python/index.yml)
- [Tutoriais do Visual Studio | **JavaScript**, **TypeScript** e **Node.js**](../javascript/index.yml)

## <a name="see-also"></a>Veja também

- [Abrir um projeto de um repositório no Visual Studio 2017](tutorial-open-project-from-repo-visual-studio-2017.md)
- [Nova experiência de git no Visual Studio 2019](../ide/git-with-visual-studio.md)
- [Compare o git e o Team Explorer lado a lado](../ide/git-team-explorer-feature-comparison.md)
- [Azure DevOps Services: introdução ao Azure Repos e ao Visual Studio](/azure/devops/repos/git/gitquickstart/)
- [Microsoft Learn: introdução ao Azure DevOps](/learn/modules/get-started-with-devops/)