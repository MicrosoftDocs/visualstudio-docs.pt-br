---
title: Visual Studio 2015 | Microsoft Docs
titleSuffix: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 772b6cf4-cee5-42d0-bc18-b4eb07e22ff0
caps.latest.revision: 36
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: c6bd4e34e25add01de6e6e54c2439c2ca80ccf33
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53062477"
---
# <a name="visual-studio-ide"></a>Visual Studio IDE
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]
O Microsoft Visual Studio 2015 é um pacote de ferramentas de criação de software que abrange desde a fase de planejamento até o design da interface do usuário, a codificação, o teste, a depuração, a análise da qualidade e do desempenho do código, a implantação nos clientes e a coleta de telemetria de uso. Essas ferramentas foram projetadas para funcionar em conjunto da maneira mais perfeita possível e são todas expostas por meio do Ambiente de Desenvolvimento Integrado (IDE) do Visual Studio.

Você pode usar o Visual Studio para criar vários tipos de aplicativos, desde aplicativos simples de armazenamento e jogos para clientes móveis, até sistemas grandes e complexos que movimentam empresas e data centers. Você pode criar:

- aplicativos e jogos executados não somente no Windows, mas também no Android e no iOS.

- sites e serviços Web com base em ASP.NET, JQuery, AngularJS e outras estruturas populares.

- aplicativos para plataformas e dispositivos tão diversos quanto: Azure, Office, Sharepoint, Hololens, Kinect e Internet das Coisas, para citar apenas alguns exemplos.

- jogos e aplicativos com uso intensivo de gráficos para uma variedade de dispositivos Windows, incluindo o Xbox, usando o DirectX.

O Visual Studio por padrão fornece suporte para C#, C e C++, JavaScript, F#e o Visual Basic. Visual Studio funciona e se integra bem com aplicativos de terceiros como o Unity por meio de [ferramentas do Visual Studio para Unity](../cross-platform/visual-studio-tools-for-unity.md) extensão e Apache Cordova por meio de [Visual Studio Tools for Apache Cordova](http://msdn.microsoft.com/library/db446f2c-6ba4-4c76-aac5-4c66f43b8c42). Você pode estender o Visual Studio por conta própria, criando ferramentas personalizadas que realizem tarefas especializadas.

Se você nunca usou o Visual Studio antes, aprenda os conceitos básicos com nossos [Introdução ao desenvolvimento com o Visual Studio](../ide/get-started-developing-with-visual-studio.md) tutoriais e explicações passo a passo.

Se você quiser saber sobre os novos recursos no Visual Studio 2015, consulte [o que há de novo no Visual Studio 2015](../what-s-new-in-visual-studio-2015.md).

## <a name="visual-studio-setup"></a>Configuração do Visual Studio
 Você pode descobrir qual edição do Visual Studio é adequada para você na [edições do Visual Studio](http://www.visualstudio.com/products/visual-studio-with-msdn-overview-vs).

 É possível instalar o Visual Studio 2015 baixando-o em [Downloads do Visual Studio](http://www.visualstudio.com/downloads/download-visual-studio-vs.aspx). Se você precisar saber mais sobre o processo de instalação, consulte [instalar o Visual Studio 2015](../install/install-visual-studio-2015.md).

## <a name="ide-basics"></a>Noções básicas do IDE
 A imagem a seguir mostra o IDE do Visual Studio com um projeto aberto, e a janela do Gerenciador de soluções para navegar nos arquivos de projeto e a janela do Team Explorer para navegar em código-fonte controlam e acompanhamento de item de trabalho. Os recursos na barra de título são destacadas são explicados abaixo em mais detalhes.

 ![IDE do Visual Studio](../ide/media/visualstudioide.png "VisualStudioIDE")

### <a name="signing-in"></a>Entrando
 Ao iniciar o Visual Studio pela primeira vez, você pode entrar usando sua conta da Microsoft ou sua conta corporativa ou de estudante. Ao entrar você poderá sincronizar suas configurações, como layouts de janela, entre vários dispositivos e conectar-se automaticamente aos serviços que precisar, como as assinaturas do Azure e o Visual Studio Team Services. Se você tiver uma licença baseada em assinatura, será necessário entrar no Visual Studio regularmente para manter seu token de licença atualizado. Se você tiver uma licença de chave do produto (Product Key), não será necessário entrar, mas se você o fizer será muito mais conveniente para conectar-se ao Visual Studio Team Services e às suas contas com o Azure, Office 365 e Salesforce.com. Para obter mais informações, consulte [Entrando no Visual Studio](../ide/signing-in-to-visual-studio.md).

 Se você tiver várias contas do Visual Studio Team Services, várias contas do Azure ou várias assinaturas do MSDN, poderá vinculá-las e acessar recursos e serviços em todas as suas contas com um logon único. Para obter mais informações, consulte [Trabalhar com várias contas de usuário](../ide/work-with-multiple-user-accounts.md).

### <a name="staying-up-to-date"></a>Manter-se atualizado
 O ícone de notificação no canto superior direito da barra de título informa quando as atualizações estão disponíveis para o Visual Studio ou qualquer componente relacionado que você instalou. Você pode optar por descartar ou tomar ação em relação a essas notificações. Para obter mais informações, consulte [Notificações do Visual Studio](../ide/visual-studio-notifications.md).

### <a name="finding-things-and-getting-help"></a>Localizando coisas e obter ajuda
 O [início rápido](../ide/reference/quick-launch-environment-options-dialog-box.md) janela mostrada abaixo é uma maneira rápida de localizar os comandos do Visual Studio, ferramentas e recursos e assim por diante quando você não souber o local de menu de atalho ou do teclado. Basta digitar o que você está procurando e o Início Rápido lhe dará um link para a informação.

 ![Resultados de Início Rápido para 'novo projeto'](../ide/media/productivity-quicklaunch.png "Productivity_QuickLaunch")

 O MSDN é o site da Microsoft para obter a documentação técnica; Você está lendo esta página no MSDN agora! No Visual Studio, você pode pressionar **F1** para ir para a página de Ajuda do MSDN para a janela ativa. Você também pode pressionar **F1** no editor de código para ir para a página de Ajuda do MSDN para a API ou a palavra-chave na posição atual do cursor. Por exemplo, em um arquivo c#, coloque o cursor em algum lugar ou no final de uma `System.String` declaração e pressione **F1** para ir para a página de Ajuda do MSDN para <xref:System.String>.

### <a name="giving-feedback"></a>Fornecendo comentários
 É fácil fornecer comentários sobre o Visual Studio sempre que você quiser. Clique no ícone de comentários na barra de título ao lado de **QuickLaunch** e, em seguida, clique em **Relatar um problema** ou **Fornecer uma sugestão**. Edições de pré-lançamento do Visual Studio também tem uma opção **Classificar este Produto**. Examinamos todos esses comentários e usamos para aprimorar o produto. Para obter mais informações, consulte [Fale conosco](../ide/talk-to-us.md).

### <a name="personalizing-the-ide"></a>Personalizando o IDE
 Você pode personalizar o layout da janela de acordo com seu estilo de desenvolvimento. Você pode encaixar, deixar flutuante ou ocultar qualquer janela a qualquer momento e também pode executar o editor no modo de tela inteira. Você pode criar e salvar vários layouts de janela personalizados que mostram apenas as janelas necessárias para contextos específicos. Por exemplo, é possível criar um layout de tela inteira para ver apenas o editor de código. E você pode criar layouts diferentes para depuração e para operações de equipe. Para obter mais informações, consulte [Personalizando layouts de janela](../ide/customizing-window-layouts-in-visual-studio.md).

 Você poderá personalizar o Visual Studio de muitas outras formas e usar perfil móvel das configurações se você trabalhar em vários computadores. Para obter mais informações, confira [Personalizando o IDE](../ide/personalizing-the-visual-studio-ide.md).

 Existem atalhos de teclado para quase tudo e também é possível personalizá-los. Para criar novos atalhos, digite "Teclado" em Início Rápido para abrir a caixa de diálogo Teclado. A partir daí, você pode pressionar F1 para ir para a página de Ajuda do MSDN, se você precisar de mais informações sobre as opções. Para obter mais informações, consulte [Atalhos de teclado padrão no Visual Studio](../ide/default-keyboard-shortcuts-in-visual-studio.md).

## <a name="connecting-to-visual-studio-team-services-and-team-foundation-server"></a>Conectar-se ao Visual Studio Team Services e o Team Foundation Server
 O VSTS (Visual Studio Team Services) é um serviço baseado em nuvem para hospedagem de projetos de software e para habilitar a colaboração nas equipes. O VSTS oferece suporte a sistemas Git e Team Foundation Source Control, bem como as metodologias de desenvolvimento Agile, CMMI e Scrum. O TFVC (Controle de Versão do Team Foundation) usa um repositório de servidor único e centralizado para arquivos de versão e de controle. É sempre feito check-in das alterações locais no servidor central em que outros desenvolvedores podem obter as alterações mais recentes. O TFS (Team Foundation Server) 2015 é o hub de gerenciamento do ciclo de vida do aplicativo para o Visual Studio. Ele habilita a participação de todos os envolvidos com o processo de desenvolvimento usando uma única solução. O TFS também é útil para gerenciar equipes e projetos heterogêneos.

 Se você tiver uma conta do Visual Studio Team Services ou um Team Foundation Server em sua rede, será possível conectar-se a eles através da janela do Team Explorer. Nessa janela você pode fazer check-in ou check-out de código no controle do código-fonte, gerenciar itens de trabalho, iniciar compilações e acessar salas da equipe e workspaces. Você pode abrir o Team Explorer na **início rápido** ou no menu principal, em **exibir &#124; Team Explorer** ou do **equipe &#124; gerenciar conexões**.  Para obter mais informações sobre o Visual Studio Team Services, consulte [www.visualstudio.com](https://www.visualstudio.com/). Para obter mais informações sobre o Team Foundation Server, consulte [Team Foundation Server](https://www.visualstudio.com/products/tfs-overview-vs).

 A imagem a seguir mostra o painel do Team Explorer para uma solução que é hospedada no VSTS:

 ![Visual Studio Team Explorer](../ide/media/vs2015-teamexplorer.png "VS2015_TeamExplorer")

## <a name="creating-solutions-and-projects"></a>Criando soluções e projetos
 Embora você possa usar o Visual Studio para procurar arquivos de código individuais, é mais comum que você esteja trabalhando em um *Projeto*. Um projeto do Visual Studio é uma coleção de arquivos e recursos que são compilados em um arquivo executável binário único para aplicativos (por exemplo, um .exe, DLL ou appx). Para sites que não são de ASP.NET, nenhum executável é produzido e o projeto contém apenas o HTML, os arquivos JavaScript e as imagens. Como você pode precisar criar vários binários ou sites que estão bastante relacionados algumas vezes, o Visual Studio tem o conceito de Solução, que pode conter vários projetos ou sites. Quando você cria um projeto, na verdade está criando um projeto em uma solução e depois você pode adicionar mais projetos a essa solução se precisar. Por exemplo, se você tiver um projeto de DLL, você poderá adicionar um projeto .exe à solução que carrega e consome a DLL.

 Um *modelo de projeto* é uma coleção de arquivos de código e definições de configuração previamente preenchidos que você configura rapidamente para criar um tipo específico de aplicativo. O Visual Studio vem com muitos modelos de projeto para escolher e se nenhum dos modelos padrão funcionar pra você, é possível criar os seus próprios modelos. Depois de criar um projeto com um modelo, você pode começar a escrever seu próprio código nele, seja nos arquivos fornecidos ou em novos arquivos adicionados. Para obter mais informações, consulte [Soluções e projetos](../ide/solutions-and-projects-in-visual-studio.md). A ilustração a seguir mostra a caixa de diálogo Novo Projeto com os modelos de projeto que estão disponíveis para aplicativos ASP.NET.

 ![Caixa de diálogo Novo projeto do Visual Studio](../ide/media/vs2015-newprojectdialog.png "VS2015_NewProjectDialog")

## <a name="designing-the-user-interface"></a>Projetando a interface do usuário
 Um designer é uma ferramenta intuitiva que permite que você crie uma interface do usuário sem escrever código. Você pode arrastar controles da interface do usuário, como caixas de listagem, calendários e botões do [caixa de ferramentas](../ide/reference/toolbox.md) janela na superfície de design que representa a caixa de diálogo ou janela. Você pode redimensionar e reorganizar os elementos sem escrever nenhum código. Designers são incluídos para qualquer tipo de projeto que tem uma interface do usuário.

 Se o projeto tiver uma interface de usuário baseada em XAML, o designer padrão é o Blend para Visual Studio, uma ferramenta de gráficos sofisticados que funciona perfeitamente com o Visual Studio.

 ![Prancheta](../ide/media/b5-artboard.png "b5_artboard")

|||
|-|-|
|![](../designers/media/b1-1.png "B1_1")|**Modo de exibição de Design** Mostra o design visual do documento. Nesse modo de exibição, você pode desenhar ou modificar objetos na superfície de design.|
|![](../designers/media/b1-2.png "B1_2")|**Navegação estrutural** Mova-se rapidamente entre o modo de edição de modelo, o modo de edição de estilo e o escopo de edição de objeto em um objeto selecionado.|
|![](../designers/media/b1-3.png "B1_3")|**Aplicar zoom** Use para ampliar a superfície de design ou os objetos dela.|
|![](../designers/media/b1-4.png "B1_4")|**Controles da superfície de design** Use esses controles (**Mostrar grade de ajuste**, **Ajustar às linhas de grade** e **Habilitar ou desabilitar ajuste às guias de alinhamento**) para definir as opções de ajuste. Ajustes são úteis para alinhar objetos uns aos outros ou em linhas com espaçamento uniforme na superfície de design.|
|![](../designers/media/b1-5.png "B1_5")|**Editor de códigos** Edite seu código XAML, C#, C++ ou Visual Basic manualmente no editor de códigos.|

 Para obter mais informações, consulte [projetar XAML no Visual Studio e no Blend para Visual Studio](../designers/designing-xaml-in-visual-studio.md).

## <a name="writing-navigating-and-understanding-code"></a>Escrever, navegar e compreensão do código
 Se você é um desenvolvedor, a janela do editor é o lugar em que você provavelmente passa a maior parte do tempo. O Visual Studio inclui editores para C#, C++, Visual Basic, JavaScript, XML, HTML, CSS, e F#, e terceiros oferecem editores de plug-in (e compiladores) para muitas outras linguagens.

 Você pode editar os arquivos individuais no editor de texto clicando **arquivo &#124; abrir &#124; arquivo.** Para editar arquivos em um projeto aberto, clique no nome do arquivo no Gerenciador de soluções. O código é colorizado e você pode personalizar o esquema de cores digitando "Cores" no Início Rápido. Você pode ter várias janelas do editor de texto com guias abertas ao mesmo tempo. Você pode dividir cada janela de forma independente. Também é possível executar o editor de texto no modo de tela inteira.

 ![Greetingsconsoleapp no editor de códigos](../ide/media/c-ide-editorlinenumberswordwrapon.png "IDE_EditorLineNumbersWordWrapOn C + +")

 O editor de texto é altamente interativo (se desejar que ele seja assim), com muitos recursos de produtividade que ajudarão a escrever códigos mais rapidamente. Os recursos variam por linguagem, e você não precisa usar qualquer um deles (tipo de "Editor" no início rápido) para ativar ou desativar recursos do: Alguns dos recursos de produtividade comuns são:

1. [Refatoração](../ide/refactoring-in-visual-studio.md) inclui operações como renomeação inteligente de variáveis, movimentação de linhas de código selecionadas para uma função distinta, movimentação do código para outros locais, reordenação de parâmetros de função e muito mais.

2. *IntelliSense* é um termo abrangente para um conjunto de recursos populares que exibe informações de tipo sobre seu código diretamente no editor e, em alguns casos, escreve pequenos pedaços de código pra você. É como ter a documentação básica embutida no editor, o que evita que você tenha que consultar informações de tipo em uma janela de ajuda separada. Os recursos do IntelliSense variam de acordo com a linguagem. Para obter mais informações, consulte [IntelliSense do Visual C#](../ide/visual-csharp-intellisense.md), [IntelliSense do Visual C++](../ide/visual-cpp-intellisense.md), [IntelliSense do JavaScript](../ide/javascript-intellisense.md), [IntelliSense específico do Visual Basic](../ide/visual-basic-specific-intellisense.md). A ilustração a seguir mostra alguns recursos do IntelliSense em funcionamento:

    ![Lista de membros do Visual Studio](../ide/media/vs2015-intellisense.png "vs2015_Intellisense")

3. **Rabiscos** alerta sobre erros ou problemas potenciais em seu código em tempo real, enquanto você digita, permitindo que você corrija imediatamente sem esperar que o erro seja descoberto durante o momento da compilação ou da execução. Se você passar o mouse sobre o rabisco, verá informações adicionais sobre o erro. Uma lâmpada também podem aparecer na margem esquerda com sugestões de como corrigir o erro. Para obter mais informações, consulte [Realizar ações rápidas com lâmpadas](../ide/perform-quick-actions-with-light-bulbs.md).

    ![Lâmpada com o mouse focalizando](../ide/media/vs2015-lightbulb-hover.png "VS2015_LightBulb_Hover")

4. [Indicadores](../ide/setting-bookmarks-in-code.md) permitem que você navegue rapidamente até linhas específicas nos arquivos em que você está trabalhando ativamente.

5. A janela [Hierarquia de Chamada](../ide/reference/call-hierarchy.md) pode ser invocada no menu de contexto do editor de texto para mostrar os métodos que chamam e são chamados pelo método sob o cursor.

6. **Lentes de Código** permitem localizar referências e alterações em seu código, bugs vinculados, itens de trabalho, revisões de código e testes de unidade, tudo sem sair do editor. Para obter mais informações, consulte [Localizar alterações de código e outros históricos](../ide/find-code-changes-and-other-history-with-codelens.md).

7. A janela **Espiar Definição** mostra uma definição de método ou de tipo embutida, sem navegar para fora de seu contexto atual. Agora esta janela funciona também para XAML.

8. A opção de menu de contexto **Ir para Definição** leva você diretamente para o local em que a função ou o objeto estão definidos. Outros comandos de navegação também estão disponíveis clicando com o botão direito do mouse no editor.

9. Uma ferramenta relacionada, o [Pesquisador de Objetos](http://msdn.microsoft.com/en-us/f89acfc5-1152-413d-9f56-3dc16e3f0470), habilita a inspeção de assemblies de .NET ou de Windows Runtime em seu sistema para ver que tipos eles contêm e quais métodos e propriedades esses tipos contêm.

     ![Pesquisador de Objetos mostrando System.Timer](../ide/media/objectbrowser.png "ObjectBrowser")

   A maioria dos itens no menu Editar e no menu Exibir está relacionada ao editor de códigos de alguma forma. Para obter mais informações sobre o editor, consulte [Escrevendo código](../ide/writing-code-in-the-code-and-text-editor.md) e [Editando seu código](https://www.visualstudio.com/features/ide-vs).

## <a name="compiling-and-building-your-code"></a>Compilando e criando seu código

Criar um projeto significa para compilar o código-fonte e executar todas as etapas necessárias para produzir o executável. Linguagens diferentes têm operações de build diferentes e sites regulares não compilam. Independentemente do tipo de projeto, o menu Compilar é o local padrão para esses comandos. Para compilar e executar seu código com um único pressionamento de teclas, pressione F5. Todo compilador é completamente configurável por meio do IDE. A barra de ferramentas Compilar permite que você especifique se deseja criar uma versão de depuração do programa, com símbolos e verificação de erros adicional habilitada para dar suporte a pontos de interrupção e etapa única no depurador ou a um build de lançamento, que é o que você finalmente entregará aos usuários. Você pode configurar mais definições de build e muitas outras configurações na página de propriedades de um projeto. Clique com botão direito no nó do projeto no Gerenciador de soluções e escolha Propriedades. Você também pode executar compilações da linha de comando.

A saída da compilação, incluindo uma mensagem de erro ou sucesso, aparecem na **saída** janela. O **Error List** mostra informações detalhadas sobre erros de compilação.

## <a name="debugging-your-code"></a>Depurando seu código
 Depurador de última geração do Visual Studio permite depurar o código em execução no seu projeto local, em um dispositivo remoto ou em um emulador, como aqueles para Android ou Windows Phone. Você pode percorrer o código em uma declaração por vez e inspecionar variáveis à medida que avança, você pode percorrer aplicativos com multithread e pode definir pontos de interrupção que são atingidos somente quando uma condição especificada for verdadeira. Tudo isso pode ser configurado no editor de códigos em si, para que você não precisa deixar o contexto do seu código.

 ![Janela de inspeção de configurações do ponto de interrupção](../ide/media/dbg-breakpoints-peekwindow.png "DBG_Breakpoints_PeekWindow")

 O próprio depurador tem várias janelas que permitem que você exiba e manipule variáveis locais, a pilha de chamadas e outros aspectos do ambiente de tempo de execução. Você pode encontrar essas janelas no menu **Depurar**.

 A [Janela Imediata](../ide/reference/immediate-window.md) permite a digitação de uma expressão e a visualização imediada de seu resultado.

 A janela [IntelliTrace](http://msdn.microsoft.com/en-us/629e9660-c59a-446b-8c30-290059158f61) registra cada chamada de método e outros eventos em um programa .NET em execução e pode ajudar a localizar rapidamente a origem de um problema.

 Para obter mais informações, consulte [Depuração no Visual Studio](../debugger/debugging-in-visual-studio.md).

## <a name="testing-your-code"></a>Testar seu código
 O Visual Studio inclui uma estrutura de teste de unidade para código gerenciado (.NET) e outra para o C++ nativo. Para criar testes de unidade é só adicionar um Projeto de Teste à sua solução, escrever seus testes e, em seguida, executá-los na janela Gerenciador de Testes. Para obter mais informações, consulte [Efetuar teste de unidade em seu código](../test/unit-test-your-code.md).

 ![Gerenciador de testes de unidade](../ide/media/ute-failedpassednotrunsummary.png "UTE_FailedPassedNotRunSummary")

## <a name="analyzing-code-quality-and-performance"></a>Analisando a qualidade do código e o desempenho
 O Visual Studio inclui ferramentas avançadas para análise estática e em tempo de execução. As ferramentas de análise estática ajudam a identificar possíveis erros no design, na globalização, na interoperabilidade, no desempenho, na segurança e em outras categorias. O teste de desempenho ou criação de perfil envolve a medição de como o seu programa é executado. Acesse essas ferramentas no menu **Analisar**. Para obter mais informações, consulte [Melhorando a qualidade com as ferramentas de diagnóstico do Visual Studio](http://msdn.microsoft.com/library/73baa961-c21f-43fe-bb92-3f59ae9b5945).

## <a name="connecting-to-cloud-services-and-databases"></a>Conectar-se a bancos de dados e serviços de nuvem
 O [Gerenciador de servidores](http://msdn.microsoft.com/library/4ea29b3b-bbb2-45e4-9082-eaf635c41c4d) janela no Visual Studio mostra os recursos em todas as contas gerenciadas na sua conta de personalização (aquele com você fez logon), incluindo instâncias do SQL Server, Azure, Salesforce.com, Office 365, e sites da Web.

 ![Gerenciador de servidores](../ide/media/vs2015-serverexplorer3.png "vs2015_ServerExplorer3")

 O Visual Studio inclui o [SSDT](https://msdn.microsoft.com/data/tools.aspx) (Microsoft SQL Server Data Tools), que permite você criar, depurar, manter e refatorar bancos de dados. Você pode trabalhar com um projeto de banco de dados ou diretamente com uma instância local ou não de banco de dados conectado.

 O Pesquisador de Objetos do SQL Server no Visual Studio oferece uma exibição de seus objetos de banco de dados semelhante à do SQL Server Management Studio. O Pesquisador de Objetos do SQL Server permite que você realize tarefas de administração e design leves de banco de dados, incluindo edição de dados de tabela, comparação de esquemas e execução de consultas usando menus contextuais diretamente do Pesquisador de Objetos do SQL Server. O SSDT também inclui tipos de projetos e ferramentas especiais para desenvolvimento de soluções de BI (Business Intelligence) do SQL Server 2012 Analysis Services, Reporting Services e Integration Services (anteriormente conhecidas como Business Intelligence Development Studio).

 ![Pesquisador de objetos do SQL Server](../ide/media/vs2015-sqlobjectexplorer.png "vs2015_SQLObjectExplorer")

## <a name="deploying-your-finished-application"></a>Implantar o aplicativo concluído
 Quando seu aplicativo está pronto ser implantado para os clientes, o Visual Studio fornece as ferramentas para fazer isso, não importa se você está implantando na Windows Store, em um site do SharePoint ou com tecnologias InstallShield ou o Windows Installer. Tudo isso está acessível por meio do IDE. Para obter mais informações, consulte [Implantação de aplicativos, serviços e componentes](../deployment/deploying-applications-services-and-components.md).

## <a name="architecture-and-modeling-tools-enterprise-only"></a>Ferramentas de arquitetura e modelagem (somente Enterprise)
 Você pode usar as ferramentas de arquitetura e modelagem do Visual Studio para projetar e modelar seu aplicativo. Essas ferramentas ajudam a visualizar a estrutura, o comportamento e as relações do código. Você pode criar modelos em diferentes níveis de detalhe em todo o ciclo de vida do aplicativo como parte do processo de desenvolvimento. Você pode controlar os requisitos, as tarefas, os casos de teste, os bugs e outros trabalhos associados com seus modelos vinculando os elementos de modelo a itens de trabalho do Team Foundation Server e ao plano de desenvolvimento. Para obter mais informações, consulte [Criar design e modelar seu aplicativo](../modeling/analyze-and-model-your-architecture.md).

## <a name="extending-visual-studio-through-the-visual-studio-sdk"></a>Estendendo o Visual Studio por meio do SDK do Visual Studio
 O Visual Studio é uma plataforma extensível. Uma extensão do Visual Studio é uma ferramenta personalizada que se integra com o IDE. Você pode adicionar extensões de terceiros ou criar suas próprias extensões. Para obter mais informações, consulte [Desenvolvendo extensões do Visual Studio](http://msdn.microsoft.com/library/5b1b5db3-6005-44cf-83b0-e608d7764d14).

 As [Diretrizes de experiência de usuário do Visual Studio](../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md) são uma referência essencial para qualquer pessoa que deseja escrever extensões para o Visual Studio. Essas diretrizes específicas da plataforma incluem informações sobre design, fontes, cores, ícones, controles comuns e outros padrões de interação de caixa de diálogo que farão com que seu novo recurso se integre de maneira perfeita com o Visual Studio.

## <a name="in-this-guide"></a>Neste guia

|||
|-|-|
|[Contas de usuário e atualizações](../ide/user-accounts-and-updates.md)|[Personalizando o IDE](../ide/personalizing-the-visual-studio-ide.md)|
|[Como: Mover-se no IDE](../ide/how-to-move-around-in-the-visual-studio-ide.md)|[Introdução ao desenvolvimento com o Visual Studio](../ide/get-started-developing-with-visual-studio.md)|
|[Localizando e usando extensões do Visual Studio](../ide/finding-and-using-visual-studio-extensions.md)|[Soluções e projetos](../ide/solutions-and-projects-in-visual-studio.md)|
|[Escrevendo código](../ide/writing-code-in-the-code-and-text-editor.md)|[Depurando no Visual Studio](../debugger/debugging-in-visual-studio.md)|
|[Ferramentas de Criação de Perfil](../profiling/profiling-tools.md)|[Melhorar a qualidade do código](http://msdn.microsoft.com/library/73baa961-c21f-43fe-bb92-3f59ae9b5945)|
|[Criando interfaces do usuário](../designers/designing-user-interfaces.md)|[Análise e modelagem de arquitetura](../modeling/analyze-and-model-your-architecture.md)|
|[Compilando e criando](../ide/compiling-and-building-in-visual-studio.md)|[Implantando aplicativos, serviços e componentes](../deployment/deploying-applications-services-and-components.md)|
|[Suporte ao IDE do Visual Studio de 64 bits](../ide/visual-studio-ide-64-bit-support.md)|[Segurança](../ide/security-in-visual-studio.md)|
|[Exemplos do Visual Studio](../ide/visual-studio-samples.md)|[Microsoft Help Viewer](../ide/microsoft-help-viewer.md)|
|[Globalizando e localizando aplicativos](../ide/globalizing-and-localizing-applications.md)|[Referência da interface do usuário](../ide/reference/general-user-interface-elements-visual-studio.md)|

## <a name="see-also"></a>Consulte também

- [Instalação do Visual Studio 2015](../install/install-visual-studio-2015.md)
- [Editando seu código](https://www.visualstudio.com/features/ide-vs)
- [Novidades no Visual Studio 2015](../what-s-new-in-visual-studio-2015.md)
- [Portabilidade, migração e atualização de projetos do Visual Studio](../porting/porting-migrating-and-upgrading-visual-studio-projects.md)
- [Fale conosco](../ide/talk-to-us.md)