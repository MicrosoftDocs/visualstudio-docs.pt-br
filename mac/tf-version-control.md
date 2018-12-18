---
title: Controle de Versão do Team Foundation (TFVC)
description: Conexão ao Team Foundation Server ou ao Azure DevOps Services com o TFVC (Controle de Versão do Team Foundation).
author: conceptdev
ms.author: crdun
ms.date: 09/05/2018
ms.topic: article
ms.technology: vs-ide-general
ms.assetid: 52D3D26A-4D01-4FD1-AAA1-AE7D7BD39746
ms.openlocfilehash: 9cb6a466d764c85012477fb2d849c05920908f02
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51295924"
---
# <a name="connecting-to-team-foundation-version-control"></a>Conexão com o Controle de Versão do Team Foundation

> [!NOTE]
> O suporte para o Controle de Versão do Team Foundation está em versão prévia no momento e algumas funcionalidades ainda não estão funcionando totalmente. Adoraríamos receber seus comentários sobre problemas na [Comunidade de Desenvolvedores](https://developercommunity.visualstudio.com/spaces/41/index.html). Mais alterações ainda estão por vir!

O Azure Repos fornece dois modelos de controle de versão: o GIT, que é o controle de versão distribuído, e o TFVC (Controle de Versão do Team Foundation), que é o controle de versão centralizado. Este artigo fornece uma visão geral e um ponto de partida para usar o TFVC com o Visual Studio para Mac.

## <a name="requirements"></a>Requisitos

* Visual Studio Community, Professional ou Enterprise para Mac versão 7.5 ou posterior.
* Azure DevOps Services ou Team Foundation Server 2013 e posterior.
* Um projeto no Azure DevOps Services ou no Team Foundation Server, configurado para usar o Controle de Versão do Team Foundation.

## <a name="installation"></a>Instalação

No Visual Studio para Mac, escolha **Visual Studio > Extensões** no menu. Na guia **Galeria**, selecione **Controle de Versão > Controle de Versão do Team Foundation para o TFS e o VSTS** e clique em **Instalar**:

![Gerenciador de extensões](media/tfvc-install.png)

Siga os prompts para instalar a extensão. Depois de instalá-la, reinicie o IDE.

## <a name="updating-the-extension"></a>Atualizando a extensão

Periodicamente, são feitas atualizações na extensão do TFVC. Para acessar as atualizações, escolha **Visual Studio > Extensões...** no menu e selecione a guia **Atualizações**. Selecione a extensão na lista e pressione o botão **Atualizar**:

![Gerenciador de extensão mostrando a atualização](media/tfvc-update.png)

Pressione **Instalar** na próxima caixa de diálogo para desinstalar o pacote antigo e instalar um novo.

Para obter informações sobre as novidades em cada versão, confira as [Notas de Versão](/visualstudio/releasenotes/vs2017-mac-preview-relnotes#team-foundation-version-control-extension--release-notes).

## <a name="using-the-add-in"></a>Usando o suplemento

Depois de instalar a extensão, selecione o item de menu **Controle de Versão > TFS/Azure DevOps > Abrir do Repositório Remoto**.

![Item de menu para abrir a extensão](media/tfvc-source-control-explorer-devops.png)

Escolha o VSTS ou o Team Foundation Server para começar e pressione **Continuar**:

![Conectar a um servidor](media/tfvc-choose-server-type-devops.png)

### <a name="azure-repos-authentication"></a>Autenticação do Azure Repos

Quando você seleciona um projeto que está hospedado no Azure Repos, é solicitado que você insira os detalhes da conta Microsoft:

![Conectar-se com o Azure Repos](media/tfvc-vsts-login.png)

### <a name="tfs-authentication"></a>Autenticação do TFS

Para conectar-se ao TFS, insira os detalhes do servidor e suas credenciais da conta. Insira um domínio para usar a autenticação NTLM, caso contrário, deixe em branco para usar a autenticação básica. Selecione **Adicionar Servidor**:

![Entrar em um servidor TFS](media/tfvc-login.png)

## <a name="selecting-a-project"></a>Selecionando um projeto

Depois que você se autenticar com êxito, será exibida uma lista de repositórios associados à conta na caixa de diálogo **Abrir do Controle do Código-Fonte**:

![Caixa de diálogo Abrir do Controle do Código-Fonte com projetos exibidos](media/tfvc-vsts-projects.png)

Essa caixa de diálogo é organizada com os seguintes nós:

- Organização ou coleção do Azure DevOps – Exibe todas as organizações conectadas à conta Microsoft com que você fez logon.
- Projetos – Em cada organização ou coleção, você pode ter um número de projetos. Um projeto é onde o código-fonte, os itens de trabalho e os builds automatizados são hospedados.

Neste ponto, você pode pesquisar e filtrar pelo nome de um projeto ou de uma organização.

### <a name="adding-a-new-server"></a>Adicionando um novo servidor

Para adicionar um novo servidor à lista, pressione o botão **Adicionar Host** na caixa de diálogo **Abrir do Controle do Código-Fonte**:

![Botão de adição realçado para adicionar o novo servidor à lista](media/tfvc-add-new-server.png)

Selecione o provedor na lista e insira suas credenciais:

![Caixa de diálogo mostrando a opção de provedor de controle do código-fonte](media/tfvc-add-new-creds-devops.png)

## <a name="creating-a-new-workspace"></a>Criando um novo workspace

Para começar a trabalhar com um projeto, você precisa ter um _workspace_. Se você ainda não tem um workspace, crie um na caixa de combinação **Workspace** na caixa de diálogo **Abrir do Controle do Código-Fonte**:

![Opção da caixa de combinação Criar workspace](media/tfvc-create-new-workspace.png)

Defina o nome e o caminho local para seu novo workspace e selecione **Criar Workspace**:

![Inserindo um nome e um caminho local para o novo workspace](media/tfvc-local-workspace.png)

## <a name="using-the-source-code-explorer"></a>Usando o Source Code Explorer

Depois de criar um workspace e mapear o projeto, você poderá começar a trabalhar com o _Source Code Explorer_.

Para abrir o Source Code Explorer, selecione o item de menu **Controle de Versão > TFS/Azure DevOps > Source Control Explorer**.

O Source Code Explorer permite que você navegue em todos os projetos mapeados e em seus arquivos e pastas. Ele também permite que você execute todas as ações básicas de controle do código-fonte, como:

- Obter a versão mais recente
- Obter uma versão específica
- Fazer check-out e check-out de arquivos
- Bloquear e desbloquear arquivos
- Adicionar, excluir e renomear arquivos
- Exibir histórico
- Comparar alterações.

Muitas dessas ações estão disponíveis por meio de ações de contexto no projeto:

![Ações de menu de contexto para um projeto](media/tfvc-sourcecode-actions.png)

## <a name="managing-workspaces"></a>Gerenciando workspaces

Se você ainda não criou um espaço de trabalho, conforme descrito na seção [Criando um espaço de trabalho](#creating-a-new-workspace), o Source Code Explorer estará vazio:

![Source Code Explorer vazio](media/tfvc-setup-empty-sce.png)

Para configurar seu projeto remoto com um workspace local, use as seguintes etapas:

1. Selecione o **Servidor** na caixa de combinação.
1. Observe que não há "nenhum workspace" e o caminho local está como "Não Mapeado". Selecione o link **Não Mapeado** para exibir a caixa de diálogo **Criar Workspace**.
1. Forneça um nome para o workspace e, em seguida, clique em **Adicionar Pasta de Trabalho** para mapear o projeto para uma pasta local no seu computador:

    ![Caixa de diálogo Criar Workspace, mostrando as opções padrão](media/tfvc-workspace1.png)

1. Selecione a pasta "$" para mapear todos os projetos em seu servidor para o mesmo espaço de trabalho ou selecione um projeto individual e clique em **OK**:

    ![Navegue para a caixa de diálogo de pasta mostrando todos os projetos](media/tfvc-workspace2.png)

1. Selecione o local em seu computador local para onde deseja mapear os projetos e clique em **Selecionar Pasta**.
1. Confirme os detalhes do novo workspace pressionando **OK**

    ![Caixa de diálogo Criar Workspace, com a pasta de trabalho adicionada](media/tfvc-workspace3.png)

Depois que o workspace for configurado, ele poderá ser alterado ou removido clicando no botão **Gerenciar Workspaces** no Source Code Explorer.

![Gerenciar Workspaces](media/tfvc-workspace4.png)

## <a name="troubleshooting"></a>Solução de problemas

### <a name="problems-using-basic-authentication"></a>Problemas no uso da autenticação básica

As opções a seguir podem ser usadas para a autenticação no servidor:

- OAuth
- Basic
- NTLM

Para usar a autenticação Básica é necessário habilitar **Credenciais de autenticação alternativas** no Azure DevOps Services, seguindo as etapas abaixo:

1. Entre em sua organização do Azure DevOps como o proprietário (https://dev.azure.com/{organization}/{project}).

2. Na barra de ferramentas da organização, selecione o ícone de engrenagem e escolha **Política**:

    ![Opção de configurações de política selecionada](media/tfvc-auth2.png)

3. Examine as configurações de conexão do aplicativo. Altere essas configurações, com base em suas políticas de segurança:

    ![Opção de configurações de política selecionada](media/tfvc-auth.png)

### <a name="i-do-not-see-anything-in-tfvc"></a>Não vejo nada no TFVC

Para definir o TFVC (Controle de Versão do Team Foundation) no computador de desenvolvimento, você **precisa** criar um workspace, conforme a descrição na seção [Gerenciando workspaces](#managing-workspaces).

No Source Control Explorer, pressione o botão **Gerenciar Workspaces**. Siga as etapas para mapear o projeto para uma pasta no computador de desenvolvimento.

### <a name="i-do-not-see-any--all-of-my-projects"></a>Não vejo um/nenhum dos meus projetos

Após a autenticação, você deverá ver a lista de projetos. Por padrão, apenas os projetos do TFS são mostrados. Para ver outros tipos de projetos, marque a caixa "Ver todos os projetos".

Tenha em mente que os projetos que estão no servidor não serão exibidos se você não tiver os privilégios corretos.

#### <a name="i-am-getting-the-error-cannot-create-the-workspace-please-try-again"></a>Estou recebendo o erro "Não é possível criar o workspace. Tente novamente"

Ao tentar [criar um workspace](#creating-a-new-workspace), verifique se as seguintes condições são atendidas:

- Nenhum uso de caracteres inválidos no nome do workspace.
- O nome deve ter menos de 64 caracteres.
- O caminho local não pode ser usado por outros workspaces.

## <a name="see-also"></a>Consulte também

- [Develop and share your code in TFVC using Visual Studio (on Windows)](/azure/devops/repos/tfvc/share-your-code-in-tfvc-vs) [Desenvolver e compartilhar seu código no TFVC usando o Visual Studio (no Windows)]