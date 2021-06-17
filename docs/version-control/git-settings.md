---
title: Configurações do Git Visual Studio
titleSuffix: ''
description: Saiba como Visual Studio arquivos .gitconfig e configurações do Git para gerenciar suas preferências
ms.date: 06/08/2021
ms.topic: conceptual
ms.author: prnadago
author: prnadago
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.manager: jmartens
monikerRange: '>=vs-2019'
ms.openlocfilehash: f8dd9781833706a73b82a71236d42cc71c9fb9ec
ms.sourcegitcommit: 113b7df611583307d3965984233a33355d6b0318
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/16/2021
ms.locfileid: "112126607"
---
# <a name="git-settings-and-preferences-in-visual-studio"></a>Configurações e preferências do Git Visual Studio

No Visual Studio, você pode configurar e exibir configurações e preferências comuns do Git, como seu nome e endereço de email, suas ferramentas de mesclagem e comparação preferenciais e muito mais. Essas configurações e preferências podem ser  exibidas e configuradas na caixa de diálogo Opções na página Configurações **Globais** do Git (aplica-se a todos os seus **repositórios)** ou na página Configurações do Repositório Git (aplica-se ao repositório atual).

Você pode definir dois tipos de configurações:

- [Configurações do Git](#git-settings) – as configurações nesta seção correspondem às configurações do Git salvas nos arquivos de configuração do Git. Essas configurações podem ser exibidas e modificadas Visual Studio, mas são gerenciadas por arquivos de configuração do Git.
- [Visual Studio configurações –](#visual-studio-settings) as configurações nesta seção definem as configurações e as preferências relacionadas ao Git que são gerenciadas pelo Visual Studio.

## <a name="how-to-configure-settings"></a>Como definir configurações

1. Para definir as configurações do Git Visual Studio, escolha **Configurações** no menu Git de nível superior.

   :::image type="content" source="media/git-menu-settings.png" alt-text="O menu Git com um callout para o comando Configurações.":::

2. Escolha **Configurações Globais do Git** ou **Configurações** do Repositório Git para exibir e definir configurações de nível global ou de repositório.

   :::image type="content" source="media/source-control-settings.png" alt-text="O painel de navegação na caixa de diálogo Opções com um texto explicando as configurações do Git.":::

3. Você pode definir várias configurações comuns do Git, conforme descrito nas seções a seguir deste artigo. Depois de definir as configurações desejadas, selecione **OK** para salvar as configurações atualizadas.

   :::image type="content" source="media/ok-button.png" alt-text="A área de exibição da caixa de diálogo Opções com um texto explicador para o botão OK.":::

## <a name="git-settings"></a>Configurações do Git

Você também pode configurar e verificar algumas das definições de configuração mais comuns do Git. Você pode exibir e modificar as seguintes configurações Visual Studio, mesmo que elas sejam gerenciadas por arquivos de configuração do Git.

- [Nome e email](#name-and-email)
- [Remoção de branches remotos durante a busca](#prune-remote-branches-during-fetch)
- [Rebasear o branch local ao esvasar](#rebase-local-branch-when-pulling)
- [Provedor de rede criptográfico](#cryptographic-network-provider)
- [Auxiliar de credenciais](#credential-helper)
- [Diff & merge Tools](#diff--merge-tools)
- [Arquivos Git](#git-files)
- [Controles remotos](#remotes)
- [Outras configurações](#other-settings)

>[!NOTE]
>As configurações do Git configuradas  nas Configurações Globais do Visual Studio correspondem às configurações no arquivo  de configuração específico do usuário do Git e as configurações em Configurações do Repositório correspondem às configurações no arquivo de configuração específico do repositório. Para obter mais informações sobre a configuração do Git, consulte o capítulo Pro Git sobre como personalizar [o Git,](https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration)a documentação [do git-config](https://git-scm.com/docs/git-config)e a referência do Git Pro nos [arquivos de configuração](https://git-scm.com/docs/git-config#FILES). Para definir as configurações do Git não expostas no Visual Studio, use o comando para gravar um `git config` valor em seus arquivos de configuração: `git config [--local|--global|--system] section.key value` .

### <a name="name-and-email"></a>Nome e email

O nome e o email que você fornecer serão usados como as informações do committer para qualquer confirmação que você fizer. Essa configuração está disponível em escopos globais e de repositório e corresponde às configurações de user.name e user.email `git config` [](https://git-scm.com/docs/git-config#Documentation/git-config.txt-username) configurações. [](https://git-scm.com/docs/git-config#Documentation/git-config.txt-useremail)

1. No menu Git, vá para **Configurações.** Para definir o nome de usuário e o email no nível global, acesse **Configurações Globais do Git;** para definir o nome de usuário e o email no nível do repositório, acesse **Configurações do Repositório Git.**

2. Forneça seu nome de usuário e email e escolha **OK** para salvar. 

   :::image type="content" source="media/user-email-setting.png" alt-text="Painel configurações globais do Git na caixa de diálogo Opções com um texto explicando o nome de usuário de um email.":::

### <a name="prune-remote-branches-during-fetch"></a>Remoção de branches remotos durante a busca

A remoção remove branches de acompanhamento remoto que não existem mais no remoto e ajuda você a manter a lista de branches limpa e atualizada. Essa configuração está disponível em escopos globais e de repositório e corresponde à `git config` [configuração fetch.prune.](https://git-scm.com/docs/git-config#Documentation/git-config.txt-fetchprune)

É recomendável definir essa opção **como True** no nível global. As configurações válidas são, da seguinte forma:

- True (recomendado)
- Falso
- Desaquete (padrão)

1. No menu Git, vá para **Configurações.** Acesse **Configurações Globais do Git** para configurar essa opção no nível global; acesse **Configurações do Repositório Git** para configurar essa opção no nível do repositório.

2. De **definir Remoção de branches remotos durante a busca** como **True** (recomendado). Selecione **Ok** para salvar.

:::image type="content" source="media/prune-setting.png" alt-text="Captura de tela que mostra &quot;Remoção de branches remotos durante a busca&quot; realçada e com &quot;True&quot; selecionado na lista lista.":::    

### <a name="rebase-local-branch-when-pulling"></a>Rebasear o branch local ao esvasar

A rebasing reserva as alterações feitas por confirmações no branch atual que não estão no branch upstream, redefine o branch atual para o branch upstream e aplica as alterações que foram deixadas de lado. Essa configuração está disponível em escopos globais e de repositório e corresponde à `git config` [configuração pull.rebase.](https://git-scm.com/docs/git-config#Documentation/git-config.txt-pullrebase) As configurações válidas são, da seguinte forma:

- True: rebaixe o branch atual sobre o branch upstream após a busca.
- False: mescla o branch atual no branch upstream.
- Desaixar (padrão): a menos que especificado em outros arquivos de configuração, mesce o branch atual no branch upstream.
- Interativo: rebase no modo interativo.
- Preservar: rebaixar sem nivelar confirmações de mesclagem criadas localmente.

1. No menu Git, vá para **Configurações.** Acesse **Configurações Globais do Git** para configurar essa opção no nível global; acesse **Configurações do Repositório Git** para configurar essa opção no nível do repositório.

2. De **definir Rebase do branch local ao estorar** para a configuração desejada e selecione **OK** para salvar.

    :::image type="content" source="media/rebase-setting.png" alt-text="Captura de tela que mostra a opção &quot;Rebase local branch ao esvasar&quot; realçada e &quot;True&quot; selecionada na lista baixa.":::

Não é possível configurar para `pull.rebase` Interativo **no** Visual Studio. Visual Studio não tem suporte interativo de base.
Para configurar `pull.rebase` o para usar o modo interativo, use a linha de comando.

### <a name="cryptographic-network-provider"></a>Provedor de rede criptográfico

O provedor de rede criptográfica é uma definição de configuração do Git no escopo global que define qual back-end TLS/SSL usar em runtime e corresponde à configuração `git config` [http.sslBackend.](https://git-scm.com/docs/git-config#Documentation/git-config.txt-httpsslBackend) Os valores são, da seguinte forma:

- OpenSSL: use [OpenSSL](https://www.openssl.org/) para protocolos TLS e SSL.
- Canal Seguro: use [o Canal Seguro (schannel)](/windows/win32/secauthn/secure-channel) para protocolos TLS e SSL. O Schannel é a solução nativa do Windows, acessando o Windows Credential Store, permitindo assim o gerenciamento de certificados em toda a empresa.
- Desafina (padrão): se essa configuração for desafina, OpenSSL será o padrão.

1. No menu Git, vá para **Configurações.** Acesse **Configurações Globais do Git** para definir essa configuração.

2. De **definir Provedor de rede criptográfico** com o valor desejado e selecione **OK** para salvar.

   :::image type="content" source="media/network-provider-setting.png" alt-text="Captura de tela que mostra 'Provedor de rede criptográfico' realçada com 'OpenSSL' selecionado na lista de lista.":::

### <a name="credential-helper"></a>Auxiliar de credenciais

Quando Visual Studio executa uma operação remota do Git, o ponto de extremidade remoto pode rejeitar a solicitação porque exige que as credenciais sejam fornecidas com a solicitação. Nesse momento, o Git invoca um auxiliar de credencial, que retornará as credenciais necessárias para executar a operação e, em seguida, tentará a solicitação novamente. O auxiliar de credencial usado corresponde à `git config` [configuração credential.helper.](https://git-scm.com/docs/gitcredentials) Ele está disponível no escopo global com os seguintes valores:

- GCM para Windows: use [o Git Gerenciador de Credenciais para Windows](https://github.com/microsoft/Git-Credential-Manager-for-Windows) como auxiliar.
- GCM Core: use [o Git Gerenciador de Credenciais Core](https://github.com/microsoft/Git-Credential-Manager-Core) como auxiliar.
- Desconhece (padrão): se essa configuração não for definida, o auxiliar de credencial definido na configuração do sistema será usado. A partir do Git para Windows 2.29, o auxiliar de credencial padrão é o GCM Core.

1. No menu Git, vá para **Configurações.** Acesse **Configurações Globais do Git** para definir essa configuração.

2. De **definir Auxiliar de credencial** como o valor desejado e selecione **OK** para salvar.

:::image type="content" source="media/credential-helper-setting.png" alt-text="Captura de tela mostrando a configuração do auxiliar de credenciais na caixa de diálogo Opções.":::

### <a name="diff--merge-tools"></a>Diff & de mesclagem

O Git mostrará diferenças e conflitos de mesclagem em suas ferramentas preferenciais. As configurações nesta seção correspondem às `git config` [configurações diff.tool](https://git-scm.com/docs/git-config#Documentation/git-config.txt-difftool) e [merge.tool.](https://git-scm.com/docs/git-config#Documentation/git-config.txt-mergetool) Você pode configurar o Git para usar Visual Studio como sua ferramenta de mesclagem ou comparação em Configurações **Globais** do Git e Configurações do Repositório **Git** selecionando **Usar Visual Studio**. Para configurar outras ferramentas de comparação e mesclagem, use com a `git config` [opção diff.tool](https://git-scm.com/docs/git-config#Documentation/git-config.txt-difftool) ou [merge.tool.](https://git-scm.com/docs/git-config#Documentation/git-config.txt-mergetool)

:::image type="content" source="media/tools-setting.png" alt-text="Captura de tela que mostra a seção para definir a ferramenta Diff padrão e a ferramenta Mesclar na caixa de diálogo Opções.":::

### <a name="git-files"></a>Arquivos Git

Você pode usar a seção **Arquivos Git** no escopo Configurações do Repositório **Git** para exibir e editar os arquivos [gitignore](https://git-scm.com/docs/gitignore) e [gitattributes](https://git-scm.com/docs/gitattributes) para seu repositório.

:::image type="content" source="media/git-files-setting.png" alt-text="Captura de tela que mostra a seção para exibir e editar os arquivos de ignorar e atributos em seu repositório.":::

### <a name="remotes"></a>Remotos

Você pode usar o painel **remotos** em **configurações do repositório git** para configurar os remotos para seu repositório. Essa configuração corresponde ao comando [remoto do git](https://git-scm.com/docs/git-remote) e permite que você adicione, edite ou remova remotos.

:::image type="content" source="media/remotes-settings.png" alt-text="Captura de tela mostrando o painel remotos git na caixa de diálogo opções.":::

### <a name="other-settings"></a>Outras configurações

Para exibir todas as outras definições de configuração do git, você pode abrir e exibir os próprios arquivos de configuração ou pode executar `git config --list` para exibir as configurações.

## <a name="visual-studio-settings"></a>Configurações do Visual Studio

As configurações a seguir gerenciam as preferências relacionadas ao git no Visual Studio e são gerenciadas pelo Visual Studio em vez de arquivos de configuração do git. Todas as configurações nesta seção são definidas na página de **configurações globais do git** .

- [Local padrão](#default-location)
- [Fechar soluções abertas que não estão sob o Git ao abrir um repositório](#close-open-solutions-not-under-git-when-opening-a-repository)
- [Habilitar o download de imagens do autor de fontes de terceiros](#enable-download-of-author-images-from-third-party-sources)
- [Confirmar alterações após mesclar por padrão](#commit-changes-after-merge-by-default)
- [Habilitar Push--Force](#enable-push---force-with-lease)
- [Abrir pasta no Gerenciador de Soluções ao abrir um repositório git](#open-folder-in-solution-explorer-when-opening-a-git-repository)
- [Carregar automaticamente a solução ao abrir um repositório git](#automatically-load-the-solution-when-opening-a-git-repository)
- [Fazer check-out automaticamente de branches com o clique duplo ou a tecla Enter](#automatically-check-out-branches-with-double-click-or-the-enter-key)

### <a name="default-location"></a>Local padrão

**Local padrão** configura a pasta padrão na qual os repositórios são clonados.

:::image type="content" source="media/default-location-setting.png" alt-text="Captura de tela mostrando o campo local padrão na caixa de diálogo opções.":::

### <a name="close-open-solutions-not-under-git-when-opening-a-repository"></a>Fechar soluções abertas que não estão sob o Git ao abrir um repositório

Por padrão, o Visual Studio fecha qualquer solução ou pasta aberta quando você alterna para outro repositório. Quando isso for feito, ele também poderá carregar a solução ou a pasta do novo repositório com base em se você optar por [abrir a pasta no Gerenciador de soluções ao abrir um repositório git](#open-folder-in-solution-explorer-when-opening-a-git-repository) e [carregar automaticamente a solução ao abrir um repositório git](#automatically-load-the-solution-when-opening-a-git-repository). Isso mantém a consistência entre o Open Code e o Open Repository. No entanto, se sua solução não estiver na mesma raiz de pasta que seu repositório, convém manter a solução aberta quando você alternar para seu repositório. Você pode fazer isso com essa configuração. Os valores são os seguintes:

- Sim: quando um repositório é aberto, a solução atualmente aberta é sempre fechada
- Não: quando um repositório é aberto, o Visual Studio executa uma verificação se a solução atual está no git. Se não estiver, a solução permanecerá aberta.
- Sempre perguntar (padrão): quando isso é definido, você pode fazer uma escolha por meio de uma caixa de diálogo por repositório aberta, independentemente de você desejar manter a solução atual aberta ou fechá-la.

:::image type="content" source="media/close-sln-setting.png" alt-text="Captura de tela mostrando a configuração fechar solução na caixa de diálogo opções.":::


### <a name="enable-download-of-author-images-from-third-party-sources"></a>Habilitar o download de imagens do autor de fontes de terceiros

Habilitar o download de imagens do autor de fontes de terceiros é uma configuração específica do Visual Studio no escopo global. Quando marcada, as imagens do autor são baixadas do [serviço de imagem Gravatar](https://en.gravatar.com/), se disponível, e exibidas nas exibições confirmar e histórico.

:::image type="content" source="media/download-image-setting.png" alt-text="Captura de tela mostrando a caixa de seleção para habilitar o download de imagens do autor de uma fonte de terceiros no diálogo opções. ":::

>[!IMPORTANT]
>Para fornecer imagens de autor nas exibições de confirmação e de histórico, a ferramenta cria um hash MD5 para os endereços de email do autor armazenados no repositório ativo. Esse hash é enviado para Gravatar para localizar um valor de hash correspondente para os usuários que se inscreveram anteriormente para o serviço. Se uma correspondência for encontrada, a imagem do usuário será recuperada do serviço e exibida no Visual Studio. Os usuários que não tiverem configurado o serviço retornarão uma imagem gerada aleatoriamente. Observe que os endereços de email não são gravados pelo Visual Studio, nem são compartilhados com o Gravatar ou com terceiros.

### <a name="commit-changes-after-merge-by-default"></a>Confirmar alterações após mesclar por padrão

Quando a **confirmação é alterada após a mesclagem por padrão** , o Git cria automaticamente uma nova confirmação quando um Branch é mesclado com o Branch atual.

:::image type="content" source="media/merge-commit-setting.png" alt-text="Captura de tela mostrando a caixa de seleção para confirmar as alterações após mesclar por padrão na caixa de diálogo opções.":::

- Quando marcada, `git merge` os comandos emitidos pelo Visual Studio são executados com a `--commit` opção.
- Quando desmarcado, `git merge` os comandos emitidos pelo Visual Studio são executados com as `--no-commit --no-ff` opções.

Para obter mais informações sobre essas opções, consulte [--Commit e--no-Commit](https://git-scm.com/docs/git-merge#Documentation/git-merge.txt---commit) e [--no-FF](https://git-scm.com/docs/git-merge#Documentation/git-merge.txt---no-ff).

### <a name="enable-push---force-with-lease"></a>Habilitar Push--Force-com-Lease

Quando habilitada, essa configuração permite que você `push --force-with-lease` entre no Visual Studio. Por padrão, **habilitar Push--Force-with-Lease** está desabilitado.

:::image type="content" source="media/push-force-setting.png" alt-text="Captura de tela mostrando a caixa de seleção para habilitar o push Force com concessão na caixa de diálogo opções.":::

Para obter mais informações, consulte [Push--Force-by-Lease](https://git-scm.com/docs/git-push#Documentation/git-push.txt---no-force-with-lease).

### <a name="open-folder-in-solution-explorer-when-opening-a-git-repository"></a>Abrir pasta no Gerenciador de Soluções ao abrir um repositório git
<!-- todo: write section -->
Quando você usa o Visual Studio para abrir ou alternar para um repositório git, o Visual Studio carrega o conteúdo git para que você possa exibir alterações, confirmações, ramificações e gerenciar seu repositório de dentro do IDE. Além disso, o Visual Studio também carregará o código do repositório em Gerenciador de Soluções. O Visual Studio examinará a pasta do repositório em busca de soluções, CMakeLists.txt ou qualquer outro arquivo de exibição que ele reconheça e as exibirá como uma lista no Gerenciador de Soluções. A partir daí, você pode selecionar uma solução para carregar ou a pasta para exibir o conteúdo do diretório. Ao desativar essa caixa de seleção, o Visual Studio não abrirá a pasta do repositório em Gerenciador de Soluções. Essencialmente, isso permitirá que você abra o Visual Studio apenas como um Gerenciador de repositório git. Esta configuração está ativada por padrão.

:::image type="content" source="media/open-folder-setting.png" alt-text="Captura de tela que mostra a caixa de seleção para abrir a pasta ao abrir um repositório git na caixa de diálogo opções.":::

### <a name="automatically-load-the-solution-when-opening-a-git-repository"></a>Carregar automaticamente a solução ao abrir um repositório git

Essa configuração é aplicável somente quando a [pasta abrir no Gerenciador de soluções ao abrir uma configuração de repositório git](#open-folder-in-solution-explorer-when-opening-a-git-repository) está ativada. Quando você abre um repositório git no Visual Studio e a verificação de pasta subsequente detecta que há apenas uma solução presente no repositório, o Visual Studio carrega automaticamente essa solução. Se você desativar a configuração, a Gerenciador de Soluções exibirá a única solução presente no repositório na lista de exibições. Mas ele não carregará a solução. Por padrão, essa configuração está desativada.

:::image type="content" source="media/load-solution-setting.png" alt-text="Captura de tela mostrando a caixa de seleção para carregar automaticamente a solução ao abrir um repositório git na caixa de diálogo opções.":::

### <a name="automatically-check-out-branches-with-double-click-or-the-enter-key"></a>Fazer check-out automaticamente de branches com o clique duplo ou a tecla Enter

A janela do repositório Git tem uma lista de branches exibidos em uma estrutura de árvore. A seleção única de uma ramificação alternará o painel Histórico de confirmação para exibir as confirmações da ramificação selecionada. Para fazer check-out de uma ramificação, você pode clicar com o botão direito do mouse para abrir o menu de contexto e selecionar **checkout**. Se você ativar essa configuração, clicar duas vezes ou pressionar a tecla Enter fará check-out do Branch e exibirá suas confirmações. 
  
:::image type="content" source="media/checkout-branch-setting.png" alt-text="Captura de tela mostrando a caixa de seleção para fazer check-out de ramificações com dois cliques ou Enter Key na caixa de diálogo Options.":::


## <a name="see-also"></a>Confira também

> [!IMPORTANT]
> Se você tiver uma sugestão para nós, informe-nos! Agradecemos a oportunidade de se envolver com você em decisões de design por meio do portal [**da comunidade de desenvolvedores**](https://aka.ms/vsgitsuggestions) .

- Introdução [ao git e ao GitHub no tutorial do Visual Studio](/learn/modules/visual-studio-github-push/) sobre Microsoft Learn
- Vídeo [Introdução ao Git no Visual Studio](https://www.youtube.com/watch?v=GCZ9x3yqkyc) no YouTube
- Publicação [aprimorada de produtividade com git na postagem de blog do Visual Studio](https://devblogs.microsoft.com/visualstudio/enhanced-productivity-with-git-in-visual-studio/)
- [caixa de diálogo Opções](../ide/reference/options-dialog-box-visual-studio.md)
