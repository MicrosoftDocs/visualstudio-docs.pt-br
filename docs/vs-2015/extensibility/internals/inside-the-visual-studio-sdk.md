---
title: Dentro do SDK do Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- roadmap, Visual Studio integration SDK
- Visual Studio integration SDK roadmap
- integration roadmap, Visual Studio SDK
ms.assetid: 9118eaa4-0453-4dc5-9e16-c7062d254869
caps.latest.revision: 31
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: b7a7642d8cd33d53bb7d6d2a472a0690713e25d3
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51795824"
---
# <a name="inside-the-visual-studio-sdk"></a>Por dentro do SDK do Visual Studio
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Esta seção fornece informações detalhadas sobre as extensões do Visual Studio, incluindo a arquitetura do Visual Studio, componentes, serviços, esquemas, utilitários e assim por diante.  
  
## <a name="extensibility-architecture"></a>Arquitetura de extensibilidade  
 A ilustração a seguir mostra a arquitetura de extensibilidade do Visual Studio. Os VSPackages fornece funcionalidade de aplicativo, que é compartilhada entre o IDE como serviços. O IDE padrão também oferece uma ampla gama de serviços, tais como <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>, que fornecem acesso à funcionalidade de janelas do IDE.  
  
 ![Gráfico de arquitetura do ambiente](../../extensibility/internals/media/environment.gif "ambiente")  
Modo de exibição generalizado da arquitetura do Visual Studio  
  
## <a name="vspackages"></a>VSPackages  
 Os VSPackages são módulos de software que formam e estendem o Visual Studio com elementos da interface do usuário, serviços, projetos, editores e designers. Os VSPackages são a unidade de arquitetura central do Visual Studio. Para obter mais informações, consulte [VSPackages](../../extensibility/internals/vspackages.md).  
  
## <a name="visual-studio-shell"></a>Shell do Visual Studio  
 Shell do Visual Studio fornece a funcionalidade básica e dar suporte a comunicação cruzada entre suas extensões de componente VSPackages e MEF. Para obter mais informações, consulte [Shell do Visual Studio](../../extensibility/internals/visual-studio-shell.md).  
  
## <a name="user-experience-guidelines"></a>Diretrizes da Experiência do Usuário  
 Se você estiver planejando criar novos recursos para o Visual Studio, você deve dar uma olhada nestas diretrizes para obter dicas de design e a usabilidade: [diretrizes de experiência de usuário do Visual Studio](../../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md).  
  
## <a name="commands"></a>Comandos  
 Comandos são funções que realizam tarefas, como imprimir um documento, a atualização de uma exibição ou criando um novo arquivo.  
  
 Quando você estende o Visual Studio, você pode criar comandos e registrá-los com o shell do Visual Studio. Você pode especificar como esses comandos aparecerá no IDE, por exemplo, em um menu ou barra de ferramentas. Normalmente um comando personalizado é exibido na **ferramentas** menu e um comando para exibir uma janela de ferramenta seriam exibido na **Other Windows** submenu a **exibição** menu.  
  
 Quando você cria um comando, você também deve criar um manipulador de eventos para ele. O manipulador de eventos determina quando o comando está visível ou habilitada, permite que você modifique seu texto e garante que o comando responde adequadamente quando ele é ativado. Na maioria dos casos, o IDE manipula os comandos usando o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface. Comandos no Visual Studio são tratados, começando com o contexto do comando interno, com base na seleção de local e continuando para o contexto mais externo, com base na seleção global. Comandos adicionados ao menu principal estão imediatamente disponíveis para execução de scripts.  
  
 Para obter mais informações, consulte [comandos, Menus e barras de ferramentas](../../extensibility/internals/commands-menus-and-toolbars.md).  
  
## <a name="menus-and-toolbars"></a>Menus e barras de ferramentas  
 Menus e barras de ferramentas fornecem uma maneira para que os usuários invocar comandos. Menus são linhas ou colunas de comandos que normalmente são exibidos como itens individuais de texto na parte superior de uma janela de ferramentas. Submenus são menus secundários que aparecem quando um usuário clica em comandos que incluem uma pequena seta. Menus de contexto exibido quando um usuário clica determinados elementos de interface do usuário. Alguns nomes de menu comuns são **arquivo**, **editar**, **exibição**, e **janela**. Para obter mais informações, consulte [estendendo Menus e comandos](../../extensibility/extending-menus-and-commands.md).  
  
 Barras de ferramentas são linhas ou colunas de botões e outros controles, como caixas de combinação, caixas de listagem e caixas de texto. Botões da barra de ferramentas normalmente têm imagens de ícone, como um ícone de pasta para um **abrir arquivo** comando ou uma impressora para um **impressão** comando. Todos os elementos de barra de ferramentas são associados a comandos. Quando você clica em um botão de barra de ferramentas, o comando associado é executado. No caso de um controle de lista suspensa, cada item na lista suspensa é associado um comando diferente. Alguns controles de barra de ferramentas, como um controle de splitter são híbridas. Um dos lados do controle é um botão de barra de ferramentas e o outro lado é uma seta para baixo que exibe vários comandos quando ele for clicado.  
  
## <a name="tool-windows"></a>Ferramenta Windows  
 Janelas de ferramentas são usadas no IDE para exibir informações. **Caixa de ferramentas**, **Gerenciador de soluções**, **as propriedades** janela, e **navegador da Web** são exemplos de janelas de ferramentas.  
  
 Normalmente, as janelas de ferramentas oferecem vários controles com a qual o usuário pode interagir. Por exemplo, o **propriedades** janela permite que o usuário defina as propriedades de objetos que têm um propósito específico. O **propriedades** janela é especializada nesse sentido, mas também geral porque ele pode ser usado em muitas situações diferentes. Da mesma forma, o **saída** é especializada em janela porque ele fornece uma saída com base em texto, mas geral porque muitos subsistemas no Visual Studio podem usá-lo para fornecer saída para o usuário do Visual Studio.  
  
 Considere a imagem a seguir do Visual Studio, que contém várias janelas de ferramentas.  
  
 ![Captura de tela](../../extensibility/internals/media/t1gui.png "T1gui")  
  
 Algumas das janelas de ferramentas estão encaixadas juntas em um único painel que exibe a janela de ferramenta do Gerenciador de soluções e oculta as outras janelas de ferramentas, mas torna-os disponíveis clicando nas guias. A figura mostra duas outras janelas de ferramentas, o **lista de erros** e **saída** janela, encaixada juntas em um único painel.  
  
 Também mostrado é o painel do documento principal, que mostra as várias janelas do editor. Embora as janelas de ferramentas normalmente têm uma única instância (por exemplo, você pode abrir somente um **Gerenciador de soluções**), janelas do editor podem ter várias instâncias, cada um deles é usada para editar um documento separado, mas todos os quais ferramentas estão encaixados em o mesmo painel. A figura mostra um painel de documento que tem duas janelas do editor, uma janela de designer de formulário e uma janela do navegador que mostra a página de início. Todas as janelas no painel do documento estão disponíveis clicando nas guias, mas a janela do editor que contém o arquivo EditorPane.cs está visível e Active Directory.  
  
 Quando você estende o Visual Studio, você pode criar ferramenta janelas que permitem que os usuários do Visual Studio interagir com sua extensão. Você também pode criar seus próprios editores que permitem que os usuários do Visual Studio editar documentos. Como seus editores e janelas de ferramenta serão integrados ao Visual Studio, você não precisa programá-los para encaixar ou exibidos corretamente em uma guia. Quando eles são registrados corretamente no Visual Studio, eles terão automaticamente os recursos típicos de janelas de ferramentas e janelas de documentos no Visual Studio. Para obter mais informações, consulte [estendendo e personalizando ferramenta Windows](../../extensibility/extending-and-customizing-tool-windows.md).  
  
## <a name="document-windows"></a>Janelas de documento  
 Uma janela de documento é uma janela com moldura filho de uma janela de interface de documentos múltiplos (MDI). Janelas de documento normalmente são usadas para hospedar os editores de texto, editores de formulários (também conhecido como designers) ou controles de edição, mas eles também podem hospedar outros tipos de funcionais. O **novo arquivo** caixa de diálogo inclui exemplos de janelas de documento que o Visual Studio fornece.  
  
 A maioria dos editores são específicas para uma linguagem de programação ou para um tipo de arquivo, como páginas HTML, conjuntos de quadros, arquivos de C++ ou arquivos de cabeçalho. Selecionando um modelo na **novo arquivo** caixa de diálogo, um usuário cria dinamicamente uma janela de documento para o editor para o tipo de arquivo que está associado com o modelo. Uma janela de documento também é criada quando um usuário abre um arquivo existente.  
  
 Janelas de documento são restritas para a área de cliente do MDI. Cada janela de documento tem uma guia na parte superior e ordem de guia está vinculada a outras janelas que podem ser abertas na área de MDI. Clicando duas vezes na guia de uma janela de documento exibe um menu de atalho que inclui opções para dividir a área MDI em vários grupos de guia horizontal ou vertical. Dividir a área MDI permite que vários arquivos sejam exibidos ao mesmo tempo. Para obter mais informações, consulte [documento Windows](../../extensibility/internals/document-windows.md).  
  
## <a name="editors"></a>Editores  
 Editor do Visual Studio permite que você personalizá-lo e usá-lo para seu próprio tipo de conteúdo por meio do MEF Managed Extensibility Framework (). Em muitos casos você não precisará criar um VSPackage para estender o editor, embora se você quiser incluir recursos do shell (por exemplo, um comando de menu ou uma tecla de atalho), você pode combinar uma extensão do MEF com um VSPackage.  
  
 Você também pode criar um editor personalizado, por exemplo, se você quiser ler e gravar em um banco de dados, ou se você quiser usar um designer. Você também pode usar um editor externo, como o bloco de notas ou o Microsoft WordPad. Para obter mais informações, consulte [Editor e extensões do serviço de linguagem](../../extensibility/editor-and-language-service-extensions.md).  
  
## <a name="language-services"></a>Serviços de linguagem  
 Se você quiser que o editor do Visual Studio para dar suporte à programação novas palavras-chave ou até mesmo uma nova linguagem de programação, você pode criar um serviço de linguagem. Cada serviço de linguagem pode implementar determinados recursos do editor totalmente, parcialmente ou nada. Dependendo de como estiver configurado, o serviço de linguagem pode fornecer realce de sintaxe, correspondência de chaves, suporte ao IntelliSense e outros recursos no editor.  
  
 No coração de um serviço de linguagem são um analisador e um scanner. Um scanner (ou analisador léxico) divide um arquivo de origem em elementos que são conhecidos como tokens e um analisador estabelece as relações entre esses tokens. Quando você cria um serviço de linguagem, você deve implementar o analisador e o scanner para que o Visual Studio possa entender os tokens e a gramática da linguagem. Você pode criar serviços de linguagem gerenciada ou não gerenciado. Para obter mais informações, consulte [extensibilidade de serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-extensibility.md).  
  
## <a name="projects"></a>Projetos  
 No Visual Studio, os projetos são contêineres usados pelos desenvolvedores para organizar e compilar o código-fonte e outros recursos. Projetos permitem organizar, compilar, depurar e implantar o código-fonte, as referências a serviços Web e bancos de dados e outros recursos. Os VSPackages pode estender o sistema de projeto do Visual Studio, fornecendo ferramentas personalizadas, subtipos do projeto e tipos de projeto.  
  
 Projetos também podem ser reunidos em uma solução, que é um agrupamento de um ou mais projetos que trabalham juntos para criar um aplicativo. Projeto e informações de status que pertencem à solução são armazenadas em dois arquivos de solução, o arquivo de solução com base em texto (. sln) e o arquivo de opção (. suo) de usuário de solução de binário. Esses arquivos são semelhantes aos arquivos de grupo (. vbg) que foram usados nas versões anteriores do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], e o espaço de trabalho (dsw) e o usuário opções de arquivos (. opt) que foram usados nas versões anteriores do [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)].  
  
 Para obter mais informações, consulte [projetos](../../extensibility/internals/projects.md) e [soluções](../../extensibility/internals/solutions.md).  
  
## <a name="project-and-item-templates"></a>Modelos de item e de projeto  
 Visual Studio inclui modelos de projeto predefinidos e modelos de item de projeto. Você pode também tornar seus próprios modelos ou adquirir modelos da comunidade e, em seguida, integrá-las ao Visual Studio. O [MSDN Code Gallery](http://code.msdn.microsoft.com/Project/ProjectDirectory.aspx?ProjectSearchText=visual%20studio) é o lugar ideal para os modelos e extensões.  
  
 Modelos contêm a estrutura de projeto e os arquivos básicos que são necessários para compilar um determinado tipo de aplicativo, controle, biblioteca ou classe. Quando você deseja desenvolver um software que se parece com um dos modelos, criar um projeto com base no modelo e, em seguida, modifique os arquivos no projeto.  
  
> [!NOTE]
>  Não há suporte para essa arquitetura de modelo para [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] projetos. Para obter informações sobre como criar [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] modelos de projeto, consulte [Projetando um assistente](http://msdn.microsoft.com/library/a7c0be7e-9297-4fed-83e3-5645c896d56b).  
  
 Para obter mais informações, consulte [adicionando projeto e modelos de Item de projeto](../../extensibility/internals/adding-project-and-project-item-templates.md).  
  
## <a name="properties-and-options"></a>Propriedades e opções  
 O **propriedades** janela exibe as propriedades de um único ou vários itens selecionados: [estendendo propriedades](../../extensibility/internals/extending-properties.md) páginas de opções contêm conjuntos de opções que pertencem a um componente específico, como um programação da linguagem ou um VSPackage: [opções e páginas de opções](../../extensibility/internals/options-and-options-pages.md). As configurações são recursos geralmente relacionados à interface do usuário que podem ser importados e exportados: [suporte para configurações de usuário](../../extensibility/internals/support-for-user-settings.md).  
  
## <a name="visual-studio-services"></a>Serviços do Visual Studio  
 Um serviço fornece um conjunto específico de interfaces de componentes consumir. Visual Studio fornece um conjunto de serviços que podem ser usados por todos os componentes, incluindo as extensões. Por exemplo, serviços do Visual Studio permitem que janelas de ferramenta a ser mostrado ou oculto dinamicamente, habilitar o acesso à Ajuda, barra de status ou eventos de interface do usuário. Editor do Visual Studio também fornece serviços que podem ser importados por extensões de editor. Para obter mais informações, consulte [Using e fornecendo serviços](../../extensibility/using-and-providing-services.md).  
  
## <a name="debugger"></a>Depurador  
 O depurador é a interface do usuário para os componentes de depuração específicas de idioma. Se você tiver criado um novo serviço de linguagem, você precisará criar um mecanismo de depuração específicas para conectar-se no depurador do. Para obter mais informações, consulte [extensibilidade do depurador do Visual Studio](../../extensibility/debugger/visual-studio-debugger-extensibility.md).  
  
## <a name="source-control"></a>Controle do código-Fonte  
 Para obter informações sobre como implementar um plug-in de controle do código-fonte ou VSPackage, consulte [controle de origem](../../extensibility/internals/source-control.md).  
  
## <a name="wizards"></a>Assistentes  
 Você pode criar um assistente em conjunto com um novo tipo de projeto, para que o assistente pode ajudar os usuários tomam as decisões certas ao criar um novo projeto desse tipo. Para obter mais informações, consulte [assistentes](../../extensibility/internals/wizards.md).  
  
## <a name="custom-tools"></a>Ferramentas personalizadas  
 Ferramentas personalizadas permitem que você associe uma ferramenta de um item em um projeto e executar essa ferramenta, sempre que o arquivo é salvo. Para obter mais informações, consulte [ferramentas personalizados](../../extensibility/internals/custom-tools.md).  
  
## <a name="vssdk-utilities"></a>Utilitários VSSDK  
 VSSDK inclui um conjunto de utilitários que podem ser necessários para trabalhar com diferentes aspectos de VSPackages. Para obter mais informações, consulte [utilitários VSSDK](../../extensibility/internals/vssdk-utilities.md).  
  
## <a name="using-windows-installer"></a>Usando o Windows Installer  
 Em alguns casos, você talvez precise usar o instalador do Windows em vez do instalador do VSIX: por exemplo, talvez você precise escrever no registro. Para obter informações sobre como usar o Windows Installer com suas extensões, consulte [instalando VSPackages com o Windows Installer](../../extensibility/internals/installing-vspackages-with-windows-installer.md).  
  
## <a name="help-viewer"></a>Visualizador da Ajuda  
 Você pode integrar seu próprio de Ajuda e páginas de F1 do Visualizador da Ajuda. Para obter mais informações, consulte [SDK do Microsoft Help Viewer](../../extensibility/internals/microsoft-help-viewer-sdk.md).

