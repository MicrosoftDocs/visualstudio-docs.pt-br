---
title: A experiência do Git no Visual Studio 2019
titleSuffix: ''
description: Saiba como a nova experiência integrada do Git no Visual Studio 2019 pode ajudá-lo a ser mais produtivo.
ms.date: 04/01/2021
ms.topic: overview
ms.author: tglee
author: TerryGLee
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.manager: jmartens
ms.openlocfilehash: 7e8f428ea82fb36abf944b06c22e73f1b9ca9fb6
ms.sourcegitcommit: 113b7df611583307d3965984233a33355d6b0318
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/16/2021
ms.locfileid: "112126548"
---
# <a name="git-experience-in-visual-studio"></a>Experiência do Git no Visual Studio

O Git agora é a experiência de controle de versão padrão Visual Studio 2019. Desde [a versão 16.6,](/visualstudio/releases/2019/release-notes-v16.6)trabalhamos na criação do conjunto de recursos e na iteração com base em seus comentários. A nova experiência do Git é 1000001 para todos com o lançamento da [versão 16.8.](/visualstudio/releases/2019/release-notes/)

> [!TIP]
> O Git é o sistema de controle de versão moderno mais amplamente usado, portanto, se você é um desenvolvedor profissional ou se está aprendendo a codificar, o Git pode ser muito útil para você. Se você for novo no Git, o https://git-scm.com/ site será um bom lugar para começar. Lá, você encontrará folhas de consulta, um livro online popular e vídeos básicos do Git.

## <a name="how-to-use-git-in-visual-studio"></a>Como usar o Git no Visual Studio

Vamos mostrar como usar a nova experiência do Git no Visual Studio 2019, mas se você quiser fazer um tour rápido primeiro, confira o seguinte vídeo: <br><br>*Comprimento do vídeo: 5,27 minutos*

> [!VIDEO https://www.youtube.com/embed/UHrAg3iKoe0]

Há três maneiras de começar a usar o Git com Visual Studio para ser mais produtivo:

- [Abra um repositório Git existente.](#open-an-existing-local-repository) Se o código já estiver em seu computador, você poderá abri-lo usando Arquivo Aberto   >    >  **Projeto/Solução** (ou Pasta ) e o Visual Studio detectará automaticamente se ele tem um repositório Git inicializado.
- [Crie um repositório Git.](#create-a-new-git-repository) Se o código não estiver associado ao Git, você poderá criar um novo repositório Git.
- [Clone um repositório Git existente.](#clone-an-existing-git-repository) Se o código em que você gostaria de trabalhar não estiver em seu computador, você poderá clonar todos os repositórios remotos existentes.

> [!NOTE]
> A partir da [versão 16.8,](/visualstudio/releases/2019/release-notes/)o Visual Studio 2019 inclui uma experiência de conta do GitHub totalmente integrada. Agora você pode adicionar as contas do GitHub e GitHub Enterprise ao seu keychain. Você poderá adicioná-los e adotá-los da mesma forma que faz com as contas da Microsoft, o que significa que você terá um tempo mais fácil de acessar seus recursos do GitHub em Visual Studio. Para obter mais informações, consulte [a página Trabalhar com contas do GitHub Visual Studio](../ide/work-with-github-accounts.md) dados.

## <a name="create-a-new-git-repository"></a>Criar um repositório Git

Se o código não estiver associado ao Git, você poderá começar criando um novo repositório Git. Para fazer isso, selecione **Git**  >  **Create Git Repository** na barra de menus. Em seguida, na caixa de diálogo Criar um repositório **Git,** insira suas informações.

:::image type="content" source="media/git-create-repository.png" alt-text="A caixa de diálogo Criar um Repositório Git Visual Studio.":::

A **caixa de diálogo Criar um** repositório Git facilita o push do novo repositório para o GitHub. Por padrão, seu novo repositório é privado, o que significa que você é o único que pode acessá-lo. Se você desmarcar a caixa, seu repositório será público, o que significa que qualquer pessoa no GitHub poderá exibi-lo.

> [!TIP]
> Seja seu repositório público ou privado, é melhor ter um backup remoto do código armazenado com segurança no GitHub, mesmo se você não estiver trabalhando com uma equipe. Isso também disponibiliza seu código para você, independentemente do computador que você está usando.

Você pode optar por criar um repositório Git somente local usando a **opção Somente** local. Ou você pode vincular seu projeto local a um repositório remoto vazio existente no Azure DevOps ou em qualquer outro provedor Git usando a **opção Remoto** Existente.

## <a name="clone-an-existing-git-repository"></a>Clonar um repositório Git existente

Visual Studio inclui uma experiência de clone simples. Se você sabe a URL do repositório que você gostaria de clonar, pode colar a URL na seção Local do repositório e, em seguida, escolher o local do disco no qual Visual Studio clonar. 

:::image type="content" source="media/git-clone-repository.png" alt-text="A caixa de diálogo Clonar um Repositório Git Visual Studio.":::

Se você não conhece a URL do repositório, o Visual Studio facilita a navegação e, em seguida, clona o gitHub ou o repositório Azure DevOps existente.

### <a name="open-an-existing-local-repository"></a>Abrir um repositório local existente

Depois de clonar um repositório ou criar um, Visual Studio o repositório Git e  o adiciona à sua lista de Repositórios Locais no menu Git. A partir daqui, você pode acessar e alternar rapidamente entre seus repositórios Git.

:::image type="content" source="media/git-local-repositories.png" alt-text="A opção Repositórios Locais no menu Git no Visual Studio ":::

## <a name="view-files-in-solution-explorer"></a>Exibir arquivos no Gerenciador de Soluções

Quando você clona um repositório ou abre um repositório local, Visual Studio alterna para esse contexto do Git salvando e fechando soluções e projetos abertos anteriormente. Gerenciador de Soluções carrega a pasta na raiz do repositório Git e examina a árvore de diretórios em busca de arquivos de exibição. Eles incluem arquivos como CMakeLists.txt ou aqueles com a extensão de arquivo .sln.

Visual Studio ajusta sua Exibição com base em qual arquivo de exibição você carrega Gerenciador de Soluções:

- Se você clonar um repositório que contém um único arquivo .sln, Gerenciador de Soluções carregará diretamente essa solução para você.
- Se Gerenciador de Soluções não detectar nenhum arquivo .sln em seu repositório, por padrão, ele carregará o Modo de Exibição de Pasta.
- Se o repositório tiver mais de um arquivo .sln, Gerenciador de Soluções mostrará a lista de Exibições disponíveis para sua escolha.

Você pode alternar entre a Exibição aberta no  momento e a lista de Exibições usando o botão Alternar Exibições na barra de ferramentas Gerenciador de Soluções aplicativo.

:::image type="content" source="media/git-solution-explorer-views.png" alt-text="Gerenciador de Soluções com o botão Alternar Exibições selecionado Visual Studio.":::

## <a name="git-changes-window"></a>Janela Alterações Git

O Git rastreia as alterações de arquivo em seu repositório enquanto você trabalha e separa os arquivos em seu repositório em três categorias. Essas alterações são equivalentes ao que você verá ao inserir o `git status` comando na linha de comando:

- **Arquivos não modificados:** esses arquivos não foram alterados desde sua última confirmação.
- **Arquivos modificados:** esses arquivos têm alterações desde a última confirmação, mas você ainda não os treinou para a próxima confirmação.
- **Arquivos em fases:** esses arquivos têm alterações que serão adicionadas à próxima confirmação.

Ao fazer seu trabalho, Visual Studio o controle das alterações de  arquivo em seu projeto na seção Alterações da **janela Alterações do Git.**

:::image type="content" source="media/git-changes-window.png" alt-text="A janela Alterações do Git Visual Studio.":::

Quando estiver pronto para preparar as alterações, clique no botão (mais) em cada arquivo que deseja preparar ou clique com o botão direito do mouse em um arquivo e **+** selecione **Estágio**. Você também pode fazer o estágio de todos os arquivos modificados com um clique usando o botão de estágio tudo **+** (mais) na parte superior da **seção** Alterações.

Quando você faz uma alteração, Visual Studio cria uma **seção Alterações em Fases.** Somente as alterações na **seção Alterações em** Fases são adicionadas à próxima confirmação, o que pode ser feito selecionando Commit **Staged**. O comando equivalente para essa ação é `git commit -m "Your commit message"` . As alterações também podem ser desatagadas clicando no **botão –** (menos). O comando equivalente para essa ação é `git reset <file_path>` desemocar um único arquivo ou `git reset <directory_path>` desemocar todos os arquivos em um diretório.

Você também pode optar por não preparação dos arquivos modificados ignorando a área de preparação. Nesse caso, o Visual Studio permite que você commit suas alterações diretamente sem precisar adá-las. Basta inserir sua mensagem de commit e, em seguida, **selecionar Commit All**. O comando equivalente para essa ação é `git commit -a` .

Visual Studio também facilita a confirmação e a sincronização com um clique usando os atalhos **Commit All** e Push e Commit All **e Sync.** Ao clicar duas vezes em  qualquer  arquivo nas seções Alterações e Alterações em fases, você poderá ver uma comparação linha a linha com a versão não modificada do arquivo.

:::image type="content" source="media/git-file-version-compare.png" alt-text="A comparação linha a linha de versões de arquivo no Visual Studio ":::

> [!TIP]
> Você pode associar um Azure DevOps de trabalho a uma confirmação usando o caractere "#" se estiver conectado ao repositório Azure DevOps. Você pode conectar seu repositório Azure DevOps por meio **Team Explorer**  >  **Gerenciar Conexões**.

### <a name="select-an-existing-branch"></a>Selecionar um branch existente

Visual Studio exibe o branch atual no seletor na parte superior da janela **Alterações do Git.**

:::image type="content" source="media/git-changes-current-branch-selector.png" alt-text="Os branches atuais que você pode exibir usando o seletor na parte superior do seletor de Alterações do Git Visual Studio ":::

O branch atual também está disponível na barra de status no canto inferior direito do Visual Studio IDE.

:::image type="content" source="media/git-changes-current-branch-status-bar.png" alt-text="Os branches atuais que você pode exibir usando a barra de status no canto inferior direito no Visual Studio IDE ":::

Em ambos os locais, você pode alternar entre branches existentes.

### <a name="create-a-new-branch"></a>Criar uma nova ramificação

Você também pode criar um branch. O comando equivalente para essa ação é `git checkout -b <branchname>` .

Criar um branch é tão simples quanto inserir o nome do branch e baseá-lo em um branch existente.

:::image type="content" source="media/git-changes-create-new-branch.png" alt-text="A caixa de diálogo Criar um Novo Branch no Visual Studio ":::

Você pode escolher um branch local ou remoto existente como a base. A **caixa de seleção Branch** de check-out alterna automaticamente você para o branch recém-criado. O comando equivalente para essa ação é `git checkout -b <new-branch><existing-branch>` .

## <a name="git-repository-window"></a>Janela Repositório Git

Visual Studio tem uma nova janela repositório **Git,** que é uma exibição consolidada de todos os detalhes em seu repositório, incluindo todos os branches, remotos e históricos de confirmação. Você pode acessar essa janela diretamente do **Git** ou **exibição** na barra de menus ou na barra de status.

### <a name="manage-branches"></a>Gerenciar branches

Ao selecionar **Gerenciar Branches** no menu **Git,** você verá o exibição de árvore de branches na janela **Repositório Git.** No painel esquerdo, você pode usar o menu de contexto do clique com o botão direito do mouse para fazer check-out de branches, criar novos branches, mesclar, rebase, pick-pick e muito mais. Ao clicar no branch, você poderá ver uma visualização de seu histórico de confirmação no painel direito.

### <a name="incoming-and-outgoing-commits"></a>Confirmações de entrada e saída

Quando você busca um branch, a janela Alterações do **Git** tem um indicador na lista de invasões do branch, que exibe o número de confirmações nãopuladas do branch remoto. Esse indicador também mostra o número de confirmações locais não explicadas.

:::image type="content" source="media/git-repo-drop-down-indicator.png" alt-text="A janela Alterações do Git que mostra o elemento de interface do usuário do indicador no Visual Studio ":::

O indicador também funciona como um link para levar você ao histórico de confirmação desse branch na janela **Repositório Git.** A parte superior do histórico agora exibe os detalhes dessas confirmações de entrada e saída. A partir daqui, você também pode optar por Pull ou Push das confirmações.

:::image type="content" source="media/git-branch-commit-history.png" alt-text="A janela Repositório Git que mostra o histórico de confirmação de um branch no Visual Studio ":::

#### <a name="commit-details"></a>Detalhes da confirmação

Quando você clica duas vezes em **um commit**, Visual Studio abre seus detalhes em uma janela de ferramenta separada. A partir daqui, você pode reverter a confirmação, redefinir a confirmação, corrigir a mensagem de confirmação ou criar uma marca na confirmação. Quando você clica em um arquivo alterado na confirmação, Visual Studio abre a exibição **Diff** lado a lado da confirmação e seu pai.

:::image type="content" source="media/git-branch-commit-details.png" alt-text="A caixa de diálogo Detalhes da Confirmação Visual Studio ":::

## <a name="handle-merge-conflicts"></a>Lidar com conflitos de mesclagem

Conflitos poderão ocorrer durante uma mesclagem se dois desenvolvedores modificarem as mesmas linhas em um arquivo e o Git não saber automaticamente qual está correto. O Git interrompe a mesclagem e informa que você está em um estado conflitantes.

Visual Studio facilita a identificação e a resolução de um conflito de mesclagem. Primeiro, a **janela Repositório Git** mostra uma barra de informações ouro na parte superior da janela.

:::image type="content" source="media/git-merge-conflict-gold-bar.png" alt-text="A mensagem 'Mesclagem concluída com conflitos' Visual Studio ":::

A **janela Alterações git** também exibe uma mensagem ' Mesclagem está em andamento com conflitos ', com os arquivos não mesclados em sua seção separada abaixo dela.

:::image type="content" source="media/git-merge-progress-conflicts-message.png" alt-text="A mensagem 'Mesclar em andamento com conflitos' Visual Studio ":::

Mas se você não tiver nenhuma dessas janelas abertas e, em vez disso, ir para o arquivo que tem conflitos de mesclagem, não será preciso pesquisar o seguinte texto:

```bash
    <<<<<<< HEAD
    =======
    >>>>>>> main
```

Em vez Visual Studio exibe uma barra de informações ouro na parte superior da página que indica que o arquivo aberto tem conflitos. Em seguida, você pode clicar no link para abrir o **Editor de Mesclagem**.

:::image type="content" source="media/git-merge-conflict-gold-info-bar.png" alt-text="Captura de tela da mensagem 'Arquivo contém conflitos de mesclagem' Visual Studio ":::

### <a name="the-merge-editor"></a>O Editor de Mesclagem

O Editor de Mesclagem no Visual Studio é uma ferramenta de mesclagem de três vias que exibe as alterações de entrada, as alterações atuais e o resultado da mesclagem. Você pode usar a barra de ferramentas no nível superior do **Editor** de Mesclagem para navegar entre conflitos e diferenças mescladas automaticamente no arquivo.

:::image type="content" source="media/git-merge-editor.png" alt-text="O Editor de Mesclagem no Visual Studio ":::

Você também pode usar as alternâncias para mostrar/ocultar diferenças, mostrar/ocultar diferenças de palavras e personalizar o layout. Há caixas de seleção na parte superior de cada lado que você pode usar para fazer todas as alterações de um lado ou de outro. Mas, para fazer alterações individuais, você pode clicar nas caixas de seleção à esquerda das linhas conflitantes em ambos os lados. Por fim, ao concluir a resolução dos conflitos, você pode selecionar o botão Aceitar **Mesclagem** no Editor de Mesclagem. Em seguida, você escreve uma mensagem de confirmação e confirma as alterações para concluir a resolução.

## <a name="personalize-your-git-settings"></a>Personalizar as configurações do Git

Para personalizar e personalizar as configurações do Git em um nível de repositório, bem como em um nível global, vá para Configurações do **Git** na barra de menus ou para Ferramentas Opções Controle do Código-Fonte na barra  >  de   >    >   menus. Em seguida, escolha [as opções](git-settings.md) que você deseja.

:::image type="content" source="media/git-options-settings.png" alt-text="A caixa de diálogo Opções em que você pode escolher configurações de personalização e personalização Visual Studio IDE ":::

## <a name="how-to-use-the-full-team-explorer-experience-in-visual-studio"></a>Como usar a experiência de Team Explorer completa no Visual Studio

A nova experiência do Git é o sistema de controle de versão padrão Visual Studio 2019 da versão [16.8](/visualstudio/releases/2019/release-notes/) em diante. No entanto, se você quiser desativar, poderá. Vá para **Ferramentas Opções** Recursos de Visualização do Ambiente e, em seguida, alterne a caixa de seleção Nova experiência do usuário do Git, que alterna de volta para o  >    >    >   Team Explorer git. 

:::image type="content" source="media/git-opt-new-user-experience.png" alt-text="A seção Recursos de Visualização da caixa de diálogo Opções Visual Studio ":::

## <a name="whats-next"></a>O que vem a seguir

Embora a nova experiência do Git agora seja acionada por padrão no Visual Studio 2019 versão [16.8,](/visualstudio/releases/2019/release-notes/)continuamos adicionando novos recursos para aprimorar a experiência. Se você quiser conferir novas atualizações para a experiência do Git em uma versão prévia, poderá baixá-la e instalá-la Visual Studio Preview [página.](https://aka.ms/vspreview/)

> [!IMPORTANT]
> Se você tiver uma sugestão para nós, entre em contato conosco! Agradecemos a oportunidade de se envolver com você em decisões de design por meio do portal [**Developer Community.**](https://aka.ms/vs-suggest)

## <a name="see-also"></a>Confira também

- [Introdução ao Git e ao GitHub Visual Studio](/learn/modules/visual-studio-github-push/) tutorial sobre Microsoft Learn
- Vídeo [Introdução ao Git no Visual Studio](https://www.youtube.com/watch?v=GCZ9x3yqkyc) no YouTube
- [Anunciando o lançamento da experiência do Git Visual Studio](https://devblogs.microsoft.com/visualstudio/announcing-the-release-of-the-git-experience-in-visual-studio/) postagem no blog
- [O lançamento do novo vídeo de experiência do Git](https://www.youtube.com/watch?v=UHrAg3iKoe0&t) no YouTube
- [A Visual Studio Toolbox apresenta: O novo](https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/The-New-Git-Experience) vídeo de experiência do Git no Channel 9 e no [YouTube](https://www.youtube.com/watch?v=ZiQ2LXtAJ6I&feature=youtu.be)
- [Novas atualizações interessantes para a experiência do Git Visual Studio](https://devblogs.microsoft.com/visualstudio/exciting-new-updates-to-the-git-experience-in-visual-studio/) postagem no blog
- [Experiência aprimorada do Git Visual Studio postagem no blog 2019](https://devblogs.microsoft.com/visualstudio/improved-git-experience-in-visual-studio-2019/)
- [Trabalhar com contas do GitHub no Visual Studio](../ide/work-with-github-accounts.md)
- [Visual Studio notas de versão de 2019](/visualstudio/releases/2019/release-notes)
