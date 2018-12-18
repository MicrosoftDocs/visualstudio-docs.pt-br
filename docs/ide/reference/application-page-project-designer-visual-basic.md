---
title: Página Aplicativo das propriedades de projeto do VB
ms.date: 10/30/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesApplicationWPF
- vb.ProjectPropertiesApplication
helpviewer_keywords:
- Project Designer, Application page
- Application page in Project Designer
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 4ceb1612ee678a005cba0be0cfb44337c126cb71
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50670956"
---
# <a name="application-page-project-designer-visual-basic"></a>Página de Aplicativo, Designer de Projeto (Visual Basic)

Use a página **Aplicativo** do Designer de Projeto para especificar as propriedades e configurações de aplicativo de um projeto.

Para acessar a página **Aplicativo**, escolha um nó de projeto (não o nó **Solução**) no **Gerenciador de Soluções**. Em seguida, escolha **Projeto** > **Propriedades** na barra de menus. Quando o **Designer de Projeto** for exibido, selecione a guia **Aplicativo**.

[!INCLUDE[note_settings_general](../../data-tools/includes/note_settings_general_md.md)]

## <a name="general-application-settings"></a>Configurações gerais de aplicativos

As opções a seguir permitem definir as configurações gerais para um aplicativo.

### <a name="assembly-name"></a>Nome do assembly

Especifica o nome do arquivo de saída que conterá o manifesto do assembly. Se você alterar essa propriedade, a propriedade **Nome de Saída** também será alterada.

Também é possível especificar o nome do arquivo de saída em um prompt de comando usando a opção de compilador [entrada/saída (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/out).

Para obter informações sobre como acessar esta propriedade de forma programática, consulte <xref:VSLangProj.ProjectProperties.AssemblyName%2A>.

### <a name="root-namespace"></a>Namespace raiz

Especifica o namespace base para todos os arquivos no projeto. Por exemplo, se você configurasse o **Namespace raiz** para `Project1` e tivesse um `Class1` fora de qualquer namespace em seu código, seu namespace seria `Project1.Class1`. Se você tivesse um `Class2` em um namespace `Order` no código, seu namespace seria `Project1.Order.Class2`.

Se você desmarcar **Namespace raiz**, será possível especificar a estrutura do namespace do seu projeto no código.

> [!NOTE]
> Se você usar a palavra-chave `Global` em uma [Instrução Namespace](/dotnet/visual-basic/language-reference/statements/namespace-statement), será possível definir um namespace fora do namespace raiz do seu projeto. Se você desmarcar a **Namespace raiz**, `Global` se tornará o namespace de nível superior, que acaba com a necessidade da palavra-chave `Global` em uma instrução `Namespace`. Para obter mais informações, consulte "Palavra-chave nas declarações de Namespace global" em [Namespaces no Visual Basic](/dotnet/visual-basic/programming-guide/program-structure/namespaces).

Para obter informações sobre como criar namespaces no seu código, consulte [Instrução Namespace](/dotnet/visual-basic/language-reference/statements/namespace-statement).

Para obter mais informações sobre a propriedade de namespace raiz, consulte [/rootnamespace](/dotnet/visual-basic/reference/command-line-compiler/rootnamespace).

Para obter informações sobre como acessar esta propriedade de forma programática, consulte <xref:VSLangProj.ProjectProperties.RootNamespace%2A>.

### <a name="target-framework-all-configurations"></a>Estrutura de destino (todas as configurações)

Especifica a versão no .NET Framework que o aplicativo direciona. Essa opção pode ter valores diferentes dependendo de quais versões do .NET Framework estão instaladas em seu computador.

O valor padrão corresponde à estrutura de destino especificada na caixa de diálogo **Novo projeto**.

> [!NOTE]
> Os pacotes de pré-requisitos listados na [Caixa de diálogo Pré-requisitos](../../ide/reference/prerequisites-dialog-box.md) são definidos automaticamente quando você abre a caixa de diálogo pela primeira vez. Se você alterar posteriormente a estrutura de destino do projeto, será necessário especificar os pré-requisitos manualmente para corresponder à nova estrutura de destino.

Para obter mais informações, consulte [Como destinar uma versão do .NET Framework](../../ide/how-to-target-a-version-of-the-dotnet-framework.md) e [Visão geral de multiplataforma Visual Studio](../../ide/visual-studio-multi-targeting-overview.md).

### <a name="application-type"></a>Tipo de aplicativo

Especifica o tipo de aplicativo a ser compilado. Os valores são diferentes dependendo do tipo de projeto. Por exemplo, para um projeto do **Aplicativo do Windows Forms**, é possível especificar o **Aplicativo do Windows Forms**, a **Biblioteca de Classes**, o **Aplicativo de Console**, o **Serviço Windows** ou a **Biblioteca de Controles da Web**.

Para um projeto de aplicativo Web, é necessário especificar **Biblioteca de Classes**.

Para obter mais informações sobre a propriedade **Tipo de aplicativo**, consulte [/target (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/target). Para obter informações sobre como acessar essa propriedade de forma programática, consulte <xref:VSLangProj.ProjectProperties.OutputType%2A>.

### <a name="auto-generate-binding-redirects"></a>Gerar redirecionamentos de associação automaticamente

Os redirecionamentos da associação serão adicionados ao seu projeto se o aplicativo ou seus componentes referenciarem mais de uma versão do mesmo assembly. Se você desejar definir manualmente os redirecionamentos de associação no arquivo de projeto, desmarque **Gerar Redirecionamentos de Associação Automaticamente**. Essa caixa de seleção foi introduzida no Visual Studio 2017 versão 15.7.

Para obter mais informações sobre o redirecionamento, confira [Redirecionando versões de assembly](/dotnet/framework/configure-apps/redirect-assembly-versions).

### <a name="startup-form--startup-object--startup-uri"></a>Formulário de inicialização/ objeto de inicialização/ URI de inicialização

Especifica o formulário de inicialização ou ponto de entrada do aplicativo.

Se **Habilitar estrutura de aplicativo** estiver selecionado (o padrão), essa lista será denominada **Formulário de inicialização** e mostrará somente formulários, porque a estrutura de aplicativo dá suporte somente a formulários de inicialização, não objetos.

Se o projeto for um Aplicativo de Navegador do WPF, essa lista será denominada **URI de inicialização** e o padrão será **Page1.xaml**. A lista **URI de inicialização** permite que você especifique o recurso de interface do usuário (um elemento XAML) que o aplicativo exibe quando o ele é iniciado. Para obter mais informações, consulte <xref:System.Windows.Application.StartupUri%2A>.

Se **Habilitar estrutura de aplicativo** estiver desmarcado, essa lista se tornará **Objeto de inicialização** e mostrará os formulários e classes ou módulos com um `Sub Main`.

**Objeto de inicialização** define o ponto de entrada a ser chamado quando o aplicativo é carregado. Geralmente, isso é definido como o principal formulário em seu aplicativo ou como o procedimento `Sub Main` que deve ser executado quando o aplicativo é iniciado. Como as bibliotecas de classe não têm um ponto de entrada, sua única opção para essa propriedade é **(Nenhum)**. Para obter mais informações, consulte [/main](/dotnet/visual-basic/reference/command-line-compiler/main). Para acessar essa propriedade de forma programática, consulte <xref:VSLangProj.ProjectProperties.StartupObject%2A>.

### <a name="icon"></a>Ícone

Define o arquivo .ico que você deseja usar como o ícone do programa. Selecione **\<Procurar.. >** para procurar um gráfico existente. Consulte [-win32icon](/dotnet/visual-basic/reference/command-line-compiler/win32icon) (ou [-win32icon (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/win32icon-compiler-option)) para obter mais informações. Para acessar essa propriedade de forma programática, consulte <xref:VSLangProj.ProjectProperties.ApplicationIcon%2A>.

### <a name="assembly-information"></a>Informações do assembly

Clique neste botão para exibir a [Caixa de diálogo de Informações do Assembly](../../ide/reference/assembly-information-dialog-box.md).

### <a name="enable-application-framework"></a>Habilitar estrutura do aplicativo

Especifica se um projeto usará a estrutura de aplicativo. A configuração dessa opção afeta as opções disponíveis em **Formulário de inicialização**/**Objeto de inicialização**.

Se essa caixa de seleção estiver selecionada, seu aplicativo usará o padrão `Sub Main`. Marcar essa caixa de seleção habilita os recursos na seção **Propriedades da estrutura dos aplicativos do Windows** e também exige que você selecione um formulário de inicialização.

Se essa caixa de seleção estiver desmarcada, seu aplicativo usará o `Sub Main` personalizado que você especificou no **Formulário de inicialização**. Nesse caso, é possível especificar um objeto de inicialização (um `Sub Main` personalizado em um método ou em uma classe) ou um formulário. Além disso, as opções na seção **Propriedades da estrutura dos aplicativos do Windows** ficam indisponíveis.

### <a name="view-windows-settings"></a>Exibir configurações do Windows

Clique neste botão para gerar e abrir o arquivo *app.manifest*. O Visual Studio usa esse arquivo para gerar dados de manifesto do aplicativo. Em seguida, defina o nível de execução solicitado pelo UAC modificando a tag `<requestedExecutionLevel>` no *app.manifest* da seguinte maneira:

`<requestedExecutionLevel level="asInvoker" />`

O ClickOnce funciona com um nível de `asInvoker` ou no modo virtualizado (não há geração de manifesto). Para especificar o modo virtualizado, remova toda a marcação de app.manifest.

Para obter mais informações sobre a geração de manifesto, consulte [Implantação do ClickOnce no Windows Vista](../../deployment/clickonce-deployment-on-windows-vista.md).

## <a name="windows-application-framework-properties"></a>Propriedades da estrutura do aplicativo do Windows

As seguintes configurações estão disponíveis na seção **Propriedades da estrutura dos aplicativos do Windows**. Essas opções estarão disponíveis somente se a caixa de seleção **Habilitar estrutura de aplicativo** estiver selecionada.

> [!TIP]
> A seção depois desta descreve as configurações **Propriedades da estrutura do aplicativos do Windows** específicas para aplicativos WPF (Windows Presentation Foundation).

### <a name="enable-xp-visual-styles"></a>Habilitar estilos visuais do XP

Habilita ou desabilita os estilos visuais do Windows XP, também conhecidos como *Temas do Windows XP*. Os estilos visuais do Windows XP habilitam, por exemplo, controles com cantos arredondados e cores dinâmicas. O padrão é habilitado.

### <a name="make-single-instance-application"></a>Criar um aplicativo de instância única

Marque esta caixa de seleção para impedir que usuários executem várias instâncias do aplicativo. A configuração padrão para essa caixa de seleção é *desmarcada*, o que permite que várias instâncias do aplicativo sejam executadas. Para saber mais, confira o evento <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance>.

### <a name="save-mysettings-on-shutdown"></a>Salvar My.Settings no desligamento

Marque esta caixa de seleção para especificar que as configurações `My.Settings` do aplicativo são salvas quando os usuários desligam seus computadores. A configuração padrão é habilitado. Se essa opção estiver desabilitada, será possível salvar as configurações do aplicativo manualmente chamando `My.Settings.Save`.

### <a name="authentication-mode"></a>Modo de autenticação

Selecione **Windows** (o padrão) para especificar o uso da autenticação do Windows para identificar o usuário conectado no momento. É possível recuperar essas informações no tempo de execução usando o objeto `My.User`. Selecione **Definido pelo aplicativo** se você for fornecer seu próprio código para autenticar usuários em vez de usar os métodos de autenticação padrão do Windows.

### <a name="shutdown-mode"></a>Modo de desligamento

Selecione **Quando o formulário de inicialização fechar** (o padrão) para especificar que o aplicativo saia quando o formulário definido como o formulário de inicialização for fechado, mesmo se outros formulários estiverem abertos. Selecione **Quando o último formulário fechar** para especificar que o aplicativo saia quando o último formulário for fechado ou quando a instrução `My.Application.Exit` ou `End` for chamada explicitamente.

Selecione **No desligamento explícito** para especificar que o aplicativo saia quando você chamar explicitamente `Shutdown`.

Selecione **No fechamento da última janela** para especificar que o aplicativo saia quando a última janela for fechada ou quando você chamar explicitamente `Shutdown`. Essa é a configuração padrão.

Selecione **No fechamento da janela principal** para especificar que o aplicativo saia quando a janela principal for fechada ou quando você chamar explicitamente `Shutdown`.

### <a name="splash-screen"></a>Tela inicial

Selecione o formulário que você deseja usar como uma tela inicial. É necessário ter criado anteriormente uma tela inicial usando um formulário ou modelo. O padrão é **(Nenhum)**.

### <a name="view-application-events"></a>Exibir eventos de aplicativo

Clique neste botão para exibir um arquivo de código de eventos no qual você pode gravar eventos para os eventos de estrutura do aplicativo `Startup`, `Shutdown`, `UnhandledException`, `StartupNextInstance` e `NetworkAvailabilityChanged`. Também é possível substituir determinados métodos de estrutura do aplicativo. Por exemplo, é possível alterar o comportamento de exibição da tela inicial substituindo `OnInitialize`.

## <a name="windows-application-framework-properties-for-windows-presentation-foundation-wpf-apps"></a>Propriedades de estrutura do aplicativo do Windows para aplicativos WPF (Windows Presentation Foundation)

As seguintes configurações estarão disponíveis na seção **Propriedades da estrutura do aplicativo do Windows** quando o projeto for um aplicativo WPF (Windows Presentation Foundation). Essas opções estarão disponíveis somente se a caixa de seleção **Habilitar estrutura de aplicativo** estiver selecionada. As opções listadas nesta tabela estão disponíveis somente para aplicativos WPF ou aplicativos de navegador WPF. Elas não estão disponíveis para bibliotecas de controle de usuário ou de controle personalizado WPF.

### <a name="shutdown-mode"></a>Modo de desligamento

Esta propriedade é aplicável somente a aplicativos WPF (Windows Presentation Foundation).

Selecione **No desligamento explícito** para especificar que o aplicativo saia quando você chamar explicitamente <xref:System.Windows.Application.Shutdown%2A>.

Selecione **No fechamento da última janela** para especificar que o aplicativo saia quando a última janela for fechada ou quando você chamar explicitamente <xref:System.Windows.Application.Shutdown%2A>. Essa é a configuração padrão.

Selecione **No fechamento da janela principal** para especificar que o aplicativo saia quando a janela principal for fechada ou quando você chamar explicitamente <xref:System.Windows.Application.Shutdown%2A>.

Para obter mais informações sobre como usar essa configuração, consulte <xref:System.Windows.Application.Shutdown%2A>

### <a name="edit-xaml"></a>Editar XAML

Este botão abre o arquivo de definição de aplicativo (Application.xaml) no editor XAML. Quando você clicar neste botão, *Application.xaml* será aberto no nó de definição de aplicativo. Talvez seja necessário editar esse arquivo para executar determinadas tarefas, como a definição de recursos. Se o arquivo de definição de aplicativo não existir, o Designer de Projeto criará um.

### <a name="view-application-events"></a>Exibir eventos de aplicativo

Este botão abre o arquivo de classe `Application` (*Application.xaml.vb*) em um editor de código. Se o arquivo não existir, o Designer de Projeto criará um com o namespace e o nome de classe apropriado.

O objeto <xref:System.Windows.Application> gera eventos quando ocorrem determinadas alterações no estado do aplicativo (por exemplo, na inicialização ou no desligamento do aplicativo). Para obter uma lista completa dos eventos que essa classe expõe, consulte <xref:System.Windows.Application>. Esses eventos são manipulados na seção de código do usuário da classe parcial `Application`.