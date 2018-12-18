---
title: Novidades no Visual Studio 2017
description: Saiba mais sobre os novos recursos do Visual Studio 2017.
ms.custom: ''
ms.date: 12/04/2018
ms.prod: visual-studio-dev15
ms.technology: vs-acquisition
ms.topic: conceptual
f1_keywords:
- VS.StartPage.WhatsNew
helpviewer_keywords:
- Visual Studio, what's new
- what's new [Visual Studio]
ms.assetid: 7307e180-ba28-4774-8a43-cbb980085a71
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: a007d6557fe7ebd533ee34fecc8b8c0315024edf
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895763"
---
# <a name="what39s-new-in-visual-studio-2017"></a>Novidades no Visual Studio 2017

**Atualizado para a [versão 15.9](/visualstudio/releasenotes/vs2017-relnotes?context=visualstudio/default&contextView=vs-2017)**

Deseja atualizar de uma versão anterior do Visual Studio? Veja o que o Visual Studio 2017 pode oferecer a você: produtividade inigualável para qualquer desenvolvimento, aplicativo e plataforma. Use o Visual Studio 2017 para desenvolver aplicativos para Android, iOS, Windows, Linux, Web e nuvem. Codifique rapidamente, depure e diagnostique com facilidade, teste com frequência e faça lançamentos com confiança. Também é possível estender e personalizar o Visual Studio criando suas próprias extensões. Use o controle de versão, seja ágil e colabore de maneira eficiente com esse lançamento!

Veja uma recapitulação de alto nível das alterações feitas em relação à versão anterior, o Visual Studio 2015:

* **[Princípios básicos redefinidos](#redefined-fundamentals)**. Uma nova experiência de instalação significa que é possível instalar mais rapidamente e instalar o que você deseja quando necessário.
* **[Desempenho e produtividade](#performance-and-productivity)**. Nosso foco ficou em novos e modernos recursos de desenvolvimento para desktop, dispositivos móveis e nuvem. Além disso, o Visual Studio é iniciado mais rapidamente, é mais dinâmico e usa menos memória do que antes.
* **[Desenvolvimento de aplicativo na nuvem com o Azure](#cloud-app-development-with-azure)**. Um pacote interno de ferramentas do Azure que permite criar com facilidade aplicativos diretamente em nuvem da plataforma Microsoft Azure. O Visual Studio facilita a configuração, o build, a depuração, o empacotamento e a implantação de aplicativos e serviços no Azure.
* **[Desenvolvimento de aplicativos do Windows](#windows-app-development)**. Use os modelos da UWP no Visual Studio 2017 para criar um projeto único para todos os dispositivos do Windows 10 &ndash; PC, tablet, smartphone, Xbox, HoloLens, Surface Hub e muito mais.
* **[Desenvolvimento de aplicativos móveis](#mobile-app-development)**. Inove e obtenha resultados rápidos com o Xamarin, que unifica seus requisitos móveis multiplataforma em uma base de código principal e um conjunto de habilidades.
* **[Desenvolvimento de multiplataforma](#cross-platform-development)**. Distribua software perfeitamente para qualquer plataforma de destino. Estenda os processos do DevOps para o SQL Server por meio do Redgate Data Tools e automatize com segurança as implantações do banco de dados por meio do Visual Studio. Ou então, use o .NET Core para escrever aplicativos e bibliotecas que são executados sem modificações nos sistemas operacionais Windows, Linux e macOS.
* **[Desenvolvimento de jogos](#games-development)**. Com o VSTU (Ferramentas do Visual Studio para Unity), é possível usar o Visual Studio para escrever scripts de jogo e editor em C# e, em seguida, usar seu depurador avançado para encontrar e corrigir erros.
* **[Desenvolvimento de IA](#ai-development)**. Com as Visual Studio Tools for AI, é possível usar as funcionalidades de produtividade do Visual Studio para acelerar a inovação em IA. Crie, teste e implante soluções de Aprendizado Profundo/IA que são integradas com o Azure Machine Learning para obter funcionalidades robustas de experimentação.

> [!NOTE]
> Para obter uma lista completa dos novos recursos e funcionalidades no Visual Studio 2017, consulte as [Notas de versão atuais](/visualstudio/releasenotes/vs2017-relnotes?context=visualstudio/default&contextView=vs-2017). E para ver ofertas futuras de recursos, consulte as [Notas da versão prévia](/visualstudio/releasenotes/vs2017-preview-relnotes?context=visualstudio/default&contextView=vs-2017).

Veja aqui informações mais detalhadas de algumas das melhorias mais importantes e das novas funcionalidades no Visual Studio 2017.

## <a name="redefined-fundamentals"></a>Princípios básicos redefinidos

### <a name="a-new-setup-experience"></a>Uma nova experiência de instalação

[Baixar o Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) ou [Verificar os requisitos do sistema do Visual Studio](/visualstudio/productinfo/vs2017-system-requirements-vs?context=visualstudio/default&contextView=vs-2017)

 O Visual Studio facilita e agiliza a instalação de recursos específicos de que você precisa, quando necessário. Além disso, ele também se desinstala completamente.

 A alteração mais importante que você verá ao instalar o Visual Studio é a sua nova experiência de instalação. Na guia **Cargas de Trabalho**, você verá opções de instalação que estão agrupadas para representar estruturas comuns, linguagens e plataformas. Ela abrange tudo, desde o desenvolvimento de área de trabalho do .NET até o desenvolvimento de aplicativos do C++ no Windows, Linux e iOS.

Escolha as cargas de trabalho de que você precisa e altere-as quando necessário.

 ![Caixa de diálogo de instalação do Visual Studio 2017](../install/media/install-visual-studio-enterprise.png)

E você também tem opções para ajustar sua instalação:

* Deseja escolher seus próprios componentes em vez de usar cargas de trabalho? Selecione a guia **Componentes individuais** no instalador.
* Deseja instalar Pacotes de Idiomas sem precisar alterar também a opção de idioma do Windows? Escolha a guia **Pacotes de idiomas** do instalador.
* **Novidade no 15.7**: quer alterar o local onde o Visual Studio faz instalações? Escolha a guia **Opções de instalação** do instalador.

Para saber mais sobre a nova experiência de instalação, incluindo instruções passo a passo que explicam a instalação, consulte a página [Instalando o Visual Studio](../install/install-visual-studio.md).

### <a name="a-focus-on-accessibility"></a>Um foco na acessibilidade

Como **novidade na versão 15.3**, fizemos mais de 1.700 correções direcionadas para melhorar a compatibilidade entre o Visual Studio e as tecnologias adaptativas que muitos dos nossos clientes usam. Hoje, há vários cenários que são mais compatíveis com leitores de tela, temas de alto contraste e outras tecnologias adaptativas. O depurador, o editor e o shell também tiveram melhorias significativas.

Para saber mais, confira a postagem no blog [Accessibility improvements in Visual Studio 2017 version 15.3](https://blogs.msdn.microsoft.com/visualstudio/2017/08/14/accessibility-improvements-in-visual-studio-2017-version-15-3/) (Aprimoramentos de acessibilidade no Visual Studio 2017 versão 15.3).

## <a name="performance-and-productivity"></a>Desempenho e produtividade

### <a name="sign-in-across-multiple-accounts"></a>Entrar através de várias contas

Introduzimos um novo serviço de identidade no Visual Studio que permite compartilhar contas de usuário entre o Team Explorer, as Ferramentas do Azure, a publicação da Microsoft Store e muito mais.

É possível permanecer conectado por mais tempo também. O Visual Studio não solicitará um novo logon a cada 12 horas. Para obter mais informações, consulte a postagem de blog [Menos solicitações de Entrada no Visual Studio](https://blogs.msdn.microsoft.com/visualstudio/2016/08/15/fewer-visual-studio-sign-in-prompts/).

### <a name="start-visual-studio-faster"></a>Iniciar o Visual Studio mais rápido

O novo Centro de Desempenho do Visual Studio pode ajudá-lo a otimizar o tempo de inicialização do IDE. O Centro de Desempenho lista todas as extensões e janelas de ferramentas que podem causar lentidão na inicialização do IDE. Você pode usá-lo para melhorar o desempenho de inicialização, determinando quando iniciar as extensões ou se as janelas de ferramentas serão abertas na inicialização.

### <a name="faster-on-demand-loading-of-extensions"></a>Carregamento sob demanda de extensões mais rápido

O Visual Studio está movendo suas extensões (e trabalhando com extensões de terceiros também) para que elas sejam carregadas sob demanda, em vez de na inicialização do IDE. Curioso para saber quais extensões afetam a inicialização, carga de solução e desempenho de digitação? Você pode ver essas informações em **Ajuda** > **Gerenciar desempenho do Visual Studio**.

  ![Caixa de diálogo Opções no Visual Studio 2017](../ide/media/vs2017ide-manage-vs-perf.png)

#### <a name="manage-your-extensions-with-roaming-extensions-manager"></a>Gerenciar suas extensões com o Roaming Extension Manager

Agora ficou ainda mais fácil configurar cada ambiente de desenvolvimento com suas extensões favoritas ao entrar no Visual Studio. O novo Roaming Extension Manager acompanha todas as suas extensões favoritas criando uma lista sincronizada na nuvem.

Para ver uma lista de suas extensões no Visual Studio, clique em **Ferramentas** > **Extensões e Atualizações** e, em seguida, clique em **Gerenciador de Extensão de Roaming**.

![Visual Studio 2017 – Caixa de diálogo Extensões e Atualizações](../ide/media/vs2017ide-extensions-and-updates.png)

O Roaming Extension Manager rastreia todas as extensões instaladas, mas você pode escolher quais você deseja adicionar à lista de Roaming.

![Visual Studio 2017 – Caixa de diálogo Extensões e Atualizações](../ide/media/vs2017ide-RoamingExtensionManager.png)

Quando você usa o Roaming Extension Manager, há três tipos de ícones em sua lista:

* ![Ícone de Roaming](../ide/media/vs2017ide-roamedicon.png) **_Roaming_**: uma extensão que faz parte dessa Lista de Roaming, mas que não está instalada no computador.
  (Você pode instalá-las usando o botão **Download**).
* ![Ícone de Roaming e Instalado](../ide/media/vs2017ide-roamedinstalledicon.png) **_Roaming e Instalado_**: todas as extensões que fazem parte dessa Lista de Roaming e que estão instaladas no ambiente de desenvolvimento.
  (Se você decidir que não deseja usar perfil móvel, poderá remover essas extensões usando o botão **Parar Roaming**).
* ![Ícone de Instalado](../ide/media/vs2017ide-installedicon.png) **_Instalado_**: todas as extensões instaladas nesse ambiente, mas que não fazem parte da Lista de Roaming.
  (Você pode adicionar extensões à Lista de Roaming usando o botão **Iniciar Roaming**).

Qualquer extensão baixada enquanto você estiver conectado será adicionada à lista como **Roaming e Instalado**. Além disso, a extensão fará parte da lista Roaming, que fornece acesso a ela em qualquer computador.

### <a name="experience-live-unit-testing"></a>Experimentar o Live Unit Testing

No Visual Studio Enterprise 2017, o Live Unit Testing fornece resultados de teste de unidade dinâmicos e a cobertura de código no editor durante a codificação. Funciona com projetos do C# e Visual Basic para ambos o .NET Framework e o .NET Core e dá suporte a três estruturas de teste do MSTest, xUnit e NUnit.

![Live Unit Testing](../ide/media/lut-codewindow.png)

Para obter mais informações, veja [Introducing Live Unit Testing](../test/live-unit-testing-intro.md) (Introdução ao Live Unit Testing). Para obter uma lista das novas funcionalidades adicionadas em cada versão do Visual Studio Enterprise 2017, veja [What's new in Live Unit Testing](../test/live-unit-testing-whats-new.md) (Novidades no Live Unit Testing).

### <a name="set-up-a-cicd-pipeline"></a>Configurar um pipeline de CI/CD

#### <a name="automated-testing"></a>Teste automatizado

Testes automatizados são uma parte importante de qualquer pipeline de DevOps. Ele permite que você teste e libere sua solução de modo consistente e confiável em ciclos muito mais curtos. Fluxos de CI/CD (integração contínua e entrega contínua) podem ajudar a tornar o processo mais eficiente.

Para saber mais sobre testes automatizados, confira a postagem no blog [CI/CD pipeline for automated tests in DevOps](https://blogs.msdn.microsoft.com/visualstudioalmrangers/2017/04/20/set-up-a-cicd-pipeline-to-run-automated-tests-efficiently/) (Pipeline de CI/CD para testes automatizados no DevOps).

E, para obter mais informações sobre as novidades na extensão de DevLabs [Ferramentas de Entrega Contínua para Visual Studio](https://marketplace.visualstudio.com/items?itemName=VSIDEDevOpsMSFT.ContinuousDeliveryToolsforVisualStudio), confira a postagem no blog [Committing with Confidence: Commit Time Code Quality](https://blogs.msdn.microsoft.com/visualstudio/2017/08/21/committing-with-confidence-commit-time-code-quality-information-updated/) (Confirmação com segurança: qualidade do código da hora de confirmação).

### <a name="visual-studio-ide-enhancements"></a>Aprimoramentos no IDE do Visual Studio

#### <a name="multi-caret-editing"></a>Edição com vários cursores

**Novo na 15.8**: a edição simultânea de vários locais em um arquivo agora é fácil. Comece criando pontos de inserção e seleções em vários locais em um arquivo. Em seguida, use o recurso de edição com vários cursores para fazer a mesma edição em dois ou mais lugares ao mesmo tempo.

Para obter mais informações, confira a seção [Seleção com vários cursores](finding-and-replacing-text.md#multi-caret-selection) da página [Localizar e substituir texto](finding-and-replacing-text.md).

#### <a name="keep-keybinding-profiles-consistent"></a>Manter os perfis de associação de teclas consistentes

**Novo na 15.8**: agora, você pode manter suas associações de teclas consistentes entre as ferramentas com dois novos perfis de teclado: Visual Studio Code e ReSharper (Visual Studio). Você pode encontrar esses esquemas em **Ferramentas** > **Opções** > **Geral** > **Teclado** e no menu suspenso superior.

  ![Novos perfis de associação de teclas para Visual Studio Code e o ReSharper](../ide/media/vs-keyboard-mappings-code-resharper.png)

#### <a name="use-new-refactorings"></a>Usar novas refatorações

A refatoração é o processo de aperfeiçoar seu código após ele ter sido gravado. Ela altera a estrutura interna do código, sem modificar seu comportamento. Adicionamos novas refatorações constantemente. Eis apenas algumas delas:

* Adicionar parâmetro (de CallSite)
* Gerar substituições
* Adicionar argumento nomeado
* Adicionar verificação de null para parâmetros
* Inserir separadores de dígitos em literais
* Alterar a base para literais numéricos (por exemplo, de hexadecimal para binário)
* Converter if para switch
* Remover variáveis não utilizadas

Para obter mais informações, consulte [Ações Rápidas](../ide/common-quick-actions.md).

#### <a name="interact-with-git"></a>Interagir com o Git

Quando você está trabalhando com um projeto no Visual Studio, pode configurar, confirmar rapidamente e publicar o código em um serviço Git. Também é possível gerenciar os repositórios Git usando o menu e cliques de botões no canto direito inferior do IDE.

![O Visual Studio 2017 interage com a caixa de diálogo do GIT](../ide/media/vsIDE-GitInteraction.png)

#### <a name="experience-improved-navigation-controls"></a>Controles de navegação com experiência aprimorada

Atualizamos a experiência de navegação para ajudá-lo a chegar de um lugar a outro com mais confiança e menos distrações.

* **Novidade na versão 15.4**: **Ir para definição** (**Ctrl**+**clique** ou **F12**) &ndash; Os usuários de mouse têm uma maneira mais fácil de navegar até a definição de um membro pressionando **Ctrl** e clicando no membro. Ao pressionar **Ctrl** e focalizar um símbolo de código, ele será sublinhado e virará um link. Para obter mais informações, veja [Go To Definition and Peek Definition](../ide/go-to-and-peek-definition.md) (Ir para Definição e Inspecionar Definição).

* **Ir para Implementação** (**Ctrl**+**F12**) &ndash; Navegue de qualquer membro ou tipo base até suas várias implementações.

* **Ir para Todos** (**Ctrl**+**T** ou **Ctrl**+**,**) &ndash; Navegue diretamente para qualquer declaração de arquivo/tipo/membro/símbolo. É possível filtrar a lista de resultados ou usar a sintaxe de consulta (por exemplo, “f searchTerm” para arquivos, “t searchTerm” para tipos, etc.).

  ![Ir para Todos aprimorado](../ide/media/vs2017ide-navigation-go-to.png)

* **Localizar Todas as Referências** (**Shift**+**F12**) &ndash; Com a colorização de sintaxe, é possível agrupar os resultados de Localizar Todas as Referências com uma combinação de projeto, definição e caminho. Também é possível “bloquear” os resultados para que você possa continuar encontrando outras referências sem perder os resultados originais.

  ![Nova ferramenta Localizar Todas as Referências](../ide/media/vs2017ide-find-all-references.png)

* **Visualizador de Estrutura** &ndash; As linhas verticais cinzas pontilhadas (guias de recuo) atuam como pontos de referência no código para fornecer o contexto no quadro de exibição. É possível reconhecê-los nas populares Productivity Power Tools. É possível usá-las para visualizar e descobrir em qual bloco de código você está a qualquer momento, sem a necessidade de rolagem. Focalizar as linhas exibe uma dica de ferramenta que mostra a abertura desse bloco e seus pais. Esse recurso está disponível para todas as linguagens compatíveis por meio de gramáticas TextMate, bem como C#, Visual Basic e XAML.

  ![Visualizador de estrutura do Visual Studio 2017](../ide/media/vsIDE-StructureVisualizer.png)

Para obter mais informações sobre os novos recursos de produtividade, consulte a postagem no blog [Produtividade no Visual Studio 2017](https://blogs.msdn.microsoft.com/visualstudio/2016/11/28/productivity-in-visual-studio-2017-rc/) de Mark Wilson-Thomas.

### <a name="visual-c"></a>Visual C++

Você verá diversas melhorias no Visual Studio, como a distribuição de Diretrizes do C++ Core com o Visual Studio, atualização do compilador com a adição de suporte avançado para recursos do C++ 11 e C++, além da adição e atualização de funcionalidades nas bibliotecas C++. Também melhoramos o desempenho do IDE do C++, as cargas de trabalho de instalação e muito mais.

Além disso, corrigimos mais de 250 bugs e problemas relatados no compilador e nas ferramentas, muitos deles enviados pelos clientes por meio do [Comunidade de Desenvolvedores para C++](https://developercommunity.visualstudio.com/spaces/62/index.html "Comunidade de Desenvolvedores para C++").

Para obter detalhes completos, consulte a página [Novidades do Visual C++ no Visual 2017](/cpp/top/what-s-new-for-visual-cpp-in-visual-studio).

### <a name="debugging-and-diagnostics"></a>Depuração e diagnóstico

#### <a name="run-to-click"></a>Executar com um Clique

Agora, é possível avançar com mais facilidade durante a depuração, sem configurar um ponto de interrupção para parar na linha desejada. Quando você está parado no depurador, basta clicar no ícone exibido ao lado da linha de código. O código será executado e parará nessa linha na próxima vez que for acessado no caminho do código.

![Depuração do Visual Studio 2017 – Executar com um Clique](../ide/media/vs2017ide-RunToClick.png)

#### <a name="the-new-exception-helper"></a>O novo Auxiliar de Exceção

O novo Auxiliar de Exceção ajuda você a exibir as informações de exceção rapidamente. As informações são apresentadas em um formato compacto, com acesso instantâneo às exceções internas. Ao diagnosticar uma NullReferenceException, é possível ver rapidamente o que era nulo diretamente dentro do Auxiliar de Exceção.

![A nova caixa de diálogo Auxiliar de Exceção no Visual Studio](../ide/media/vs2017ide-ExceptionHelper.png)

Para obter mais informações, consulte a postagem de blog [Use the new Exception Helper in Visual Studio](https://blogs.msdn.microsoft.com/devops/2016/03/31/using-the-new-exception-helper-in-visual-studio-15-preview/) (Usar o novo Auxiliar de Exceção no Visual Studio).

#### <a name="snapshots-and-intellitrace-step-back"></a>Instantâneos e retrocesso do IntelliTrace

**Novidade na versão 15.5**: o retrocesso do IntelliTrace tira automaticamente um instantâneo do seu aplicativo em cada evento de etapa do depurador e do ponto de interrupção. Os instantâneos registrados permitem retornar aos pontos de interrupção ou às etapas anteriores e exibir o estado do aplicativo como ele era no passado. O retrocesso do IntelliTrace poderá poupar seu tempo quando você desejar ver o estado do aplicativo anterior, mas não desejar reiniciar a depuração nem recriar o estado do aplicativo desejado.

É possível navegar e exibir instantâneos usando os botões **Voltar** e **Avançar** na barra de ferramentas **Depurar**. Esses botões navegam pelos eventos exibidos na guia **Eventos** na janela **Ferramentas de Diagnóstico**. Voltar ou avançar para um evento ativa automaticamente a depuração histórica no evento selecionado.

![A caixa de diálogo Novo Auxiliar de Exceção no Visual Studio](../debugger/media/intellitrace-step-back-icons-description.png  "Botões Voltar e Avançar")

Para obter mais informações, consulte a página [View snapshots using IntelliTrace step-back](../debugger/how-to-use-intellitrace-step-back.md) (Exibir instantâneos usando o retrocesso do IntelliTrace).

### <a name="containerization"></a>Transporte em contêineres

Os contêineres fornecem uma densidade de aplicativo aumentada e um custo de implantação menor, juntamente com melhorias na produtividade e na agilidade de DevOps.

#### <a name="docker-container-tooling"></a>Ferramentas de Contêiner do Docker

**Novidade na versão 15.5**:

* O Visual Studio inclui ferramentas para contêineres do Docker que agora são compatíveis com Dockerfiles de vários estágios, que simplificam a criação de imagens de contêiner otimizadas.
* Por padrão, Visual Studio efetuará pull, compilará e executará automaticamente as imagens de contêiner necessárias em segundo plano quando você abrir um projeto que tenha suporte do Docker. Você pode desabilitar isso por meio da configuração **Iniciar automaticamente os contêineres em segundo plano** no Visual Studio.

## <a name="cloud-app-development-with-azure"></a>Desenvolvimento de aplicativo na nuvem com o Azure

### <a name="azure-functions-tools"></a>Ferramentas do Azure Functions

Como parte da carga de trabalho de "desenvolvimento do Azure", há ferramentas para ajudá-lo a desenvolver funções do Azure usando as bibliotecas de classes do C# pré-compiladas. Agora você pode criar, executar, depurar em seu computador de desenvolvimento local e, em seguida, publicar diretamente no Azure por meio do Visual Studio.

Para obter mais informações, consulte a página [Ferramentas do Azure Functions para Visual Studio](https://docs.microsoft.com/azure/azure-functions/functions-develop-vs).

### <a name="debug-live-aspnet-apps-using-snappoints-and-logpoints-in-live-azure-applications"></a>Depurar aplicativos ASP.NET dinâmicos usando snappoints e logpoints nos aplicativos dinâmicos do Azure

**Novidades na versão 15.5**: o Depurador de Instantâneo tira um instantâneo de seus aplicativos em produção quando o código no qual você está interessado é executado. Para instruir o depurador a tirar um instantâneo, defina snappoints e logpoints em seu código. O depurador permite ver exatamente o que deu errado sem afetar o tráfego do seu aplicativo de produção. O Depurador de Instantâneo pode ajudar a reduzir drasticamente o tempo que leva para resolver problemas que ocorrem em ambientes de produção.

A coleção de instantâneos está disponível para os seguintes aplicativos Web em execução no Serviço de Aplicativo do Azure:

* Aplicativos ASP.NET em execução no .NET Framework 4.6.1 ou posterior.
* Aplicativos ASP.NET Core em execução no .NET Core 2.0 ou posterior no Windows.

Para obter mais informações, consulte [Debug live ASP.NET apps using snappoints and logpoints](../debugger/debug-live-azure-applications.md) (Depurar aplicativos ASP.NET dinâmicos usando snappoints e logpoints).

## <a name="windows-app-development"></a>Desenvolvimento de aplicativos para Windows

### <a name="universal-windows-platform"></a>Plataforma Universal do Windows

A UWP (Plataforma Universal do Windows) é a plataforma de aplicativo do Windows 10. Você pode desenvolver aplicativos para a UWP com apenas um conjunto de APIs, um pacote do aplicativo e um repositório para alcançar todos os dispositivos do Windows 10 &ndash; PC, tablet, smartphone, Xbox, HoloLens, Surface Hub e muito mais. A UWP é compatível com diferentes tamanhos de telas e com uma variedade de modelos de interação, seja uma entrada por toque, um teclado, um controlador de jogos ou uma caneta. No núcleo dos aplicativos da UWP está a ideia de que os usuários desejam que suas experiências sejam móveis em TODOS os dispositivos, e de que eles querem usar o dispositivo mais conveniente ou produtivo para a tarefa em questão.

 ![Plataforma Universal do Windows](../cross-platform/media/uwp_coreextensions.png)

Escolha sua linguagem de desenvolvimento preferencial&mdash;entre C#, Visual Basic, C++ ou JavaScript&mdash;para criar um aplicativo da Plataforma Universal do Windows para dispositivos do Windows 10. O Visual Studio 2017 fornece um modelo de aplicativo da UWP para cada idioma, permitindo que você crie um projeto único para todos os dispositivos. Quando seu trabalho for concluído, você poderá produzir um pacote do aplicativo e enviá-lo à Microsoft Store pelo Visual Studio para divulgar seu aplicativo aos clientes em qualquer dispositivo do Windows 10.

**Novidade na versão 15.5**: o Visual Studio 2017 versão 15.5 fornece o melhor suporte para o SDK do Windows 10 Fall Creators Update (10.0.16299.0). O Windows 10 Fall Creators Update também oferece várias melhorias para os desenvolvedores da UWP. Aqui estão algumas das maiores alterações: 

* **Compatível com o .NET Standard 2.0**<br/>Além da implantação simplificada do aplicativo, o Windows 10 Fall Creators Update é a primeira versão do Windows 10 compatível com o .NET Standard 2.0. De fato, o [.NET Standard](https://blogs.msdn.microsoft.com/dotnet/2016/09/26/introducing-net-standard/) é uma implementação de referência da biblioteca de classes base que qualquer plataforma do .NET pode implementar. A meta do .NET Standard é facilitar o máximo possível para os desenvolvedores do .NET compartilhar o código em qualquer plataforma do .NET que eles escolham trabalhar.
* **O melhor da UWP e do Win32**<br/>Melhoramos a Plataforma do Windows 10 com a [Ponte de Desktop](https://docs.microsoft.com/windows/uwp/porting/desktop-to-uwp-root) para tornar o Windows 10 melhor para todos os desenvolvedores do .NET, quer o foco atual esteja na UWP, no WPF, no Windows Forms ou no Xamarin. Com o novo tipo de projeto do Pacote de Aplicativo no Visual Studio 2017 versão 15.5, você pode criar Pacotes de Aplicativos do Windows para seus projetos do WPF ou do Windows Forms, assim como você pode fazer com os projetos da UWP. Depois de empacotar seu aplicativo, você obterá todos os benefícios de implantação de aplicativo do Windows 10 e terá a opção de distribuir por meio da Microsoft Store (para aplicativos de consumidor) ou da Microsoft Store para Empresas e Educação. Como os aplicativos empacotados têm acesso à superfície da API da UWP completa e às APIs do Win32 na área de trabalho, agora você pode modernizar seus aplicativos do WPF e do Windows Forms gradualmente com as APIs da UWP e com os recursos do Windows 10. Além disso, você pode incluir os componentes do Win32 em seus aplicativos da UWP que são aprimorados na área de trabalho com todos os recursos do Win32.

Para obter mais informações sobre a UWP, consulte a página [Desenvolver aplicativos para a UWP (Plataforma Universal do Windows)](../cross-platform/develop-apps-for-the-universal-windows-platform-uwp.md).

## <a name="mobile-app-development"></a>Desenvolvimento de aplicativos móveis

### <a name="xamarin"></a>Xamarin

Como parte da carga de trabalho "Desenvolvimento móvel com o .NET", os desenvolvedores familiarizados com C#, .NET e Visual Studio podem fornecer aplicativos Android, iOS e Windows nativos usando o Xamarin. Os desenvolvedores podem aproveitar o mesmo o poder e a produtividade ao trabalhar com o Xamarin para aplicativos móveis, incluindo a depuração remota em dispositivos Android, iOS e Windows &mdash; sem precisar aprender idiomas de codificação nativa, como Objective-C ou Java.

Para obter mais informações, consulte a página [Visual Studio e Xamarin](../cross-platform/visual-studio-and-xamarin.md).

### <a name="entitlements-editor"></a>Editor de direitos

**Novidade no 15.3**: para suas necessidades de desenvolvimento do iOS, adicionamos um editor de direitos autônomo. Ele inclui uma interface do usuário amigável pela qual se pode navegar facilmente. Para iniciá-lo, clique duas vezes em seu arquivo *entitlements.plist*.

![Editor de qualificação para Xamarin](../ide/media/xamarin-entitlements-editor.png)

### <a name="visual-studio-tools-for-xamarin"></a>Ferramentas do Visual Studio para Xamarin

**Novidades na versão 15.4**: o Xamarin Live permite aos desenvolvedores implantar, testar e depurar continuamente seus aplicativos diretamente em dispositivos iOS e Android. Depois de baixar o Xamarin Live Player (disponível na App Store ou no Google Play), será possível emparelhar o dispositivo com o Visual Studio e revolucionar a forma como você cria aplicativos móveis. Essa funcionalidade agora está incluída no Visual Studio e pode ser habilitada indo até **Ferramentas** > **Opções** > **Xamarin**  >  **Outros** > **Habilitar Xamarin Live Player**.

![Animação do par, da implantação e dos modos de edição dinâmicos do Xamarin Live Player](../ide/media/xamarinliveplayer.gif)

### <a name="support-for-google-android-emulator"></a>Suporte para o Android Emulator da Google

**Novo na 15.8**: Ao usar o Hyper-V, agora você pode usar o Android Emulator da Google lado a lado com outras tecnologias que se baseiam no Hyper-V, como máquinas virtuais do Hyper-V, ferramentas do Docker, o emulador HoloLens e muito mais. (Esse recurso requer a Atualização de abril de 2018 para o Windows 10 ou posteriores.)

![O Android Emulator da Google em tecnologias Hyper-V](../ide/media/xamarin-hyperv-android-emulator.png)

#### <a name="xamarinandroid-designer-split-view-editor"></a>Editor de modo divisão do designer do Xamarin.Android

Também **novo na 15.8**: fizemos melhorias significativas na experiência do designer do Xamarin.Android. Um destaque é o novo editor de modo divisão que permite criar, editar e visualizar seus layouts ao mesmo tempo.

![O editor de modo divisão do designer do Xamarin.Android](../ide/media/android-designer-split-view.png)

Para obter mais informações, confira [Aceleração de hardware para desempenho do emulador](/xamarin/android/get-started/installation/android-emulator/hardware-acceleration?tabs=vswin)

### <a name="visual-studio-app-center"></a>Centro de Aplicativos do Visual Studio

**Novidade na versão 15.5**: o Visual Studio App Center&mdash;que agora está disponível para aplicativos Android, iOS, macOS e Windows&mdash;tem tudo de que você precisa para gerenciar o ciclo de vida dos seus aplicativos, incluindo builds automatizados, testes em dispositivos reais na nuvem, distribuição para testadores beta e lojas de aplicativos e monitoramento do uso real por meio de dados de falha e de análise. Há suporte para aplicativos escritos em Objective-C, Swift, Java, C#, Xamarin e React Native em todos os recursos.

  ![Ambiente de teste do App Center do Visual Studio](../ide/media/app-center-test-env.png)

Para obter mais informações, consulte a postagem no blog [Introducing App Center: Build, test, distribute and monitor apps in the cloud](https://blogs.msdn.microsoft.com/vsappcenter/introducing-visual-studio-app-center/) (Introdução ao App Center: criar, testar, distribuir e monitorar aplicativos na nuvem).

## <a name="cross-platform-development"></a>Desenvolvimento multiplataforma

### <a name="redgate-data-tools"></a>Redgate Data Tools

Para estender as funcionalidades de DevOps para o desenvolvimento do banco de dados do SQL Server, as Redgate Data Tools agora estão disponíveis no Visual Studio.

Incluído no Visual Studio 2017 Enterprise:

* O [Redgate ReadyRoll Core](http://www.red-gate.com/products/sql-development/readyroll/entrypage/microsoft-and-readyroll?utm_source=microsoft&utm_medium=link&utm_campaign=readyroll&utm_term=docs-newinvs) ajuda você a desenvolver scripts de migração, gerenciar alterações no banco de dados usando o controle do código-fonte e automatizar com segurança as implantações de alterações no banco de dados do SQL Server, juntamente com alterações de aplicativos.
* O [Redgate SQL Prompt Core](http://www.red-gate.com/products/sql-development/sql-prompt/entrypage/microsoft-and-sql-prompt?utm_source=microsoft&utm_medium=link&utm_campaign=sqlprompt&utm_term=docs-newinvs) ajuda você a gravar o SQL com maior rapidez e precisão com a ajuda do preenchimento inteligente de código. O SQL Prompt preenche automaticamente palavras-chave e objetos do sistema e do banco de dados, e oferece uma coluna de sugestões conforme você digita. Isso resulta em um código mais simples e em menos erros porque você não precisa se lembrar de cada alias ou nome de coluna.

Incluído em todas as edições do Visual Studio 2017:

* O [Redgate SQL Search](http://www.red-gate.com/products/sql-development/sql-search/?utm_source=microsoft&utm_medium=link&utm_campaign=sqlsearch&utm_term=docs-newinvs) aumenta a produtividade, ajudando-o a localizar rapidamente fragmentos de SQL e objetos em vários bancos de dados.

Para saber mais, consulte a postagem no blog [Redgate Data Tools no Visual Studio 2017](https://blogs.msdn.microsoft.com/visualstudio/2017/03/07/redgate-data-tools-in-visual-studio-2017/).

### <a name="net-core"></a>.NET Core

.NET Core é uma implementação de software livre, modular, multiplataforma e para fins gerais do .NET Standard que contém muitas das mesmas APIs que o .NET Framework.

A plataforma do .NET Core é composta por vários componentes, incluindo os compiladores gerenciados, o tempo de execução, as bibliotecas de classes base e vários modelos de aplicativo, como o ASP.NET Core. O .NET Core dá suporte aos três principais sistemas operacionais: Windows, Linux e macOS. Você pode usar o .NET Core nos cenários inseridos/de IoT, de dispositivo e de nuvem.

Além disso, agora ele é compatível com o Docker.

**Novidade no 15.3**: o Visual Studio 2017 versão 15.3 dá suporte a desenvolvimento no .NET Core 2.0. Usar o .NET Core 2.0 exige baixar e instalar o SDK do .NET Core 2.0 separadamente.

Para obter mais informações, consulte a página [Guia do .NET Core](/dotnet/core/index).

## <a name="games-development"></a>Desenvolvimento de jogos

### <a name="visual-studio-tools-for-unity"></a>Ferramentas do Visual Studio para Unity

Como parte da carga de trabalho "Desenvolvimento de jogos para Unity", incluímos ferramentas para lhe ajudar no desenvolvimento multiplaforma para criação de conteúdo interativo e jogos 2D e 3D. Crie uma vez e publique em 21 plataformas, incluindo todas as plataformas móveis, WebGL, desktops Mac, PC e Linux, Web ou consoles, usando o Visual Studio 2017 e o Unity 5.6.

Para obter mais informações, consulte a página [Ferramentas do Visual Studio para o Unity](../cross-platform/visual-studio-tools-for-unity.md).

## <a name="ai-development"></a>Desenvolvimento do IA

### <a name="visual-studio-tools-for-ai"></a>Ferramentas do Visual Studio para IA

**Novidade na versão 15.5**: use os recursos de produtividade do Visual Studio para acelerar a inovação em IA hoje mesmo. Use recursos do editor de código interno como realce de sintaxe, IntelliSense e formatação automática de texto. É possível testar de forma interativa seu aplicativo de aprendizagem profunda no ambiente local usando o passo a passo de depuração em variáveis locais e modelos.

  ![IDE de aprendizagem profunda](../ai/media/about/ide.png)

Para obter mais informações, consulte a página [Visual Studio Tools for AI](../ai/about-ai-tools.md) (Ferramentas do Visual Studio para IA).

## <a name="whats-next"></a>O que vem a seguir

O Visual Studio 2017 é atualizado frequentemente com novos recursos que melhoram ainda mais a experiência de desenvolvimento. Veja um resumo das atualizações mais importantes que estão em versão prévia experimental:

* **[Live Share](https://visualstudio.microsoft.com/services/live-share/)**, uma nova ferramenta que permite compartilhar uma base de código e seu contexto com um membro da equipe e ter uma colaboração bidirecional instantânea diretamente no Visual Studio. Com o Live Share, um membro da equipe pode ler, navegar, editar e depurar um projeto compartilhado com ele de forma fácil e segura.<br><br>Para saber mais, confira [Live Share FAQ](/visualstudio/liveshare/faq) (Perguntas frequentes sobre o Live Share).<br><br>
* **[IntelliCode](https://visualstudio.microsoft.com/services/intellicode/)**, uma nova funcionalidade que aprimora o desenvolvimento de software usando IA para oferecer melhores conclusões de código com reconhecimento de contexto, orientar os desenvolvedores na codificação de padrões e estilos da equipe, encontrar problemas de código difíceis de detectar e focar as revisões de código em áreas que realmente importam. <br><br>Para saber mais, confira as [Perguntas Frequentes sobre o Visual Studio IntelliCode](../ide/not-in-toc/intellicode-faq.md).

Quer saber mais sobre as novidades do Visual Studio 2017? Confira a página [Roteiro do Visual Studio](/visualstudio/productinfo/vs2018-roadmap).

## <a name="contact-us"></a>Fale conosco

 Por que enviar comentários à equipe do Visual Studio? Porque nós levamos a sério os comentários dos clientes. Eles motivam muito do que fazemos.

Se você quiser sugerir maneiras de melhorar o Visual Studio ou saber mais sobre as opções de suporte ao produto, confira a página [Fale conosco](../ide/talk-to-us.md).

### <a name="report-a-problem"></a>Relatar um problema

 Às vezes, uma mensagem não é suficiente para transmitir o impacto total de um problema que você encontrou. Se você tiver um travamento, uma falha ou outro problema de desempenho, será possível compartilhar facilmente conosco as etapas de reprodução e os arquivos de suporte (como capturas de tela e arquivos de despejo de heap e rastreamento) usando a ferramenta **Relatar um Problema**. Para obter mais informações sobre como usar essa ferramenta, consulte a página [Como relatar um problema](how-to-report-a-problem-with-visual-studio-2017.md).

## <a name="see-also"></a>Consulte também

* [Notas de versão do Visual Studio 2017](/visualstudio/releasenotes/vs2017-relnotes?context=visualstudio/default&contextView=vs-2017)
* [Novidades no Visual C++](/cpp/top/what-s-new-for-visual-cpp-in-visual-studio)
* [Novidades no C#](/dotnet/csharp/whats-new)
* [Novidades para o Team Foundation Server](/tfs/server/whats-new?view=vsts)
* [Novidades no Visual Studio para Mac](https://visualstudio.microsoft.com/vs/visual-studio-mac/)
* [Novidades no Visual Studio 2019](whats-new-visual-studio-2019.md)
