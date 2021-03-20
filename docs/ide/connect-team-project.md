---
title: Conectar-se a projetos no Team Explorer
description: Saiba como usar Team Explorer no Visual Studio para trabalhar com membros da equipe para desenvolver e gerenciar projetos.
ms.custom: SEO-VS-2020
ms.date: 11/17/2020
ms.topic: conceptual
ms.author: tglee
author: TerryGLee
ms.manager: jillfra
ms.openlocfilehash: 58603b72128af1c6dd9caae93f92c435f0851ada
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2021
ms.locfileid: "104672989"
---
# <a name="connect-to-projects-in-team-explorer"></a>Conectar-se a projetos no Team Explorer

::: moniker range="vs-2017"

Use a janela de ferramentas **Team Explorer** para coordenar seus esforços de codificação com outros membros da equipe para desenvolver um projeto e gerenciar o trabalho atribuído a você, sua equipe ou seus projetos. O **Team Explorer** conecta o Visual Studio a repositórios Git e GitHub, repositórios do TFVC (Controle de Versão do Team Foundation) e projetos hospedados no [Azure DevOps Services](/azure/devops/user-guide/what-is-azure-devops-services) ou em um [Azure DevOps Server](/azure/devops/index-all) local (anteriormente conhecido como TFS). Você pode gerenciar o código-fonte, itens de trabalho e builds.

::: moniker-end

::: moniker range="vs-2019"

Você pode usar a janela de ferramentas de **Team Explorer** para coordenar seus esforços de código com outros membros da equipe para desenvolver um projeto e para gerenciar o trabalho atribuído a você, sua equipe ou seus projetos.

> [!IMPORTANT]
> Com o lançamento recente do Visual Studio 2019 [versão 16,8](/visualstudio/releases/2019/release-notes/), a nova experiência de controle de versão do git agora está ativada por padrão. No entanto, se você preferir continuar a usar Team Explorer, vá para **ferramentas**  >  **Opções**  >    >  **Visualização** do ambiente recursos e, em seguida, alterne a caixa de seleção **nova experiência do usuário do git** . Para obter mais informações, consulte a página [experiência do git no Visual Studio](git-with-visual-studio.md) .

O **Team Explorer** conecta o Visual Studio a repositórios Git e GitHub, repositórios do TFVC (Controle de Versão do Team Foundation) e projetos hospedados no [Azure DevOps Services](/azure/devops/user-guide/what-is-azure-devops-services) ou em um [Azure DevOps Server](/azure/devops/index-all) local (anteriormente conhecido como TFS). Você pode gerenciar o código-fonte, itens de trabalho e builds.

::: moniker-end

![Home page do Team Explorer no Visual Studio](media/team-explorer/team-explorer.png "A home page do Team Explorer no Visual Studio.")

::: moniker range="vs-2017"

> [!TIP]
> Se você abrir o Visual Studio e **Team Explorer** não aparecer, abra-o escolhendo **Exibir**  >  **Team Explorer** na barra de menus ou pressionando **Ctrl** + **&#92;**, **Ctrl** + **M**.

::: moniker-end

## <a name="connect-to-a-project-or-repository"></a>Conectar-se a um projeto ou um repositório

Conecte-se a um projeto ou um repositório na página **Conectar**.

![Página Conectar no Team Explorer](media/team-explorer/connect.png "A página Team Explorer-Connect no Visual Studio")

Para se conectar a um projeto:

1. Abra a página **Conectar** escolhendo o ícone **Gerenciar Conexões**.

   ![Botão Gerenciar Conexões no Team Explorer](media/team-explorer/manage-connections.png "O botão Team Explorer-gerenciar conexões no Visual Studio.")

1. Na página **Conectar**, escolha **Gerenciar Conexões** > **Conectar-se a um projeto**.

   ![Conectar-se a um projeto no Team Explorer](media/team-explorer/connect-project.png "A opção Team Explorer-conectar a um projeto no Visual Studio.")

> [!TIP]
> Se você quiser abrir um projeto de um repositório, consulte [abrir um projeto de um repositório](../get-started/tutorial-open-project-from-repo.md). Se você quiser criar um novo projeto ou adicionar usuários a um projeto, consulte [criar um projeto (Azure DevOps)](/azure/devops/organizations/projects/create-project) e [Adicionar usuários a um projeto ou equipe (Azure DevOps)](/azure/devops/organizations/security/add-users-team-project).

## <a name="see-also"></a>Veja também

- [Compare o git e o Team Explorer lado a lado](git-team-explorer-feature-comparison.md)
- [A nova experiência de git no Visual Studio](git-with-visual-studio.md)
- [Tutorial: abrir um projeto de um repositório](../get-started/tutorial-open-project-from-repo.md)
- [Referência do Team Explorer](reference/team-explorer-reference.md)
- [Conectar-se a um projeto (Azure DevOps)](/azure/devops/organizations/projects/connect-to-projects)
- [Solucionar problemas de conexão com um projeto](/azure/devops/user-guide/troubleshoot-connection?view=azure-devops&preserve-view=true)
