---
title: 'Tutorial: Abrir um projeto de um Visual Studio 2017'
description: Saiba como abrir um projeto em um repositório Git ou Azure DevOps usando o Visual Studio 2017.
ms.custom: vs-acquisition, get-started
ms.date: 02/15/2021
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
monikerRange: vs-2017
ms.openlocfilehash: 5543a568f7246d9600ba375d9a1cf19af4cbd2d4
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389196"
---
# <a name="tutorial-open-a-project-from-a-repo-in-visual-studio-2017"></a>Tutorial: Abrir um projeto de um Visual Studio 2017

Neste tutorial, você usará o Visual Studio 2017 para se conectar a um repositório pela primeira vez e, em seguida, abrir um projeto dele.

> [!TIP]
> Há uma nova maneira mais integrada de se conectar a um repositório GitHub no [Visual Studio 2019.](https://visualstudio.microsoft.com/downloads) Para obter mais informações, consulte [**a nova experiência do Git na Visual Studio 2019.**](../ide/git-with-visual-studio.md?view=vs-2019&preserve-view=true)

## <a name="open-a-project-from-a-github-repo-by-using-visual-studio-2017"></a>Abrir um projeto de um repositório GitHub usando o Visual Studio 2017

1. Abra o Visual Studio 2017.

1. Na barra de menus superior, selecione **Arquivo**  >  **Aberto Aberto** no Controle do  >  **Código-Fonte**.

   O painel **Team Explorer – Conectar** é aberto.

    ![A janela do Team Explorer no IDE do Visual Studio](./media/open-proj-repo-team-explorer.png)

1. Na seção **Repositórios Git Locais,** selecione **Clonar**.

    ![Escolher Clone na seção Repositórios Git Locais](./media/open-proj-repo-local-git-repo-clone.png)

1. Na caixa que diz * Insira a URL de um repositório Git para **clonar** _, digite ou cole a URL do repositório e pressione _*Enter**. (Talvez você veja um prompt para entrar no GitHub; caso ocorra, entre).

   Depois que o Visual Studio clona o repositório, o Team Explorer é fechado e o Gerenciador de Soluções é aberto. É exibida uma mensagem que diz *Clique em Soluções e Pastas acima para exibir uma lista de Soluções*. Escolha **Soluções e Pastas**.

   ![Escolher "Soluções e Pastas" no Gerenciador de Soluções](./media/open-proj-repo-github-solutions-folders.png)

1. Se houver um arquivo de solução disponível, ele será exibido no menu suspenso "Soluções e Pastas". Escolha-o, e o Visual Studio abrirá sua solução.

   ![Escolha o que você deseja abrir na lista suspensa do Gerenciador de Soluções](./media/open-proj-repo-github-solutions-folders-picker.png)

   Se você não tiver um arquivo de solução (especificamente, um arquivo .sln) no seu repositório, o menu suspenso mostrará a mensagem "Nenhuma solução encontrada". No entanto, você pode clicar duas vezes em qualquer arquivo no menu de pastas para abri-lo no editor de códigos do Visual Studio.

### <a name="review-your-work"></a>Examinar seu trabalho

Exiba a animação a seguir para verificar o trabalho que você concluiu a seção anterior.

   ![Animação da abertura de um projeto em um repositório GitHub usando o Visual Studio](./media/open-project-from-github.gif)

> [!NOTE]
> Para obter informações específicas do Visual Studio 2019, consulte a página Abrir um projeto de um Visual Studio [2019.](tutorial-open-project-from-repo-visual-studio-2019.md)

## <a name="open-a-project-from-an-azure-devops-repo-by-using-visual-studio-2017"></a>Abrir um projeto de um Azure DevOps usando o Visual Studio 2017

1. Abra o Visual Studio 2017.

1. Na barra de menus superior, selecione **Arquivo**  >  **Aberto Aberto** no Controle do  >  **Código-Fonte**.

   O painel **Team Explorer – Conectar** é aberto.

    ![A janela do Team Explorer no IDE do Visual Studio](./media/open-proj-repo-team-explorer.png)

1. Há duas maneiras de se conectar ao repositório Azure DevOps:

      - Na seção **Provedores de Serviços Hospedados,** selecione **Conectar...**.

        ![A seção Provedores de Serviços Hospedados da janela Team Explorer no IDE do Visual Studio](./media/open-proj-repo-azure-devops.png)

      - Na lista **lista listada do** gerenciar conexões, **selecione Conectar-se a um Projeto...**.

        ![A seção Gerenciar Conexões da janela Team Explorer no IDE do Visual Studio](./media/open-proj-repo-azuredevops-manage-connections.png)

1. Na caixa **de diálogo Conectar-se a** um Projeto, escolha o repo ao qual você deseja se conectar e, em seguida, selecione **Clonar**.

      ![A caixa de diálogo 'Conectar-se a um Projeto' gerada de Visual Studio](./media/open-proj-azure-devops-connect-cloud-clone.png)

    > [!NOTE]
    > O que é exibido na caixa de listagem depende dos repositórios Azure DevOps a que você tem acesso.

1. Depois que o Visual Studio clona o repositório, o Team Explorer é fechado e o Gerenciador de Soluções é aberto. É exibida uma mensagem que diz *Clique em Soluções e Pastas acima para exibir uma lista de Soluções*. Escolha **Soluções e Pastas**.

      ![A notificação "Soluções e Pastas" do Team Explorer no Visual Studio](./media/open-proj-repo-solutions-folders.png)

   Um arquivo de solução (especificamente, um arquivo .sln) será exibido no menu suspenso "Soluções e Pastas". Escolha-o, e o Visual Studio abrirá sua solução.

   Se você não tiver um arquivo de solução no seu repositório, o menu suspenso mostrará a mensagem "Nenhuma solução encontrada". No entanto, você pode clicar duas vezes em qualquer arquivo no menu de pastas para abri-lo no editor de códigos do Visual Studio.

## <a name="next-steps"></a>Próximas etapas

Se você estiver pronto para codificar com o Visual Studio 2017, adeiba-se em qualquer um dos seguintes tutoriais específicos de linguagem:

- [Visual Studio tutoriais | **C#**](./csharp/index.yml)
- [Tutoriais do Visual Studio | **Visual Basic**](./visual-basic/index.yml)
- [Tutoriais do Visual Studio | **C++**](/cpp/get-started/tutorial-console-cpp)
- [Visual Studio tutoriais | **Python**](../python/index.yml)
- [Tutoriais do Visual Studio | **JavaScript**, **TypeScript** e **Node.js**](../javascript/index.yml)

## <a name="see-also"></a>Confira também

- [Abrir um projeto de um Visual Studio 2019](tutorial-open-project-from-repo-visual-studio-2019.md)
- [Nova experiência do Git no Visual Studio 2019](../ide/git-with-visual-studio.md)
- [Azure DevOps Services: Começar a Azure Repos e Visual Studio](/azure/devops/repos/git/gitquickstart/)
- [Microsoft Learn: Começar a Azure DevOps](/learn/modules/get-started-with-devops/)
