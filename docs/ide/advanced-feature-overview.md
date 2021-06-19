---
title: Recursos avançados
description: Saiba mais sobre os recursos avançados que podem ser mais apropriados para desenvolvedores experientes ou para os desenvolvedores que já estão familiarizados com Visual Studio.
ms.custom: vs-acquisition
ms.date: 06/01/2018
ms.topic: conceptual
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6cc6604816921b054b0c909177c8e641493920a8
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386190"
---
# <a name="features-of-visual-studio"></a>Funcionalidades do Visual Studio

O artigo [Visão geral do IDE do Visual Studio](../get-started/visual-studio-ide.md) fornece uma introdução básica ao Visual Studio. Este artigo descreve os recursos que podem ser mais apropriados para desenvolvedores experientes ou aqueles que já estão familiarizados com o Visual Studio.

## <a name="modular-installation"></a>Instalação modular

O instalador modular do Visual Studio permite que você escolha e instale *cargas de trabalho*. As cargas de trabalho são grupos de recursos necessários para a linguagem de programação ou a plataforma de sua preferência. Essa estratégia ajuda a manter a superfície de instalação do Visual Studio menor, o que significa que ele é instalado e atualizado mais rapidamente também.

::: moniker range="vs-2017"

Se você ainda não tiver instalado o Visual Studio, acesse a página [Visual Studio downloads](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) para instalá-lo gratuitamente.

::: moniker-end

::: moniker range=">=vs-2019"

Se você ainda não tiver instalado o Visual Studio, acesse a página [Visual Studio downloads](https://visualstudio.microsoft.com/downloads) para instalá-lo gratuitamente.

::: moniker-end

Para saber mais sobre como configurar o Visual Studio no sistema, confira [Instalar o Visual Studio](../install/install-visual-studio.md).

## <a name="create-cloud-enabled-apps-for-azure"></a>Criar aplicativos habilitados para a nuvem para o Azure

O Visual Studio oferece um pacote de ferramentas que permite criar aplicativos habilitados para a nuvem com facilidade da plataforma Microsoft Azure. É possível configurar, compilar, depurar, empacotar e implantar aplicativos e serviços no Microsoft Azure diretamente por meio do IDE. Para obter as ferramentas e modelos de projeto do Azure, selecione a carga de trabalho **Desenvolvimento do Azure** ao instalar o Visual Studio.

![Carga de trabalho de desenvolvimento do Azure](../data-tools/media/azure-development-workload.png)

::: moniker range="vs-2017"

Após instalar a carga de trabalho **desenvolvimento do Azure**, os seguintes modelos de **nuvem** para C# estarão disponíveis na caixa de diálogo **Novo Projeto**:

![Modelos de projeto de nuvem para Visual Studio](media/cloud-project-templates.png)

::: moniker-end

O [Cloud Explorer](/azure/vs-azure-tools-resources-managing-with-cloud-explorer) do Visual Studio permite exibir e gerenciar seus recursos de nuvem baseados no Azure dentro do Visual Studio. Esses recursos podem incluir máquinas virtuais, tabelas, bancos de dados SQL e mais. O **Cloud Explorer** mostra os recursos do Azure em todas as contas gerenciadas na assinatura do Azure à qual você está conectado. E se uma operação específica exigir o portal do Azure, o **Cloud Explorer** fornecerá links que direcionem você no portal para onde for necessário.

![Cloud Explorer no Visual Studio](media/cloud-explorer.png)

É possível utilizar os serviços do Azure para seus aplicativos usando os **Serviços Conectados** como:

- [Serviço conectado do Active Directory](/azure/active-directory/develop/vs-active-directory-add-connected-service) para os usuários poderem usar suas contas no [Azure Active Directory](/azure/active-directory/active-directory-whatis) para se conectar aos aplicativos Web
- [Serviço conectado do Armazenamento do Azure](/azure/vs-azure-tools-connected-services-storage) para armazenamento de blobs, filas e tabelas
- [Serviço conectado do Key Vault](/azure/key-vault/vs-key-vault-add-connected-service) para gerenciar segredos para aplicativos Web

Os **Serviços Conectados** disponíveis dependem de seu tipo de projeto. Adicione um serviço clicando com o botão direito do mouse no projeto no **Gerenciador de Soluções** e escolhendo **Adicionar** > **Serviço Conectado**.

![Serviços conectados do Visual Studio](media/connected-services.png)

Para obter mais informações, confira [Move to the cloud With Visual Studio and Azure](https://visualstudio.microsoft.com/vs/azure-tools/) (Mover para a nuvem com o Visual Studio e o Azure).

## <a name="create-apps-for-the-web"></a>Criar aplicativos para a Web

A Internet impulsiona nosso mundo moderno e o Visual Studio pode ajudá-lo a escrever aplicativos para ele. É possível criar aplicativos Web usando ASP.NET, Node.js, Python, JavaScript e TypeScript. O Visual Studio reconhece estruturas Web como Angular, jQuery, Express e muito mais. O ASP.NET Core e o .NET Core são executados nos sistemas operacionais Windows, Mac e Linux. O [ASP.NET Core](https://dotnet.microsoft.com/learn/aspnet/what-is-aspnet-core) é uma atualização importante para MVC, WebAPI e SignalR e é executado no Windows, no Mac e no Linux.  O ASP.NET Core foi projetado desde o princípio para fornecer a você uma pilha .NET enxuta e combinável para compilar serviços e aplicativos Web modernos baseados em nuvem.

Para obter mais informações, consulte [Ferramentas da Web modernas](https://visualstudio.microsoft.com/vs/modern-web-tooling/).

## <a name="build-cross-platform-apps-and-games"></a>Criar jogos e aplicativos de plataforma cruzada

É possível usar o Visual Studio para compilar aplicativos e jogos para macOS, Linux e Windows, bem como para Android, iOS e outros [dispositivos móveis](https://visualstudio.microsoft.com/vs/mobile-app-development/).

- Crie aplicativos [.NET Core](/dotnet/core/) executados em Windows, macOS e Linux.

- Crie aplicativos móveis para iOS, Android e Windows em C# e F# usando o [Xamarin](https://developer.xamarin.com/guides/cross-platform/windows/visual-studio/).

- Crie jogos 2D e 3D em C# usando [Ferramentas do Visual Studio para Unity](/gamedev/unity/get-started/visual-studio-tools-for-unity.md).

- Compile aplicativos C++ nativos para dispositivos iOS, Android e Windows. Compartilhe código comum em bibliotecas criadas para iOS, Android e Windows usando [C++ para desenvolvimento multiplataforma](/cpp/cross-platform/visual-cpp-for-cross-platform-mobile-development).

## <a name="connect-to-databases"></a>Conectar-se aos bancos de dados

**Gerenciador de Servidores** ajuda você a procurar e gerenciar instâncias SQL Server e ativos localmente, remotamente e no Azure, Salesforce.com, Microsoft 365 e sites. Para abrir **Gerenciador de Servidores**, no menu principal, escolha **Exibir**  >  **Gerenciador de Servidores**. Para obter mais informações de como usar o Gerenciador de Servidores, confira [Adicionar novas conexões](../data-tools/add-new-connections.md).

O [SSDT (SQL Server Data Tools)](/sql/ssdt/download-sql-server-data-tools-ssdt) é um ambiente de desenvolvimento avançado do SQL Server, do Banco de Dados SQL do Azure e do SQL Data Warehouse do Azure. Ele permite compilar, depurar, manter e refatorar bancos de dados. Você pode trabalhar com um projeto de banco de dados ou diretamente com uma instância local ou não de banco de dados conectado.

O **Pesquisador de Objetos do SQL Server** no Visual Studio fornece uma exibição dos objetos de banco de dados semelhante ao SQL Server Management Studio. O Pesquisador de Objetos do SQL Server permite que você faça o trabalho leve de administração e design de banco de dados. Exemplos de trabalho incluem editar dados da tabela, comparar esquemas, executar consultas usando menus contextuais diretamente do Pesquisador de Objetos do SQL Server e muito mais.

![Pesquisador de Objetos do SQL Server](../ide/media/vs2015_sqlobjectexplorer.png)

## <a name="debug-test-and-improve-your-code"></a>Depurar, testar e melhorar o código

Quando você escrever o código, é necessário executá-lo e testá-lo para verificar o desempenho e se há bugs. O sistema de depuração de última geração do Visual Studio permite depurar o código em execução no projeto local, em um dispositivo remoto ou em um [emulador de dispositivo](../cross-platform/visual-studio-emulator-for-android.md). Você pode percorrer pelo código uma instrução por vez e inspecionar as variáveis conforme avança. Você pode definir pontos de interrupção que são atingidos somente quando uma determinada condição é verdadeira. As opções de depuração podem ser gerenciadas no próprio editor de códigos, para que você não precise sair do código. Para obter mais detalhes sobre a depuração no Visual Studio, confira [Primeiro acesso ao depurador](../debugger/debugger-feature-tour.md).

Para saber mais sobre como melhorar o desempenho de seus aplicativos, confira a funcionalidade de [criação de perfil](../profiling/profiling-feature-tour.md) do Visual Studio.

Para [testes](../test/improve-code-quality.md), o Visual Studio oferece teste de unidade, Live Unit Testing, IntelliTest, teste de desempenho e de carga e muito mais. O Visual Studio também aprimorou as funcionalidades de [análise de código](../code-quality/code-analysis-for-managed-code-overview.md) para capturar o design, segurança e outros tipos de falhas.

## <a name="deploy-your-finished-application"></a>Implantar o aplicativo concluído

Quando o aplicativo estiver pronto para ser implantado em usuários ou clientes, o Visual Studio fornecerá as ferramentas para fazer isso. As opções de implantação incluem na Microsoft Store, em um site do SharePoint ou com as tecnologias InstallShield ou Windows Installer. Ele é todo acessível por meio do IDE. Para obter mais informações, consulte [Implantar aplicativos, serviços e componentes](../deployment/deploying-applications-services-and-components.md).

## <a name="manage-your-source-code-and-collaborate-with-others"></a>Gerenciar seu código-fonte e colaborar com outros

É possível gerenciar o código-fonte em repositórios Git hospedados por qualquer provedor, incluindo o GitHub. Ou use o [Azure DevOps Services](/azure/devops/index) para gerenciar o código, bem como bugs e itens de trabalho de todo o projeto. Consulte [Introdução ao GIT e ao Azure Repos](/azure/devops/repos/git/gitquickstart?tabs=visual-studio) para obter mais informações sobre o gerenciamento de repositórios GIT no Visual Studio usando o Team Explorer. O Visual Studio também tem outros recursos de controle do código-fonte internos. Para saber mais sobre eles, confira [Novas funcionalidades do Git no Visual Studio (blog)](https://devblogs.microsoft.com/devops/new-git-features-in-visual-studio-2017/).

Os Azure DevOps Services são serviços baseados em nuvem para planejar, hospedar, automatizar e implantar o software e habilitar a colaboração nas equipes. Os Azure DevOps Services dão suporte a repositórios Git (controle de versão distribuído) e ao Controle de Versão do Team Foundation (controle de versão centralizado). Eles dão suporte a pipelines de build e versão contínuos (CI/CD) de código armazenado em sistemas de controle de versão. O Azure DevOps Services também dá suporte a metodologias de desenvolvimento Agile, CMMI e Scrum.

O TFS (Team Foundation Server) é o hub de gerenciamento do ciclo de vida do aplicativo para o Visual Studio. Ele habilita a participação de todos os envolvidos com o processo de desenvolvimento usando uma única solução. O TFS também é útil para gerenciar equipes e projetos heterogêneos.

Se você tiver uma organização do Azure DevOps ou um Team Foundation Server na rede, conecte-se a ela por meio da janela **Team Explorer** no Visual Studio. Nessa janela você pode fazer check-in ou check-out de código no controle do código-fonte, gerenciar itens de trabalho, iniciar compilações e acessar salas da equipe e workspaces. Abra o **Team Explorer** na caixa de pesquisa ou no menu principal, em **Exibir** > **Team Explorer** ou em **Equipe** > **Gerenciar Conexões**.

A imagem a seguir mostra a janela **Team Explorer** em uma solução hospedada no Azure DevOps Services.

![Team Explorer para Visual Studio](../ide/media/vs2017_teamexplorer_devops.png)

Também é possível automatizar o processo de build para compilar o código que os desenvolvedores de sua equipe fizeram check-in no controle de versão. Por exemplo, será possível criar um ou mais projetos à noite ou sempre que o check-in do código for feito. Para obter mais informações, confira [Azure Pipelines](/azure/devops/pipelines/index?view=vsts&preserve-view=true).

## <a name="extend-visual-studio"></a>Estender o Visual Studio

Se o Visual Studio não tiver a funcionalidade exata de que você precisa, será possível adicioná-la! É possível personalizar o IDE de acordo com o estilo e fluxo de trabalho, adicionar suporte para ferramentas externas que ainda não estão integradas ao Visual Studio e modificar a funcionalidade existente para aumentar a produtividade. Para encontrar a versão mais recente das Ferramentas de Extensibilidade do Visual Studio (SDK do VS), confira [Visual Studio SDK](../extensibility/visual-studio-sdk.md) (SDK do Visual Studio).

Você pode usar o .NET Compiler Platform ("Roslyn") para escrever seus próprios analisadores de código e geradores de código. Encontre tudo o que você precisa em [Roslyn](https://github.com/dotnet/Roslyn).

Encontre [extensões existentes](https://marketplace.visualstudio.com/vs) para o Visual Studio criadas pelos desenvolvedores da Microsoft, bem como pela nossa comunidade de desenvolvimento.

Para saber mais sobre como estender o Visual Studio, consulte [Estender o IDE do Visual Studio](https://visualstudio.microsoft.com/vs/extend/).

## <a name="see-also"></a>Confira também

- [Visão geral do IDE do Visual Studio](../get-started/visual-studio-ide.md)
- [Novidades no Visual Studio 2017](../ide/whats-new-visual-studio-2017.md)
- [Novidades no Visual Studio 2019](../ide/whats-new-visual-studio-2019.md)
