---
title: A experiência do git no Visual Studio 2019
titleSuffix: ''
description: Saiba como a nova experiência integrada do git no Visual Studio 2019 pode ajudá-lo a ser mais produtivo.
ms.date: 06/17/2021
ms.topic: overview
ms.author: tglee
author: TerryGLee
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.manager: jmartens
ms.openlocfilehash: ae5d17bfe09f2ebac5abb37c6d6ceed59c5398d3
ms.sourcegitcommit: a9526ab1556c47570286c7a7d3314af67fd1dcf0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2021
ms.locfileid: "112365450"
---
# <a name="git-experience-in-visual-studio"></a>Experiência de git no Visual Studio

O Git agora é a experiência de controle de versão padrão no Visual Studio 2019. Desde a [versão 16,6](/visualstudio/releases/2019/release-notes-v16.6), trabalhamos na criação do conjunto de recursos e na iteração com base em seus comentários. A nova experiência de git é ativada por padrão para todos com o lançamento da [versão 16,8](/visualstudio/releases/2019/release-notes/).

> [!TIP]
> O Git é o sistema de controle de versão moderno mais usado, portanto, se você for um desenvolvedor profissional ou se estiver aprendendo a codificar, o Git pode ser muito útil para você. Se você for novo no git, o https://git-scm.com/ site será um bom lugar para começar. Lá, você encontrará folhas de dicas, um livro online popular e vídeos de informações básicas sobre o git.

## <a name="how-to-use-git-in-visual-studio"></a>Como usar o Git no Visual Studio

Vamos orientá-lo sobre como usar a nova experiência de git no Visual Studio 2019, mas se você quiser fazer um tour rápido primeiro, confira o seguinte vídeo: <br><br>*Tamanho do vídeo: 5,27 minutos*

> [!VIDEO https://www.youtube.com/embed/UHrAg3iKoe0]

Há três maneiras de começar a usar o Git com o Visual Studio para ser mais produtivo:

- [Abra um repositório git existente](#open-an-existing-local-repository). Se o seu código já estiver em seu computador, você poderá abri-lo usando **arquivo**  >  **aberto**  >  **projeto/solução** (ou **pasta**) e o Visual Studio detectará automaticamente se ele tem um repositório git inicializado.
- [Crie um novo repositório git](#create-a-new-git-repository). Se o seu código não estiver associado ao git, você poderá criar um novo repositório git.
- [Clonar um repositório git existente](#clone-an-existing-git-repository). Se o código no qual você deseja trabalhar não estiver em seu computador, você poderá clonar quaisquer repositórios remotos existentes.

> [!NOTE]
> Começando também com a [versão 16,8](/visualstudio/releases/2019/release-notes/), o Visual Studio 2019 inclui uma experiência de conta do GitHub totalmente integrada. Agora você pode adicionar as contas do GitHub e do GitHub empresarial ao seu conjunto de chaves. Você poderá adicioná-los e aproveitá-los da mesma forma como faz com contas da Microsoft, o que significa que você terá um tempo mais fácil de acessar seus recursos do GitHub no Visual Studio. Para obter mais informações, consulte a página [trabalhar com contas do GitHub no Visual Studio](../ide/work-with-github-accounts.md) .

## <a name="create-a-new-git-repository"></a>Criar um novo repositório git

Se o seu código não estiver associado ao git, você poderá começar criando um novo repositório git. Para fazer isso, selecione **git**  >  **criar repositório git** na barra de menus. Em seguida, na caixa de diálogo **criar um repositório git** , insira suas informações.

:::image type="content" source="media/git-create-repository.png" alt-text="A caixa de diálogo criar um repositório git no Visual Studio.":::

A caixa de diálogo **criar um repositório git** facilita o envio por push do novo repositório para o github. Por padrão, o novo repositório é privado, o que significa que você é o único que pode acessá-lo. Se você desmarcar a caixa, seu repositório será público, o que significa que qualquer pessoa no GitHub poderá exibi-lo.

> [!TIP]
> Independentemente de seu repositório ser público ou privado, é melhor ter um backup remoto do código armazenado com segurança no GitHub, mesmo que você não esteja trabalhando com uma equipe. Isso também torna seu código disponível para você, independentemente do computador que você está usando.

Você pode optar por criar um repositório git somente local usando a opção **somente local** . Ou então, você pode vincular seu projeto local a um repositório remoto vazio existente no Azure DevOps ou qualquer outro provedor de git usando a opção **remota existente** .

## <a name="clone-an-existing-git-repository"></a>Clonar um repositório git existente

O Visual Studio inclui uma experiência de clonagem simples. Se você souber a URL do repositório que deseja clonar, poderá colar a URL na seção **local do repositório** e, em seguida, escolher o local do disco no qual deseja que o Visual Studio seja clonado.

:::image type="content" source="media/git-clone-repository.png" alt-text="A caixa de diálogo clonar um repositório git no Visual Studio.":::

Se você não souber a URL do repositório, o Visual Studio facilitará a navegação e a clonagem do seu repositório existente do GitHub ou DevOps do Azure.

### <a name="open-an-existing-local-repository"></a>Abrir um repositório local existente

Depois de clonar um repositório ou criar um, o Visual Studio detecta o repositório git e o adiciona à lista de **repositórios locais** no menu git. A partir daqui, você pode acessar e alternar rapidamente entre seus repositórios git.

:::image type="content" source="media/git-local-repositories.png" alt-text="A opção repositórios locais do menu git no Visual Studio ":::

## <a name="view-files-in-solution-explorer"></a>Exibir arquivos no Gerenciador de Soluções

Quando você clona um repositório ou abre um repositório local, o Visual Studio o alterna para o contexto do git salvando e fechando todas as soluções e projetos abertos anteriormente. Gerenciador de Soluções carrega a pasta na raiz do repositório git e examina a árvore de diretórios em busca de qualquer arquivo de exibição. Isso inclui arquivos como CMakeLists.txt ou aqueles com a extensão de arquivo. sln.

O Visual Studio ajusta sua exibição com base no arquivo de exibição que você carrega no Gerenciador de Soluções:

- Se você clonar um repositório que contém um único arquivo. sln, Gerenciador de Soluções carregar diretamente essa solução para você.
- Se Gerenciador de Soluções não detectar nenhum arquivo. sln em seu repositório, por padrão ele carregará a exibição de pasta.
- Se o repositório tiver mais de um arquivo. sln, Gerenciador de Soluções mostrará a lista de modos de exibição disponíveis para sua escolha.

Você pode alternar entre a exibição aberta no momento e a lista de exibições usando o botão **alternar exibições** na barra de ferramentas Gerenciador de soluções.

:::image type="content" source="media/git-solution-explorer-views.png" alt-text="Gerenciador de Soluções com o botão alternar modos de exibição selecionado no Visual Studio.":::

## <a name="git-changes-window"></a>Janela Alterações Git

O Git rastreia alterações de arquivo em seu repositório à medida que você trabalha e separa os arquivos em seu repositório em três categorias. Essas alterações são equivalentes ao que você veria ao inserir o `git status` comando na linha de comando:

- **Arquivos não modificados**: esses arquivos não foram alterados desde a última confirmação.
- **Arquivos modificados**: esses arquivos têm alterações desde a última confirmação, mas você ainda não os preparou para a próxima confirmação.
- **Arquivos preparados**: esses arquivos têm alterações que serão adicionadas à próxima confirmação.

Conforme você faz seu trabalho, o Visual Studio controla as alterações de arquivo em seu projeto na seção de **alterações** da janela de **alterações do git** .

:::image type="content" source="media/git-changes-window.png" alt-text="A janela de alterações do git no Visual Studio.":::

Quando estiver pronto para preparar as alterações, clique no **+** botão (mais) em cada arquivo que deseja preparar ou clique com o botão direito do mouse em um arquivo e selecione **estágio**. Você também pode preparar todos os arquivos modificados com um clique usando o botão preparar todos **+** (mais) na parte superior da seção de **alterações** .

Quando você testa uma alteração, o Visual Studio cria uma seção de **alterações em etapas** . Somente as alterações na seção de **alterações em etapas** são adicionadas à próxima confirmação, que você pode fazer selecionando **confirmar preparação**. O comando equivalente para essa ação é `git commit -m "Your commit message"` . As alterações também podem ser despreparadas clicando no botão **–** (menos). O comando equivalente para essa ação é `git reset <file_path>` despreparar um único arquivo ou `git reset <directory_path>` despreparar todos os arquivos em um diretório.

Você também pode optar por não preparar os arquivos modificados ignorando a área de preparo. Nesse caso, o Visual Studio permite que você confirme suas alterações diretamente sem precisar prepará-las. Basta inserir sua mensagem de confirmação e, em seguida, selecionar **confirmar tudo**. O comando equivalente para essa ação é `git commit -a` .

O Visual Studio também facilita a confirmação e a sincronização com um clique usando os atalhos **confirmar tudo e enviar** e **confirmar todos e sincronizar** . Quando você clica duas vezes em qualquer arquivo nas seções **alterações** e **alterações em etapas** , você pode ver uma comparação linha por linha com a versão não modificada do arquivo.

:::image type="content" source="media/git-file-version-compare.png" alt-text="A comparação linha por linha de versões de arquivo no Visual Studio ":::

> [!TIP]
> Você pode associar um item de trabalho do Azure DevOps com uma confirmação usando o caractere "#" se você estiver conectado ao repositório DevOps do Azure. Você pode conectar seu repositório DevOps do Azure por meio de **Team Explorer**  >  **gerenciar conexões**.

### <a name="select-an-existing-branch"></a>Selecionar uma ramificação existente

O Visual Studio exibe o Branch atual no seletor na parte superior da janela de **alterações do git** .

:::image type="content" source="media/git-changes-current-branch-selector.png" alt-text="Os branches atuais que você pode exibir usando o seletor na parte superior do seletor de alterações git no Visual Studio ":::

O Branch atual também está disponível na barra de status no canto inferior direito do IDE do Visual Studio.

:::image type="content" source="media/git-changes-current-branch-status-bar.png" alt-text="Os branches atuais que você pode exibir usando a barra de status no canto inferior direito no IDE do Visual Studio ":::

Em ambos os locais, você pode alternar entre branches existentes.

### <a name="create-a-new-branch"></a>Criar uma nova ramificação

Você também pode criar uma nova ramificação. O comando equivalente para essa ação é `git checkout -b <branchname>` .

A criação de uma nova ramificação é tão simples quanto inserir o nome da ramificação e baseá-la em uma ramificação existente.

:::image type="content" source="media/git-changes-create-new-branch.png" alt-text="A caixa de diálogo criar uma nova ramificação no Visual Studio ":::

Você pode escolher uma ramificação local ou remota existente como base. A caixa de seleção **Branch de check-out** alterna automaticamente para o Branch recém-criado. O comando equivalente para essa ação é `git checkout -b <new-branch><existing-branch>` .

## <a name="git-repository-window"></a>Janela do repositório git

O Visual Studio tem uma nova janela de **repositório git** , que é uma exibição consolidada de todos os detalhes em seu repositório, incluindo todas as ramificações, remotos e históricos de confirmação. Você pode acessar essa janela diretamente do **git** ou da **exibição** na barra de menus ou na barra de status.

### <a name="manage-branches"></a>Gerenciar branches

Ao selecionar **gerenciar branches** no menu **git** , você verá a exibição de árvore branches na janela **repositório git** . No painel esquerdo, você pode usar o menu de contexto de clique com o botão direito do mouse para fazer checkout de branches, criar novos branches, mesclar, trocar base, Cherry-escolha e muito mais. Ao clicar na ramificação, você poderá ver uma visualização do histórico de confirmação no painel direito.

### <a name="incoming-and-outgoing-commits"></a>Confirmações de entrada e de saída

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

::: moniker range="vs-2019"

## <a name="how-to-use-the-full-team-explorer-experience-in-visual-studio"></a>Como usar a experiência de Team Explorer completa no Visual Studio

A nova experiência do Git é o sistema de controle de versão padrão Visual Studio 2019 da versão [16.8](/visualstudio/releases/2019/release-notes/) em diante. No entanto, se você quiser desativar, poderá. Vá para **Ferramentas Opções** Recursos de Visualização do Ambiente e, em seguida, alterne a caixa de seleção Nova experiência do usuário do Git, que alterna de volta para o  >    >    >   Team Explorer git. 

:::image type="content" source="media/git-opt-new-user-experience.png" alt-text="A seção Recursos de Visualização da caixa de diálogo Opções Visual Studio ":::

::: moniker-end

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
