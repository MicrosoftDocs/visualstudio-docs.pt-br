---
title: Controle de Versão do Team Foundation (TFVC)
description: Conexão do Visual Studio para Mac ao Team Foundation Server/Azure DevOps com o Controle de Versão do Team Foundation (TFVC).
author: heiligerdankgesang
ms.author: dominicn
ms.date: 06/25/2019
ms.technology: vs-ide-general
ms.assetid: 52D3D26A-4D01-4FD1-AAA1-AE7D7BD39746
ms.topic: troubleshooting
ms.openlocfilehash: 33d00d853c7496e23cb5cd97a0b9abbe05e3accc
ms.sourcegitcommit: 5335a9864d5747bc917ed28d4ebeade3076b10e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2020
ms.locfileid: "85950584"
---
# <a name="connecting-to-team-foundation-version-control"></a>Conexão com o Controle de Versão do Team Foundation

> [!NOTE]
> Para obter a melhor experiência de controle de versão no macOS, recomendamos o uso do Git em vez do Controle de Versão do Team Foundation (TFVC). O Git é suportado no Visual Studio para Mac e é a opção padrão para repositórios hospedados no Team Foundation Server (TFS)/Azure DevOps. Para saber mais sobre como usar o Git com o TFS/Azure DevOps, confira o artigo [Configurar um Repositório Git](/visualstudio/mac/set-up-git-repository).
>
> Se a versão prévia da extensão do TFVC para o Visual Studio para Mac foi usada anteriormente, ela não é mais compatível ao atualizar para o Visual Studio 2019 para Mac.

Azure Repos fornece dois modelos de controle de versão: [git](/azure/devops/repos/git/?view=azure-devops), um sistema de controle de versão distribuído e [controle de versão do Team Foundation](/azure/devops/repos/tfvc/index?view=azure-devops) (TFVC), um sistema de controle de versão centralizado.

O Visual Studio para Mac fornece suporte completo para repositórios Git, mas requer algumas soluções alternativas para trabalhar com o TFVC. Se você estiver usando o TFVC para o controle de versão hoje, veja abaixo algumas soluções que você poderá usar para acessar seu código-fonte hospedado no TFVC:

* [Usar o Visual Studio Code e a extensão Azure Repos, para uma interface gráfica](#use-visual-studio-code-and-the-azure-repos-extension)
* [Conectar-se ao seu repositório usando o cliente de linha de comando Team Explorer Everywhere (TEE-CLC)](#connecting-using-the-team-explorer-everywhere-command-line-client)
* [Conectar-se ao TFVC usando a extensão Controle de Versão do Team Foundation (sem suporte) para o Visual Studio para Mac](#connect-to-tfvc-using-the-team-foundation-version-control-extension)

O restante deste artigo explica as opções listadas acima.

## <a name="requirements"></a>Requisitos

* Visual Studio Community, Professional ou Enterprise para Mac versão 7.8 e posterior.
* Azure DevOps Services, Team Foundation Server 2013 e posterior, ou Azure DevOps Server 2018 e posterior.
* Um projeto no Azure DevOps Services ou no Team Foundation Server/Azure DevOps Server, configurado para usar o Controle de Versão do Team Foundation.

## <a name="use-visual-studio-code-and-the-azure-repos-extension"></a>Usar o Visual Studio Code e a extensão Azure Repos

Se você gosta de trabalhar com uma interface gráfica para gerenciar seus arquivos no controle de versão, a extensão Azure Repos para o Visual Studio Code fornece uma solução com suporte da Microsoft. Para começar, faça o download do [Visual Studio Code](https://code.visualstudio.com) e saiba como [configurar a extensão do Azure Repos](https://marketplace.visualstudio.com/items?itemName=ms-vsts.team).

## <a name="connecting-using-the-team-explorer-everywhere-command-line-client"></a>Conectar-se usando o cliente de linha de comando Team Explorer Everywhere

Se você se sentir confortável usando o macOS Terminal, o Cliente de Linha de Comando do Team Explorer Everywhere (TEE-CLC) fornecerá uma forma com suporte de se conectar à sua fonte no TFVC.

Você pode seguir as etapas abaixo para configurar sua conexão com o TFVC e confirmar as alterações.

### <a name="setting-up-the-tee-clc"></a>Configurar o TEE-CLC

Há duas maneiras de configurar com o TEE-CLC.

* Use o Homebrew para instalar o cliente ou
* Baixe e instale manualmente o cliente

A solução mais fácil é **usando o HomeBrew**, que é um gerenciador de pacotes para macOS. Para instalar usando esse método:

1. Inicie o aplicativo macOS Terminal.
1. Instale o Homebrew usando o Terminal e as instruções na [página inicial do Homebrew](https://brew.sh/).
1. Uma vez instalado o Homebrew, execute o seguinte comando no seu Terminal: `brew install tee-clc`

Para **configurar manualmente o TEE-CLC**:

1. [Faça o download da versão mais recente do tee-clc](https://github.com/Microsoft/team-explorer-everywhere/releases) da página de lançamentos do repositório GitHub Team Explorer Everywhere (por exemplo, tee-clc-14.134.0.zip no momento desta publicação).
1. Extraia o conteúdo do .zip para uma pasta no disco.
1. Abra o aplicativo macOS Terminal e use o comando `cd` para alternar para a pasta usada na etapa anterior.
1. Na pasta, execute o comando `./tf` para testar se o cliente da linha de comando pode ser executado, você pode ser solicitado a instalar o Java ou outras dependências.

Depois que o TEE-CLC estiver instalado, você poderá executar o comando `tf eula` para visualizar e aceitar o contrato de licença do cliente.

Por fim, para autenticar com seu ambiente TFS/Azure DevOps, você precisará criar um token de acesso pessoal no servidor. Saiba mais sobre [autenticação com tokens de acesso pessoal](/azure/devops/integrate/get-started/authentication/pats?view=azure-devops). Ao criar um token de acesso pessoal para usar com o TFVC, certifique-se de fornecer acesso completo ao configurar o token.

### <a name="using-the-tee-clc-to-connect-to-your-repo"></a>Usar o TEE-CLC para se conectar ao seu repositório

Para se conectar ao seu código-fonte, primeiro você precisa criar um workspace usando o comando `tf workspace`. Por exemplo, os seguintes comandos se conectam a uma Organização no Azure DevOps Services chamada "MyOrganization": 

```bash
export TF_AUTO_SAVE_CREDENTIALS=1
tf workspace -new MyWorkspace -collection:https://dev.azure.com/MyOrganization
```

A configuração do ambiente `TF_AUTO_SAVE_CREDENTIALS` é usada para salvar suas credenciais, para que você não seja solicitado a inseri-las várias vezes. Quando for solicitado um nome de usuário, use o token de acesso pessoal criado na seção anterior e use uma senha em branco.

Para criar um mapeamento de seus arquivos de origem para uma pasta local, você usará o comando `tf workfold`. O exemplo a seguir mapeará uma pasta chamada "WebApp.Services" do projeto TFVC "MyRepository" e a configurará para ser copiada para a pasta ~/Projects/ local (ou seja, uma pasta "Projects" na pasta inicial dos usuários atuais).

```bash
tf workfold -map $/MyRepository/WebApp.Services -workspace:MyWorkspace ~/Projects/
```

Por fim, use o seguinte comando para obter os arquivos de origem do servidor e copiá-los localmente:

```bash
tf get
```

### <a name="committing-changes-using-the-tee-clc"></a>Confirmar as alterações usando o TEE-CLC

Depois de fazer alterações em seus arquivos no Visual Studio para Mac, você pode voltar ao Terminal para verificar suas edições. O comando `tf add` é usado para adicionar arquivos à lista de alterações pendentes a serem registradas e o comando `tf checkin` executa a entrada real no servidor. O comando `checkin` inclui parâmetros para adicionar um comentário ou associar um item de trabalho relacionado. No snippet de código a seguir, todos os arquivos em uma pasta `WebApp.Services` são adicionados, recursivamente, ao check-in. Em seguida, o código é verificado com um comentário e associado a um item de trabalho com a ID "42".

```bash
cd WebApp.Services
tf add * /recursive
tf checkin -comment:"Replaced 'Northwand' typos with the correct word Northwind" -associate:42
```

Para aprender mais sobre os comandos mencionados aqui, ou outros, você pode usar o seguinte comando do Terminal:

`tf help`

## <a name="connect-to-tfvc-using-the-team-foundation-version-control-extension"></a>Conectar-se ao TFVC usando a extensão de Controle de Versão do Team Foundation

> [!NOTE]
> Para obter a melhor experiência de controle de versão no macOS, recomendamos o uso do Git em vez do Controle de Versão do Team Foundation (TFVC). O Git é suportado no Visual Studio para Mac e é a opção padrão para repositórios hospedados no Team Foundation Server (TFS)/Azure DevOps. Para saber mais sobre como usar o Git com o TFS/Azure DevOps, confira o artigo [Configurar um Repositório Git](/visualstudio/mac/set-up-git-repository).
>
> Se a versão prévia da extensão do TFVC para o Visual Studio para Mac foi usada anteriormente, ela não é mais compatível ao atualizar para o Visual Studio 2019 para Mac.

Na galeria da extensão do Visual Studio para Mac, há uma extensão de Controle de Versão do Team Foundation que oferece suporte limitado para se conectar ao TFVC. A extensão não é compatível e tem vários problemas conhecidos, portanto, sua experiência pode variar ao usá-la.

Para instalar a extensão, inicie o Visual Studio para Mac e escolha o menu **Visual Studio > Extensões**. Na guia **Galeria**, selecione **Controle de Versão > Controle de Versão do Team Foundation para TFS e Azure DevOps** e clique em **Instalar...**:

![Gerenciador de extensões](media/tfvc-install.png)

Siga os prompts para instalar a extensão. Depois de instalá-la, reinicie o IDE.

### <a name="updating-the-extension"></a>Atualizando a extensão

Periodicamente, são feitas atualizações na extensão do TFVC. Para acessar as atualizações, escolha **Visual Studio > Extensions...** no menu e selecione a guia **atualizações** . Selecione a extensão na lista e pressione o botão **Atualizar** :

Pressione **Instalar** na próxima caixa de diálogo para desinstalar o pacote antigo e instalar um novo.

### <a name="using-the-extension"></a>Usar a extensão

Depois de instalar a extensão, selecione o item de menu **Controle de Versão > TFS/Azure DevOps > Abrir do Repositório Remoto...**.

![Item de menu para abrir a extensão](media/tfvc-source-control-explorer-devops.png)

Escolha o VSTS ou o Team Foundation Server para começar e pressione **Continuar**:

![Conectar a um servidor](media/tfvc-choose-server-type-devops.png)

#### <a name="azure-repos-authentication"></a>Autenticação do Azure Repos

Quando você seleciona um projeto que está hospedado no Azure Repos, é solicitado que você insira os detalhes da conta Microsoft:

![Conectar-se com o Azure Repos](media/tfvc-vsts-login.png)

#### <a name="tfs-authentication"></a>Autenticação do TFS

Para conectar-se ao TFS, insira os detalhes do servidor e suas credenciais da conta. Insira um domínio para usar a autenticação NTLM, caso contrário, deixe em branco para usar a autenticação básica. Selecione **Adicionar Servidor**:

![Entrar em um servidor TFS](media/tfvc-login.png)

### <a name="selecting-a-project"></a>Selecionando um projeto

Depois que você se autenticar com êxito, será exibida uma lista de repositórios associados à conta na caixa de diálogo **Abrir do Controle do Código-Fonte**:

![Caixa de diálogo Abrir do Controle do Código-Fonte com projetos exibidos](media/tfvc-vsts-projects.png)

Essa caixa de diálogo é organizada com os seguintes nós:

- Organização ou coleção do Azure DevOps – Exibe todas as organizações conectadas à conta Microsoft com que você fez logon.
- Projetos – Em cada organização ou coleção, você pode ter um número de projetos. Um projeto é onde o código-fonte, os itens de trabalho e os builds automatizados são hospedados.

Neste ponto, você pode pesquisar e filtrar pelo nome de um projeto ou de uma organização.

#### <a name="adding-a-new-server"></a>Adicionando um novo servidor

Para adicionar um novo servidor à lista, pressione o botão **Adicionar Host** na caixa de diálogo **Abrir do Controle do Código-Fonte**:

![Botão de adição realçado para adicionar o novo servidor à lista](media/tfvc-add-new-server.png)

Selecione o provedor na lista e insira suas credenciais:

![Caixa de diálogo mostrando a opção de provedor de controle do código-fonte](media/tfvc-add-new-creds-devops.png)

### <a name="creating-a-new-workspace"></a>Criando um novo workspace

Para começar a trabalhar com um projeto, você precisa ter um _workspace_. Se você ainda não tem um workspace, crie um na caixa de combinação **Workspace** na caixa de diálogo **Abrir do Controle do Código-Fonte**:

![Opção da caixa de combinação Criar workspace](media/tfvc-create-new-workspace.png)

Defina o nome e o caminho local para seu novo workspace e selecione **Criar Workspace**:

![Inserindo um nome e um caminho local para o novo workspace](media/tfvc-local-workspace.png)

### <a name="using-the-source-code-explorer"></a>Usando o Source Code Explorer

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

### <a name="managing-workspaces"></a>Gerenciando workspaces

Se você ainda não criou um workspace, conforme descrito na seção [Criando um workspace](#creating-a-new-workspace), o Source Code Explorer estará vazio:

![Source Code Explorer vazio](media/tfvc-setup-empty-sce.png)

Para configurar seu projeto remoto com um workspace local, use as seguintes etapas:

1. Selecione o **Servidor** na caixa de combinação.
1. Observe que não há "nenhum workspace" e o caminho local está como "Não Mapeado". Selecione o link **Não Mapeado** para exibir a caixa de diálogo **Criar Workspace**.
1. Forneça um nome para o workspace e, em seguida, clique em **Adicionar Pasta de Trabalho** para mapear o projeto para uma pasta local no seu computador:

    ![Caixa de diálogo Criar Workspace, mostrando as opções padrão](media/tfvc-workspace1.png)

1. Selecione a pasta &quot;$&quot; para mapear todos os projetos em seu servidor para o mesmo workspace ou selecione um projeto individual e clique em **OK**:

    ![Navegue para a caixa de diálogo de pasta mostrando todos os projetos](media/tfvc-workspace2.png)

1. Selecione o local em seu computador local para onde deseja mapear os projetos e clique em **Selecionar Pasta**.
1. Confirme os detalhes do novo workspace pressionando **OK**

    ![Caixa de diálogo Criar Workspace, com a pasta de trabalho adicionada](media/tfvc-workspace3.png)

Depois que o workspace for configurado, ele poderá ser alterado ou removido clicando no botão **Gerenciar Workspaces** no Source Code Explorer.

![Gerenciar Workspaces](media/tfvc-workspace4.png)

## <a name="troubleshooting-and-known-issues"></a>Solução de problemas e problemas conhecidos

#### <a name="problems-using-basic-authentication"></a>Problemas no uso da autenticação básica

As opções a seguir podem ser usadas para a autenticação no servidor:

- Oauth
- Basic
- Ntlm

Para usar a autenticação Básica é necessário habilitar **Credenciais de autenticação alternativas** no Azure DevOps Services, seguindo as etapas abaixo:

1. Entre na sua organização Azure DevOps como proprietário (https:\//dev.azure.com/{organization}/{project}).

2. Na barra de ferramentas da organização, selecione o ícone de engrenagem e escolha **Política**:

    ![Opção de configurações de política selecionada](media/tfvc-auth2.png)

3. Examine as configurações de conexão do aplicativo. Altere essas configurações, com base em suas políticas de segurança:

    ![Opção de configurações de política selecionada](media/tfvc-auth.png)

#### <a name="i-do-not-see-anything-in-tfvc"></a>Não vejo nada no TFVC

Para definir o TFVC (Controle de Versão do Team Foundation) no computador de desenvolvimento, você **precisa** criar um workspace, conforme a descrição na seção [Gerenciando workspaces](#managing-workspaces).

No Source Control Explorer, pressione o botão **Gerenciar Workspaces**. Siga as etapas para mapear o projeto para uma pasta no computador de desenvolvimento.

#### <a name="i-do-not-see-any--all-of-my-projects"></a>Não vejo um/nenhum dos meus projetos

Após a autenticação, você deverá ver a lista de projetos. Por padrão, apenas os projetos do TFS são mostrados. Para ver outros tipos de projetos, marque a caixa "Ver todos os projetos".

Tenha em mente que os projetos que estão no servidor não serão exibidos se você não tiver os privilégios corretos.

##### <a name="i-am-getting-the-error-cannot-create-the-workspace-please-try-again"></a>Estou recebendo o erro "Não é possível criar o workspace. Tente novamente"

Ao tentar [criar um workspace](#creating-a-new-workspace), verifique se as seguintes condições são atendidas:

- Nenhum uso de caracteres inválidos no nome do workspace.
- O nome deve ter menos de 64 caracteres.
- O caminho local não pode ser usado por outros workspaces.

### <a name="see-also"></a>Veja também

- [Desenvolver e compartilhar seu código no TFVC usando o Visual Studio (no Windows)](/azure/devops/repos/tfvc/share-your-code-in-tfvc-vs)