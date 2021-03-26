---
title: Dentro do SDK do Visual Studio | Microsoft Docs
description: Saiba mais sobre as extensões do SDK do Visual Studio, incluindo arquitetura, componentes, serviços, esquemas e utilitários do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- roadmap, Visual Studio integration SDK
- Visual Studio integration SDK roadmap
- integration roadmap, Visual Studio SDK
ms.assetid: 9118eaa4-0453-4dc5-9e16-c7062d254869
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e11ee862f43ead3605d8e07dc159e18da13413b8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074698"
---
# <a name="inside-the-visual-studio-sdk"></a>Por dentro do SDK do Visual Studio

Esta seção fornece informações detalhadas sobre as extensões do Visual Studio, incluindo arquitetura do Visual Studio, componentes, serviços, esquemas, utilitários e similares.

## <a name="extensibility-architecture"></a>Arquitetura de extensibilidade
 A ilustração a seguir mostra a arquitetura de extensibilidade do Visual Studio. O VSPackages fornece a funcionalidade do aplicativo, que é compartilhada no IDE como serviços. O IDE padrão também oferece uma ampla gama de serviços, como <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> , que fornecem acesso à funcionalidade de janela do IDE.

 ![Gráfico de arquitetura do ambiente](../../extensibility/internals/media/environment.gif "ambiente") Visão generalizada da arquitetura do Visual Studio

## <a name="vspackages"></a>VSPackages
 VSPackages são módulos de software que compõem e estendem o Visual Studio com elementos, serviços, projetos, editores e designers da interface do usuário. VSPackages são a unidade de arquitetura central do Visual Studio. Para obter mais informações, consulte [VSPackages](../../extensibility/internals/vspackages.md).

## <a name="visual-studio-shell"></a>Shell do Visual Studio
 O Shell do Visual Studio fornece funcionalidade básica e dá suporte à comunicação cruzada entre suas extensões VSPackages e MEF de componente. Para obter mais informações, consulte [shell do Visual Studio](../../extensibility/internals/visual-studio-shell.md).

## <a name="user-experience-guidelines"></a>Diretrizes da Experiência do Usuário
 Se você estiver planejando criar novos recursos para o Visual Studio, consulte estas diretrizes para obter dicas de design e usabilidade: [diretrizes de experiência do usuário do Visual Studio](../../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md).

## <a name="commands"></a>Comandos
 Os comandos são funções que realizam tarefas, como imprimir um documento, atualizar uma exibição ou criar um novo arquivo.

 Ao estender o Visual Studio, você pode criar comandos e registrá-los com o Shell do Visual Studio. Você pode especificar como esses comandos serão exibidos no IDE, por exemplo, em um menu ou barra de ferramentas. Normalmente, um comando personalizado é exibido no menu **ferramentas** , e um comando para exibir uma janela de ferramentas apareceria no outro submenu do **Windows** do menu **Exibir** .

 Ao criar um comando, você também deve criar um manipulador de eventos para ele. O manipulador de eventos determina quando o comando é visível ou habilitado, permite que você modifique seu texto e garante que o comando responda adequadamente quando for ativado. Na maioria dos casos, o IDE manipula os comandos usando a <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface. Os comandos no Visual Studio são tratados começando com o contexto de comando mais interno, com base na seleção local, e prosseguindo para o contexto mais externo, com base na seleção global. Os comandos adicionados ao menu principal estão imediatamente disponíveis para scripts.

 Para obter mais informações, consulte [comandos, menus e barras de ferramentas](../../extensibility/internals/commands-menus-and-toolbars.md).

## <a name="menus-and-toolbars"></a>Menus e barras de ferramentas
 Menus e barras de ferramentas fornecem uma maneira para os usuários invocarem comandos. Os menus são linhas ou colunas de comandos que normalmente são exibidos como itens de texto individuais na parte superior de uma janela de ferramentas. Os submenus são menus secundários que aparecem quando um usuário clica em comandos que incluem uma pequena seta. Menus de contexto aparecem quando um usuário clica com o botão direito do mouse em determinados elementos da interface do usuário Alguns nomes de menu comuns são **arquivo**, **Editar**, **Exibir** e **janela**. Para obter mais informações, consulte [estendendo menus e comandos](../../extensibility/extending-menus-and-commands.md).

 As barras de ferramentas são linhas ou colunas de botões e outros controles, como caixas de combinação, caixas de listagem e caixas de texto. Os botões da barra de ferramentas normalmente têm imagens de ícone, como um ícone de pasta para um comando de **arquivo aberto** ou uma impressora para um comando **Print** . Todos os elementos da barra de ferramentas são associados a comandos. Quando você clica em um botão da barra de ferramentas, seu comando associado é executado. No caso de um controle suspenso, cada item na lista suspensa é associado a um comando diferente. Alguns controles da barra de ferramentas, como um controle de Splitter, são híbridos. Um lado do controle é um botão da barra de ferramentas e o outro lado é uma seta para baixo que exibe vários comandos quando ele é clicado.

## <a name="tool-windows"></a>Janelas de ferramentas
 As janelas de ferramentas são usadas no IDE para exibir informações. A **caixa de ferramentas**, **Gerenciador de soluções**, janela **Propriedades** e **navegador da Web** são exemplos de janelas de ferramentas.

 As janelas de ferramentas normalmente oferecem vários controles com os quais o usuário pode interagir. Por exemplo, a janela **Propriedades** permite que o usuário defina as propriedades de objetos que atendem a uma finalidade específica. A janela **Propriedades** é especializada nesse sentido, mas também em geral porque ela pode ser usada em muitas situações diferentes. Da mesma forma, a janela de **saída** é especializada porque fornece saída baseada em texto, mas geral porque muitos subsistemas no Visual Studio podem usá-lo para fornecer saída para o usuário do Visual Studio.

 Considere a seguinte imagem do Visual Studio, que contém várias janelas de ferramentas:

 ![Captura de tela](../../extensibility/internals/media/t1gui.png "T1gui")

 Algumas das janelas de ferramentas são encaixadas juntas em um único painel que exibe a janela de ferramentas de Gerenciador de Soluções e oculta as outras janelas de ferramentas, mas as torna disponíveis clicando em guias. A imagem mostra duas outras janelas de ferramentas, a **lista de erros** e a janela de **saída** , encaixadas juntas em um único painel.

 Também é mostrado o painel principal do documento, que mostra várias janelas do editor. Embora as janelas de ferramentas normalmente tenham apenas uma instância (por exemplo, você pode abrir apenas uma **Gerenciador de soluções**), as janelas do editor podem ter várias instâncias, cada uma delas usada para editar um documento separado, mas todas elas são encaixadas no mesmo painel. A imagem mostra um painel de documentos que tem duas janelas de editor, uma janela de designer de formulário. Todas as janelas no painel do documento estão disponíveis clicando em guias, mas a janela do editor que contém o arquivo legenda. cs é visível e ativa.

 Ao estender o Visual Studio, você pode criar janelas de ferramentas que permitem que os usuários do Visual Studio interajam com sua extensão. Você também pode criar seus próprios editores que permitem que os usuários do Visual Studio editem documentos. Como suas janelas de ferramentas e editores serão integrados ao Visual Studio, você não precisará programá-las para encaixar ou aparecer em uma guia corretamente. Quando eles são registrados corretamente no Visual Studio, eles terão automaticamente os recursos típicos de janelas de ferramentas e janelas de documentos no Visual Studio. Para obter mais informações, consulte [estendendo e personalizando janelas de ferramentas](../../extensibility/extending-and-customizing-tool-windows.md).

## <a name="document-windows"></a>Janelas de documento
 Uma janela de documento é uma janela filho emoldurada de uma janela MDI (interface de vários documentos). As janelas de documentos normalmente são usadas para hospedar editores de texto, editores de formulário (também conhecidos como designers) ou controles de edição, mas também podem hospedar outros tipos funcionais. A caixa de diálogo **novo arquivo** inclui exemplos de janelas de documentos que o Visual Studio fornece.

 A maioria dos editores é específica a uma linguagem de programação ou a um tipo de arquivo, como páginas HTML, conjuntos de quadros, arquivos C++ ou arquivos de cabeçalho. Ao selecionar um modelo na caixa de diálogo **novo arquivo** , um usuário cria dinamicamente uma janela de documento para o editor para o tipo de arquivo que está associado ao modelo. Uma janela de documento também é criada quando um usuário abre um arquivo existente.

 As janelas de documentos são restritas à área do cliente MDI. Cada janela de documento tem uma guia na parte superior e a ordem de tabulação é vinculada a outras janelas que podem estar abertas na área MDI. Clicar com o botão direito do mouse na guia de uma janela do documento exibe um menu de atalho que inclui opções para dividir a área MDI em vários grupos de guias horizontais ou verticais. A divisão da área MDI permite que vários arquivos sejam exibidos ao mesmo tempo. Para obter mais informações, consulte [janelas de documentos](../../extensibility/internals/document-windows.md).

## <a name="editors"></a>Editores
 O editor do Visual Studio permite personalizá-lo e usá-lo para seu próprio tipo de conteúdo por meio do Managed Extensibility Framework (MEF). Em muitos casos, você não precisará criar um VSPackage para estender o editor, embora se queira incluir recursos do Shell (por exemplo, um comando de menu ou uma tecla de atalho), você pode combinar uma extensão de MEF com um VSPackage.

 Você também pode criar um editor personalizado, por exemplo, se desejar ler e gravar em um banco de dados ou se desejar usar um designer. Você também pode usar um editor externo, como o bloco de notas ou o Microsoft WordPad. Para obter mais informações, consulte [extensões de serviço de editor e linguagem](../../extensibility/editor-and-language-service-extensions.md).

## <a name="language-services"></a>Serviços de linguagem
 Se você quiser que o editor do Visual Studio dê suporte a novas palavras-chave de programação ou até mesmo uma nova linguagem de programação, crie um serviço de idioma. Cada serviço de linguagem pode implementar determinados recursos do editor totalmente, parcialmente ou não. Dependendo de como está configurado, o serviço de linguagem pode fornecer realce de sintaxe, correspondência de chaves, suporte a IntelliSense e outros recursos no editor.

 No coração de um serviço de linguagem há um analisador e um scanner. Um scanner (ou analisador léxico) divide um arquivo de origem em elementos que são conhecidos como tokens, e um analisador estabelece as relações entre esses tokens. Ao criar um serviço de idioma, você deve implementar o analisador e o verificador para que o Visual Studio possa entender os tokens e a gramática do idioma. Você pode criar serviços de linguagem gerenciados ou não gerenciados. Para obter mais informações, consulte [extensibilidade de serviço de linguagem herdada](../../extensibility/internals/legacy-language-service-extensibility.md).

## <a name="projects"></a>Projetos

No Visual Studio, os projetos são os contêineres que os desenvolvedores usam para organizar e compilar o código-fonte e outros recursos. Os projetos permitem organizar, compilar, depurar e implantar código-fonte, referências a serviços Web e bancos de dados e outros recursos. O VSPackages pode estender o sistema de projeto do Visual Studio fornecendo tipos de projeto, subtipos de projeto e ferramentas personalizadas.

Os projetos também podem ser coletados juntos em uma *solução*, que é um agrupamento de um ou mais projetos que trabalham juntos para criar um aplicativo. As informações de projeto e status relacionadas à solução são armazenadas em dois arquivos de solução, no arquivo da solução baseada em texto [(. sln)](solution-dot-sln-file.md) e no [arquivo da opção de usuário da solução binária (. suo)](solution-user-options-dot-suo-file.md). Esses arquivos são semelhantes aos arquivos de grupo (. VBG) que foram usados em versões anteriores do Visual Basic, e os arquivos de espaço de trabalho (. DSW) e de opções de usuário (. opt) que foram usados em versões anteriores do C++.

Para obter mais informações, consulte [projetos](../../extensibility/internals/projects.md) e [soluções](../../extensibility/internals/solutions-overview.md).

## <a name="project-and-item-templates"></a>Modelos de item e de projeto
 O Visual Studio inclui modelos de projeto predefinidos e modelos de item de projeto. Você também pode criar seus próprios modelos ou adquirir modelos da Comunidade e, em seguida, integrá-los ao Visual Studio. A [Galeria de códigos do MSDN](https://code.msdn.microsoft.com/site/search?query=visual%20studio) é o local para ir para modelos e extensões.

 Os modelos contêm a estrutura do projeto e os arquivos básicos que são necessários para criar um tipo específico de aplicativo, controle, biblioteca ou classe. Quando você deseja desenvolver um software que se assemelha a um dos modelos, crie um projeto com base no modelo e, em seguida, modifique os arquivos nesse projeto.

> [!NOTE]
> Não há suporte para essa arquitetura de modelo em [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] projetos.

 Para obter mais informações, consulte [adicionando projeto e modelos de item de projeto](../../extensibility/internals/adding-project-and-project-item-templates.md).

## <a name="properties-and-options"></a>Propriedades e opções
 A janela **Propriedades** exibe as propriedades de um ou vários itens selecionados: as páginas de opções de [extensão de propriedades](../../extensibility/internals/extending-properties.md) contêm conjuntos de opções que pertencem a um componente específico, como uma linguagem de programação ou uma VSPackage: [Opções e páginas de opções](../../extensibility/internals/options-and-options-pages.md). As configurações são geralmente recursos relacionados à interface do usuário que podem ser importados e exportados: [suporte para configurações do usuário](../../extensibility/internals/support-for-user-settings.md).

## <a name="visual-studio-services"></a>Serviços do Visual Studio
 Um serviço fornece um conjunto específico de interfaces para os componentes consumirem. O Visual Studio fornece um conjunto de serviços que podem ser usados por qualquer componente, incluindo extensões. Por exemplo, os serviços do Visual Studio permitem que janelas de ferramentas sejam mostradas ou ocultas dinamicamente, habilitam o acesso a eventos de ajuda, barra de status ou interface do usuário. O editor do Visual Studio também fornece serviços que podem ser importados por extensões do editor. Para obter mais informações, consulte [usando e fornecendo serviços](../../extensibility/using-and-providing-services.md).

## <a name="debugger"></a>Depurador
 O depurador é a interface do usuário para os componentes de depuração específicos ao idioma. Se você tiver criado um novo serviço de linguagem, será necessário criar um mecanismo de depuração específico para conectar-se ao depurador. Para obter mais informações, consulte [extensibilidade do depurador do Visual Studio](../../extensibility/debugger/visual-studio-debugger-extensibility.md).

## <a name="source-control"></a>Controle do código-Fonte
 Para obter informações sobre como implementar um plug-in de controle do código-fonte ou VSPackage, consulte [controle do código-fonte](../../extensibility/internals/source-control.md).

## <a name="wizards"></a>Assistentes
 Você pode criar um assistente em conjunto com um novo tipo de projeto, para que o assistente possa ajudar os usuários a tomar as decisões certas quando criarem um novo projeto desse tipo. Para obter mais informações, consulte [assistentes](../../extensibility/internals/wizards.md).

## <a name="custom-tools"></a>Ferramentas personalizadas
 As ferramentas personalizadas permitem associar uma ferramenta a um item em um projeto e executar essa ferramenta sempre que o arquivo é salvo. Para obter mais informações, consulte [ferramentas personalizadas](../../extensibility/internals/custom-tools.md).

## <a name="vssdk-utilities"></a>Utilitários VSSDK
 O VSSDK inclui um conjunto de utilitários que talvez você precise para trabalhar com diferentes aspectos do VSPackages. Para obter mais informações, consulte [utilitários do VSSDK](../../extensibility/internals/vssdk-utilities.md).

## <a name="using-windows-installer"></a>Usando Windows Installer
 Em alguns casos, talvez seja necessário usar o Windows Installer em vez do instalador VSIX: por exemplo, talvez seja necessário gravar no registro. Para obter informações sobre como usar Windows Installer com suas extensões, consulte [instalando o VSPackages com Windows Installer](../../extensibility/internals/installing-vspackages-with-windows-installer.md).

## <a name="help-viewer"></a>Visualizador da Ajuda
 Você pode integrar sua própria ajuda e páginas F1 no Visualizador da ajuda. Para obter mais informações, consulte [Microsoft Help Viewer SDK](../../extensibility/internals/microsoft-help-viewer-sdk.md).
