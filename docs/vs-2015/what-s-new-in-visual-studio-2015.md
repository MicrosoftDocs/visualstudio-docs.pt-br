---
title: O que&#39;novo no Visual Studio 2015 | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.StartPage.WhatsNew
helpviewer_keywords:
- Visual Studio, what's new
- what's new [Visual Studio]
ms.assetid: 7307e180-ba28-4774-8a43-cbb980085a71
caps.latest.revision: 364
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: ab9d2536b3f92b62233a2ae05b79a722696136e4
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51000252"
---
# <a name="what39s-new-in-visual-studio-2015"></a>O que&#39;novo no Visual Studio 2015
[!INCLUDE[vs2017banner](./includes/vs2017banner.md)]

Bem-vindo ao Visual Studio 2015, um conjunto integrado de ferramentas de produtividade do desenvolvedor, serviços de nuvem e extensões que permitem que você e sua equipe criem ótimos aplicativos e jogos para a web, para a Windows Store, para a área de trabalho, para o Android e para iOS.

Esta página destaca alguns dos recursos mais importantes que são novos desde o Visual Studio 2013 RTM, incluindo recursos que foram introduzidos pela primeira vez em uma das atualizações do Visual Studio 2013. Para obter uma lista completa das novidades no Visual Studio 2015, consulte o [notas de versão](https://www.visualstudio.com/news/vs2015-vs).

Para obter mais informações sobre os vários aprimoramentos e novos recursos no Visual Studio ALM, consulte [o que há de novo para TFS 2015](/tfs/server/whats-new?view=vsts#tfs-2015-rtm).

## <a name="a-new-setup-experience"></a>Uma nova experiência de instalação
 [!INCLUDE[downloadvs](./includes/downloadvs-md.md)]

 A experiência de instalação do Visual Studio 2015 tem foi dividida em componentes para que você só precisará instalar as partes que você precisa. Isso torna a instalação mais rápida para muitos cenários comuns que envolvem o desenvolvimento de .NET ou da Web. Se você fazer outros tipos de desenvolvimento, como desenvolvimento móvel de plataforma cruzada, ou você pode trabalhar em C++ ou F#, escolha **personalizada** instalação e, em seguida, escolha os componentes e SDKs de terceiros opcionais que você precisa. Você também pode instalar qualquer um dos componentes personalizados mais tarde. Por exemplo, se você escolher a instalação básica e, em seguida, tenta criar um novo projeto de C++, você precisará baixar as ferramentas de desenvolvimento do C++.

 ![Diálogo de instalação do Visual Studio 2015](./ide/media/vs2015-setup-screen.png "VS2015_Setup_screen")

## <a name="sign-in-across-multiple-accounts"></a>Entrar através de várias contas
 Com o Visual Studio 2015, a nova entrada experiência simplificada é projetada para simplificar bastante o acesso aos recursos online, mesmo quando você tiver várias contas do Visual Studio. Depois que você entrar no Visual Studio, você está automaticamente conectado para todas as instâncias do Visual Studio 2015 e no Blend em seu computador. Entrar automaticamente inicia o roaming de suas configurações para você. No Visual Studio 2015, sua conta é compartilhada entre recursos dessa forma, desde que você tiver um token de BOM, você pode acessar suas contas do Visual Studio Team Services da **Team Explorer**, recursos e sites do Microsoft Azure assinatura no Gerenciador de servidores. Você também verá os recursos do Azure na caixa de diálogo Novo projeto para projetos do Application Insights, e você verá seu móveis do Azure, armazenamento do Azure, [do Microsoft Office 365](http://msdn.microsoft.com/office/aa905340.aspx) e [Saleforce.com desenvolvedor](https://developer.salesforce.com/) contas no novo **adicionar um serviço conectado** caixa de diálogo.

 Você pode trabalhar com várias contas de usuário no Visual Studio, adicionando-os conforme o uso ou por meio do novo Gerenciador de conta. Em seguida, você pode alternar entre essas contas em rapidamente ao se conectar a serviços ou acessar os recursos online. Visual Studio se lembrará de contas que você adicionar, portanto, você pode usá-los de qualquer instância do Visual Studio ou Blend. Visual Studio também se movimentarão a lista de contas (embora nós não criamos suas credenciais valiosas) com sua conta de personalização para que possa começar rapidamente a trabalhar com uma dessas contas em outro dispositivo. Obviamente, você pode remover as contas na caixa de diálogo Configurações de conta a qualquer momento. Para começar, consulte [trabalhar com várias contas de usuário](./ide/work-with-multiple-user-accounts.md).

 ![Gerenciador de Conta](./ide/media/vs2015-accountmanager.gif "VS2015_AccountManager")

## <a name="choose-your-target-platforms"></a>Escolha sua plataforma de destino (s)
 Visual Studio 2015 oferece suporte ao desenvolvimento de dispositivo móvel de plataforma cruzada. Você pode escrever aplicativos e jogos que se destinam a iOS, Android e Windows e compartilham um código comum base, tudo a partir de dentro do IDE do Visual Studio. Você verá todos esses novos tipos de projeto no arquivo, caixa de diálogo Novo projeto.

 E, claro — suporte para aplicativos da área de trabalho clássicos é melhor do que nunca, com muitos aprimoramentos para linguagens, bibliotecas e ferramentas.

### <a name="cross-platform-mobile-apps-in-c-with-xamarin-for-visual-studio"></a>Aplicativos móveis de plataforma cruzada em c# com Xamarin para Visual Studio
 Xamarin é uma estrutura móvel que permite que você escreva código em c# que associa de forma nativa para iOS e Android APIs. Microsoft iniciou uma parceria em conjunto com o Xamarin em sua versão do Xamarin para Visual Studio, uma extensão que habilita você a desenvolver para iOS, Android e Windows Phone em uma única solução com código compartilhado. Com o Xamarin, você usará um idioma e uma base de código com deltas mínimo entre as plataformas.  Xamarin para Visual Studio tem suporte no Visual Studio 2010 e posterior. A edição de inicial do Xamarin está incluída no Visual Studio 2015. Para começar, consulte [compilar aplicativos com interface do usuário nativa usando Xamarin no Visual Studio](./cross-platform/build-apps-with-native-ui-using-xamarin-in-visual-studio.md).

### <a name="cross-platform-mobile-apps-in-htmljavascript-with-apache-cordova"></a>Aplicativos móveis de plataforma cruzada em HTML/JavaScript com o Apache Cordova
 Ferramentas do Visual Studio para Apache Cordova é o resultado de uma estreita colaboração entre a Microsoft e de código aberto da comunidade do Apache Cordova. As ferramentas permitem o desenvolvimento móvel de plataforma cruzada usando HTML, CSS e JavaScript (ou Typescript). Você pode direcionar o iOS, Android e Windows com uma única base de código e aproveite a riqueza do IDE do Visual Studio incluindo IntelliSense do JavaScript, o Explorador do DOM, Console do JavaScript, os pontos de interrupção, inspeções, locais, apenas meu código e muito mais.  Com o Visual Studio Tools para Apache Cordova, seus aplicativos têm acesso aos recursos nativos do dispositivo em todas as plataformas por meio do plug-ins que fornecem uma API comum em JavaScript. Para começar, consulte [Introdução ao Visual Studio Tools for Apache Cordova](http://msdn.microsoft.com/library/db446f2c-6ba4-4c76-aac5-4c66f43b8c42).

### <a name="cross-platform-mobile-games-in-c-with-unity"></a>Jogos móveis de plataforma cruzada em c# com o Unity
 Unity é uma plataforma amplamente usado para desenvolvimento de jogos 2D e 3D multiplataforma. Você pode escrever seu jogo em c# e executá-lo de modo nativo no Android, iOS, Windows Phone e muitas outras plataformas. Ferramentas do Visual Studio para Unity é uma extensão que se integra a Unity com o IDE do Visual Studio. Com essa extensão, você obtém todos os recursos do IDE do Visual Studio e o depurador, além dos recursos de produtividade que são projetados para desenvolvedores do Unity. Ferramentas do Visual Studio para Unity 2.0 Preview 2 adiciona suporte para Visual Studio 2015, além disso a um número de novos recursos, como uma melhor visualização para objetos em locais e inspeção windows. A Microsoft adquiriu recentemente SyntaxTree, os criadores do Visual Studio Tools for Unity. Para baixar as ferramentas do Visual Studio para Unity 2.0 Preview 2 e para obter mais informações sobre ferramentas do Visual Studio para Unity, consulte [Visual Studio Tools for Unity 2.0](http://Aka.ms/vstu).

### <a name="cross-platform-apps-and-libraries-for-native-c"></a>Aplicativos de plataforma cruzada e bibliotecas para C++ nativo
 C++ é um idioma disponível nativamente pela maioria dos dispositivos móveis. Você pode usá-lo a escrever código de plataforma cruzada compartilhado bibliotecas que pode ser criados para vários destinos de plataforma móvel. Você pode até criar aplicativos móveis todo em C++. Visual C++ fornece as ferramentas para editar, compilar, implantar e depurar seu código de plataforma cruzada. Além dos modelos para aplicativos do Windows, você pode criar projetos de modelos para aplicativos de atividade nativa do Android, aplicativos iOS ou projetos de biblioteca de código compartilhado para várias plataformas que incluem aplicativos híbridos de Xamarin. IntelliSense específico da plataforma permite que você explorar APIs e gerar códigos corretos para destinos de Android, iOS ou Windows. Você pode configurar sua compilação para plataformas x86 ou ARM nativas e, em seguida, implantar seu código em um simulador de iOS ou em dispositivos iOS no Mac conectado à rede, em dispositivos Android diretamente conectados ou usar o emulador do Microsoft Visual Studio de alto desempenho para o Android para teste. Você pode definir pontos de interrupção, inspecione variáveis, exibir a pilha e percorrer o código C++ no depurador do Visual Studio. Você pode compartilhar tudo, exceto o código mais específicos da plataforma em várias plataformas de aplicativo e criar para eles, tudo isso com uma solução no Visual Studio.

 Para começar a usar em C++ de plataforma cruzada, consulte [criar aplicativos móveis de plataforma cruzada com o Visual C++](./misc/build-cross-platform-mobile-apps-with-visual-cpp.md)

### <a name="universal-windows-apps-for-any-windows-10-device"></a>Aplicativos universais do Windows para qualquer dispositivo Windows 10
 Com a Plataforma Universal do Windows e nosso único núcleo do Windows, é possível executar o mesmo aplicativo em qualquer dispositivo Windows 10, de telefones a áreas de trabalho. Crie esses aplicativos Universais do Windows com o Visual Studio 2015 e as ferramentas de Desenvolvimento de Aplicativos Universais do Windows.

 ![Plataforma Universal do Windows](./cross-platform/media/uwp-coreextensions.png "UWP_CoreExtensions")

 Execute seu aplicativo em um telefone Windows 10, área de trabalho do Windows 10 ou Xbox. É o mesmo pacote do aplicativo! Com a introdução do núcleo único e unificado do Windows 10, um pacote do aplicativo pode ser executado em todas as plataformas. Várias plataformas têm SDKs de Extensão que podem ser adicionados ao aplicativo para aproveitar comportamentos específicos à plataforma. Por exemplo, o SDK de uma extensão para dispositivos móveis manipula o botão Voltar pressionado em um Windows Phone. Se você referenciar um SDK de Extensão em seu projeto, basta adicionar verificações em tempo de execução para testar se esse SDK está disponível nessa plataforma. É assim que você pode ter o mesmo pacote do aplicativo para cada plataforma!

 Use c#, Visual Basic, C++ ou JavaScript para criar essas [aplicativos Windows Universal](http://msdn.microsoft.com/library/dn975273.aspx).

### <a name="web"></a>Web
 O ASP.NET 5 é uma atualização importante para MVC, WebAPI e SignalR e é executado no Windows, Mac e Linux.  O ASP.NET 5 foi projetado desde o backup para fornecer a que você com um .NET enxuta e combinável de pilha para a criação de aplicativos modernos baseados em nuvem. As ferramentas do Visual Studio 2015 está mais estreitamente integrada com ferramentas de desenvolvimento da web populares, como o Bower e o Grunt. Para começar, consulte as várias postagens de blog sobre o [NET Web Development and Tools Blog](http://blogs.msdn.com/b/webdev/).

### <a name="classic-desktop-and-windows-store"></a>Área de trabalho clássica e a Windows Store
 Visual Studio 2015 continua a dar suporte à área de trabalho clássica e desenvolvimento da Windows Store. Conforme a evolução do Windows, o Visual Studio evoluirá junto com ele.  No Visual Studio 2015, as bibliotecas e linguagens para .NET, bem como o C++ fez avanços significativos que se aplicam a todas as versões do Windows.

#### <a name="the-net-framework"></a>O .NET Framework
 A Microsoft [!INCLUDE[net_v46](./includes/net-v46-md.md)] oferece aproximadamente 150 novas APIs e 50 atualizados APIs para permitir mais cenários. Por exemplo, agora implementam mais coleções <xref:System.Collections.Generic.IReadOnlyCollection%601> tornando-os mais fáceis de usar. Além disso, o ASP.NET 5, mencionado anteriormente, oferece uma plataforma enxuta do .NET para criar aplicativos modernos baseados em nuvem.

 Aplicativos Windows Store escritos em c# que direcionam o .NET Framework agora podem tirar proveito do .NET Native, que compila aplicativos para código nativo em vez de IL, e [!INCLUDE[net_v46](./includes/net-v46-md.md)] também adiciona o RyuJIT, um compilador just-in-(JIT) de 64 bits.

 Os novos compiladores c# e VB ("Roslyn") significativamente acelerar os tempos de compilação e fornecem APIs de análise de código abrangente. Visual Studio 2015 tira proveito do Roslyn para fornecer mais refatorações, incluindo embutido renomear, analisadores e correções rápidas.

 As linguagens c# e Visual Basic contêm muitas melhorias bastante na linguagem principal e no suporte ao IDE. Esses aprimoramentos que todos sejam acumulados para tornar sua experiência ainda mais intuitiva, conveniente e produtiva de codificação do .NET.

 Para obter mais informações, consulte [What's New](http://msdn.microsoft.com/library/1d971dd7-10fc-4692-8dac-30ca308fc0fa) e o [Blog .NET](http://blogs.msdn.com/b/dotnet/).

#### <a name="c"></a>C++
 O Visual C++ fornece avanços significativos no C + + 11/14 conformidade com a linguagem, suporte para desenvolvimento de dispositivo móvel de plataforma cruzada, suportam para funções retomáveis e await (atualmente planejados para padronização em c++17), aprimoramentos e correções no C Implementações de biblioteca padrão (STL) biblioteca de tempo de execução (CRT) e C++, as caixas de diálogo redimensionáveis no MFC, novas otimizações de compilador, compile melhor desempenho, novos recursos de diagnóstico e novas ferramentas de produtividade no editor de códigos.

 Para obter mais informações, consulte [o que há de novo para o Visual C++](http://msdn.microsoft.com/library/1cc09fad-85a2-43c2-b022-bb99f5fe0ad7) e o [Blog do Visual C++](http://blogs.msdn.com/b/vcblog/).

## <a name="device-preview-menu-bar"></a>Barra de menus de visualização do dispositivo
 Em projetos de plataforma Universal do Windows, a barra de menus de visualização de dispositivo permite que você veja como a interface do usuário baseada em XAML será renderizado em vários tamanhos de tela.

 ![Menu de visualização de dispositivo](./ide/media/vs2015-device-preview.png "vs2015_device_preview")

## <a name="visual-studio-graphics-diagnostics"></a>Diagnóstico de gráficos do Visual Studio
 Desde o Visual Studio 2013, Visual Studio Graphics diagnóstico adicionou muitos recursos novos, incluindo análise de quadro, suporte do Windows Phone, edição de sombreador e aplica e a linha de comando capturam ferramentas. Ele também adicionou suporte para depuração de aplicativos DirectX12. Para obter mais informações, consulte [diagnóstico de gráficos do Visual Studio](./debugger/visual-studio-graphics-diagnostics.md).

## <a name="connect-to-services"></a>Conectar-se aos serviços
 Visual Studio 2015 torna mais fácil do que nunca conectar seu aplicativo aos serviços.  O Assistente para adicionar serviço conectado configura seu projeto, adiciona o suporte a autenticação necessária e baixa os pacotes NuGet necessários para você começar a codificar seu serviço rapidamente e sem complicações. O assistente Adicionar serviço conectado também se integra com o novo gerente de conta para torná-lo mais fácil trabalhar com várias contas de usuário e assinaturas. No Visual Studio 2015, o suporte para os serviços a seguir é fornecido fora da caixa (supondo que você tenha uma conta):

1. Serviços móveis do Azure

2. Armazenamento do Azure

3. Office 365 (email, contatos, calendários, arquivos, usuários e grupos)

4. A equipe de vendas

   Novos serviços serão adicionados de forma contínua e você pode descobrir aquelas clicando no "localizar novos serviços link" no assistente.

   ![Adicionar caixa de diálogo Serviços conectados](./ide/media/vs2015-addconnectedservicedialog.png "VS2015_AddConnectedServiceDialog")

## <a name="design-your-ui"></a>Projetar a interface do usuário
 A experiência do Blend para criar interfaces do usuário XAML foi aprimorada significativamente. Blend foi completamente remodelado para fornecer uma interface do usuário mais intuitiva, mais poderosos recursos de edição de XAML incluindo IntelliSense e uma melhor integração com o Visual Studio. Para obter mais informações, consulte [projetar XAML no Visual Studio e no Blend para Visual Studio](./designers/designing-xaml-in-visual-studio.md).

## <a name="cross-platform-debugging-support"></a>Suporte à depuração de plataforma cruzada
 Você pode usar o Visual Studio para criar e depurar aplicativos móveis nativos que são executados em dispositivos Android, iOS e Windows. Use o [emulador do Visual Studio para Android](http://blogs.msdn.com/b/visualstudioalm/archive/2014/11/12/introducing-visual-studio-s-emulator-for-android.aspx), ou conectar um dispositivo e depurar seu código diretamente no Visual Studio.

-   **JavaScript / Cordova**. Use o [Visual Studio Tools for Apache Cordova](http://msdn.microsoft.com/library/dn879821\(v=vs.140\).aspx) para criar aplicativos nativos para Windows, iOS e Android com o JavaScript.

     [Depurar seu aplicativo](http://msdn.microsoft.com/library/c2a4a1d4-a4e8-47ec-811f-ad207c54f4d1) na biblioteca do MSDN é uma visão detalhada de suporte para Cordova de depuração do Visual Studio.

-   **C# / Xamarin**. Use [Xamarin](http://msdn.microsoft.com/library/dn879698\(v=vs.140\).aspx) para criar aplicativos nativos para Windows, iOS e Android no Visual Studio com c#.

     [Depurando](http://developer.xamarin.com/guides/ios/deployment,_testing,_and_metrics/debugging_in_xamarin_ios/) (iOS) e [depurar no dispositivo](http://developer.xamarin.com/guides/android/deployment,_testing,_and_metrics/debugging_with_xamarin_android/) no [guias do desenvolvedor Xamarin](http://developer.xamarin.com/guides) descrevem a experiência de depuração.

-   **C++ / Android**. Use o [Visual C++ para desenvolvimento móvel de plataforma cruzada](http://msdnstage.redmond.corp.microsoft.com/library/dn872463\(v=vs.140\).aspx) modelos junto com as ferramentas de terceiros, como o [NDK do Android](https://developer.android.com/tools/sdk/ndk/index.html) para criar aplicativos nativos para Windows e Android.

## <a name="debugging-and-diagnostics"></a>Depuração e Diagnóstico
 Para obter informações sobre o que há de novo na depuração, consulte [o que há de novo no depurador no Visual Studio 2015](./debugger/what’s-new-for-the-debugger-in-visual-studio-2015.md).

 Para obter informações sobre o que há de novo no diagnóstico, consulte [o que há de novo nas ferramentas de criação de perfil](./profiling/what-s-new-in-profiling-tools.md).

 A seguir é nova ou aprimorados ferramentas que executam diferentes tipos de diagnóstico e análise em seu código:

### <a name="perftips"></a>PerfTips
 As PerfTips exibem o tempo de execução dos métodos durante a depuração, permitindo que você identifique rapidamente os gargalos sem ter que invocar o criador de perfil. Para começar, consulte [PerfTips: informações de desempenho em geral durante a depuração com o Visual Studio](http://blogs.msdn.com/b/visualstudioalm/archive/2014/08/18/perftips-performance-information-at-a-glance-while-debugging-with-visual-studio.aspx)

### <a name="error-list"></a>Lista de Erros
 A lista de erros agora dá suporte à filtragem em qualquer coluna. Ele também mostra uma exibição ao vivo de erros, avisos e análise de código em toda a solução c# ou Visual Basic conforme você digita, mesmo quando uma alteração de código produz milhares de avisos. A nova lista de erros é compatível com o back com o uso existente. Para obter mais informações, consulte [janela lista de erros](./ide/reference/error-list-window.md).

### <a name="gpu-usage-tool"></a>Ferramenta de uso GPU
 A ferramenta de uso de GPU ajuda você a coletar e analisar dados de uso GPU em jogos e aplicativos de DirectX e solucionar problemas se provenientes de gargalos de desempenho na CPU ou GPU. Para se familiarizar com a ferramenta, consulte o [postagem de blog de equipe do Visual C++](http://blogs.msdn.com/b/vcblog/archive/2014/09/05/gpu-usage-tool-in-visual-studio-2013-update-4-ctp1.aspx).

## <a name="live-code-analysis-light-bulbs"></a>Análise de código dinâmica (lâmpadas)
 O novo compilador Roslyn para c# e Visual Basic não só fornece tempos de compilação — também possibilita completamente novos cenários, como análise de código dinâmica, que fornecem a rico e personalizável comentários e sugestões diretamente dentro do editor de código conforme você digita. No Visual Studio 2015, as lâmpadas exibido na margem esquerda (ao usar o teclado) ou uma dica de ferramenta (quando passar o mouse sobre um erro com o mouse). A lâmpada informa em tempo real que o compilador (possivelmente usando um conjunto de regras personalizado) detectou um problema em seu código e também tem uma sugestão para corrigir o problema. Quando você vir uma lâmpada, clique para obter sugestões acionáveis.

 ![No Editor de código do Visual Studio as lâmpadas](./ide/media/vs2015-lightbulbs.png "VS2015_LightBulbs")

## <a name="enjoy-these-additional-ide-improvements"></a>Aproveite esses aprimoramentos adicionais do IDE

### <a name="synchronized-settings-roaming-settings"></a>Configurações sincronizadas (configurações de Roaming)
 Visual Studio 2013 apresentou configurações sincronizadas para algumas das configurações mais comumente configuradas como o Editor de texto, associações de teclas, tema & fontes e cores, inicialização e Aliases de ambiente.  Visual Studio 2015 aprimora essa experiência por sincronizar mais de suas configurações e sincronizar as configurações de toda a família do Visual Studio de aplicativos, como Professional, Enterprise, SKUs de Express e Blend. Quando você entra no Visual Studio 2015 pela primeira vez com a mesma conta que você tenha usado no Visual Studio 2013, você verá as configurações sincronizadas aplicadas do Visual Studio 2013. Você pode acessar as configurações, digitando "sincronização" em **início rápido**, ou navegar para **Ferramentas > Opções > ambiente > configurações sincronizadas**.

### <a name="automatic-extension-updates"></a>Atualizações automáticas de extensão
 As extensões do Visual Studio instaladas agora serão automaticamente atualizadas quando uma nova versão está disponível na Galeria do Visual Studio. Ver [Localizando e usando extensões do Visual Studio](./ide/finding-and-using-visual-studio-extensions.md) para obter detalhes sobre como você pode personalizar as atualizações automáticas de extensão.

### <a name="title-case-menus"></a>Menus de maiusculas de título
 Você falou, nós escutamos. Menus do Visual Studio são mais uma vez capitalização de título por padrão. No entanto, se você, como o estilo todas em maiusculas, você pode configurá-lo no início ou nos **Ferramentas > Opções > geral** página de propriedades:

 ![Comandos de Menu das Main caso do Visual Studio 2015 título](./ide/media/vs2015-mainmenu.png "VS2015_MainMenu")

### <a name="high-resolution-images-and-touch-support"></a>Imagens de alta resolução e suporte a toque
 O IDE do Visual Studio agora tem imagens de alta resolução true em telas mais densos (em áreas como menus, menus de contexto, barras de comando de janela de ferramentas e em alguns projetos no Gerenciador de soluções). E, em uma tela sensível ao toque na janela do editor de código do Visual Studio, você pode usar gestos de agora, como toque e segure a tecla, aperte, toque e assim por diante para aplicar zoom, role, selecione o texto e invocar menus de contexto.

 ![Suporte no editor de toque](./ide/media/vs2015-touchsupport.png "VS2015_TouchSupport")

### <a name="custom-layouts"></a>Layouts personalizados
 Você pode criar o repositório e roaming layouts de janela personalizados. Por exemplo, você pode definir um layout preferido para uso em seu computador desktop e um layout diferente para uso em um laptop ou dispositivo de tela pequena. Ou talvez você prefira um layout para um projeto de interface do usuário e outro para um projeto de banco de dados. Associações de teclas permitem alternar rapidamente entre layouts. Esses layouts estão disponíveis em qualquer instância do Visual Studio quando você está conectado. Para obter mais informações, consulte [criar layouts de janela personalizados](./misc/create-custom-window-layouts.md).

 ![Item de menu do Visual Studio Custom Layout](./ide/media/vs2015-customlayout.png "VS2015_CustomLayout")

### <a name="notification-hub"></a>Hub de notificação
 A interface do usuário para o hub de notificação foi otimizada para torná-lo mais fácil verificar rapidamente. Tipos de notificações adicionais foram adicionados incluindo problemas de desempenho, problemas de renderização e falhas, e você agora pode informar ao Visual Studio pare de mostrar uma notificação. Para obter mais informações, consulte [Notificações do Visual Studio](./ide/visual-studio-notifications.md).

### <a name="codelens-find-what-happened-to-your-code-enterprise-and-professional-editions-only"></a>CodeLens: Localizar o que aconteceu com seu código (apenas para edições Enterprise e Professional)
 Mantenha o foco no trabalho enquanto você encontrar informações sobre seu código – sem sair do editor. Você pode revisar as alterações e outro histórico de itens de trabalho, bugs, revisões de código, e assim por diante para o código que é armazenado no Visual Studio Team Services (VSTS) ou no Team Foundation Server (TFS).

 No Visual Studio Enterprise e Professional do Visual Studio, agora você pode:

- Obter histórico para um arquivo de código completo no editor do Visual Studio.

   ![CodeLens: obtenha detalhes do arquivo de código](./ide/media/codelensfilelevel.png "CodeLensFileLevel")

- Ver um gráfico que mostra quem alterou seu código. Isso pode ajudá-lo a encontrar padrões nas alterações da sua equipe e avaliar o impacto delas.

   ![CodeLens: ver o histórico de alterações do código como um grafo](./ide/media/codelens.png "CodeLens")

- Ver facilmente quando o seu código foi alterado pela última vez.

- Localize alterações em outras ramificações que afetam o seu código.

  Ver [CodeLens](./ide/find-code-changes-and-other-history-with-codelens.md).

### <a name="design-and-modeling-tools-enterprise-edition-only"></a>Design e modelagem de ferramentas (apenas Enterprise edition)
 **Gráficos de dependência e mapas de código**

 No Visual Studio Enterprise, quando você quiser entender dependências específicas em seu código, exiba-os Criando mapas de código. Em seguida, você pode navegar essas relações usando o mapa, que aparece ao lado de seu código. Mapas de código também podem ajudar a manter o controle de seu local no código enquanto você trabalha ou depura código, portanto, você lerá menos códigos enquanto aprende mais sobre o design do seu código.

 Nesta versão, fizemos os menus de atalho para elementos de código e links muito mais fácil de usar, agrupando comandos em seções relacionadas ao selecionar, edição, gerenciamento de grupos e alterando o layout do conteúdo do grupo. Observe também que os projetos de teste são exibidos em um estilo diferente de outros projetos e que atualizamos os ícones de elementos no mapa para versões mais adequadas.

 ![Mostrar itens selecionados em um novo mapa de códigos](./ide/media/codemapsshowonnewmap.png "CodeMapsShowOnNewMap")

 Outros aprimoramentos incluem:

- **Diagramas de cima para baixo melhorados**. Para médias e grandes soluções do Visual Studio, agora você pode usar um menu de arquitetura simplificado para obter um código mais útil mapas para sua solução. Os assemblies da sua solução são agrupados pelas pastas de solução, para que você possa vê-los no contexto e aproveitar o esforço feito para estruturar a solução. Você verá imediatamente projeto e referências de assembly e, em seguida, os tipos de link que aparecem. Além disso, os assemblies externos à solução são agrupados de forma mais compacta.

- **Projetos de teste têm estilo diferente e podem ser filtrados**. Você pode agora mais fácil e rapidamente identificar os projetos de teste no mapa porque eles têm estilos diferentes. Eles também podem ser filtrados para que você possa se concentrar no código de trabalho do aplicativo.

- **Links de dependência externa de simplificado**. Links de dependência não mais representam a herança de System. Object, System. ValueType, System. Enum e System. Delegate, que facilita ver dependências externas no mapa de códigos.

- **'Drill-in into dependency links' leva os filtros em consideração**. Você obtém um diagrama simples e útil quando expande para compreender as contribuições para um link de dependência. O diagrama é menos desorganizado e leva em consideração as opções que você selecionou de filtragem de link.

- **Elementos de código são adicionados a um mapa de código com seus contexto**. Como os diagramas agora aparecem com contexto (até assembly e solução de pasta que você pode filtrar as se necessário), que você conseguir diagramas mais eficientes ao arrastar e soltar elementos de código do Gerenciador de soluções, o modo de exibição de classe, o Pesquisador de objetos; ou, quando selecionar elementos no Gerenciador de soluções e selecionando mostram no mapa de códigos.

- **Obtenha mapas de código reativos mais rapidamente**. Arrastar e soltar operações produzem um resultado imediato, e os links entre os nós são criados com muito mais rapidamente, sem afetar as operações posteriores iniciadas pelo usuário, como expandir um nó ou solicitar mais nós. Quando você cria mapas de código sem compilar a solução, todos os casos de canto, como quando os assemblies não são compilados — agora são processados.

- **Ignorar a recompilação de sua solução.** Fornece um melhor desempenho durante a criação e edição de diagramas.

- **Filtrar nós de elemento de código e grupos**. Você organizar rapidamente seus mapas ao exibir ou ocultar elementos de código com base em sua categoria, bem como pelo agrupamento de elementos de código por pastas de solução, assemblies, namespaces, pastas de projeto e tipos.

- **Filtre relações para tornar os diagramas mais fáceis de ler**. Filtragem de link agora também se aplica para cruzar os links de grupo, o que torna o trabalho com a janela de filtros menos intrusivo que do que era nas versões anteriores.

- **Criar diagramas da exibição de classe e Pesquisador de objetos**. Arraste e solte arquivos e assemblies em um novo ou um mapa existente do windows de modo de exibição de classe e Pesquisador de objetos.

  Ver [mapear as dependências nas soluções](./modeling/map-dependencies-across-your-solutions.md).

  **Outras alterações de design e modelagem nesta versão:**

- **Diagramas de camada**. Atualize esses diagramas usando o modo de exibição de classe e Pesquisador de objetos. Para atender aos requisitos de design de software, use diagramas de camada para descrever as dependências desejadas para seu software. Mantenha o código consistente com esse design, localizando o código que não atende a essas restrições e validando códigos futuros com essa linha de base.

- **Diagramas de UML**. Você não pode mais criar diagramas de classe UML e diagramas de sequência do código. Mas você ainda criar esses diagramas usando novos elementos UML.

- **Gerenciador de arquitetura**. Não há mais você pode usar o Architecture Explorer para criar diagramas. Mas você ainda pode usar o Gerenciador de soluções.

## <a name="visual-studio-extensibility-tools"></a>Ferramentas de extensibilidade do Visual Studio
 Nunca foi mais fácil de instalar as ferramentas de extensibilidade de Visual Studio (SDK do VS e modelos), como agora estão incluídas como um componente opcional durante a instalação.  As ferramentas de extensibilidade permite aos desenvolvedores criar extensões para personalizar e adicionar recursos ao Visual Studio. Para obter mais informações sobre a extensibilidade do Visual Studio, consulte [SDK do Visual Studio](./extensibility/visual-studio-sdk.md)

 Se você deseja incluir as ferramentas de extensibilidade com sua instalação personalizada, você pode encontrá-los em **recursos / ferramentas comuns / ferramentas de extensibilidade do Visual Studio**.  Você também pode instalar as ferramentas de extensibilidade mais tarde abrindo o **novo projeto** caixa de diálogo e selecionando o **instalar ferramentas do Visual Studio Extensibility** item sob **Visual C# / Extensibilidade**.

## <a name="please-give-feedback"></a>Envie comentários
 Por que enviar comentários à equipe do Visual Studio? Porque nós levamos a sério os comentários dos clientes. Na verdade, vamos examinar cada parte dos comentários que entram em nosso sistema de comentários. Seus comentários orienta muito do que fazemos.

### <a name="send-a-smile"></a>Enviar um Smiley
 Nos dizendo que você como nos ajuda a entender quando podemos atender ou exceder suas expectativas. Quando estamos Projetando e implementando novos recursos, podemos usar dados sobre os recursos que você gosta de ajudar com nossas decisões de design. Portanto, se você gosta de um recurso no Visual Studio, conte-nos sobre ele. É fácil e você pode fazer isso diretamente de dentro do IDE.

 Basta clicar no Smiley amarelo na barra de título, conte-no que você gostou, em seguida, clique no **enviar um Smiley** botão.

 E pronto! Podemos irá rotear seus comentários à equipe correta onde eles pat em si na parte de trás e começar a pensar em maneiras de encantá-lo ainda mais rapidamente.

### <a name="send-a-frown"></a>Enviar um rosto triste
 Ouvir em que precisamos fazer melhorias no produto nos ajuda a gerenciar nossa lista de pendências, concentrando-se pela primeira vez em que as coisas mais importantes para nossos clientes. Se houver algo que é bugging você, conte-nos sobre ele usando o **enviar um rosto triste** de recursos do diretamente dentro do IDE. Fizemos isso um processo muito simples demais:

 Clique no Smiley amarelo na barra de título, clique **enviar um rosto triste**. Conte-no que você não gostou, em seguida, clique em enviar um rosto triste botão. Para obter mais informações, consulte [Fale conosco](./ide/talk-to-us.md).

### <a name="report-crashes-hangs-and-performance-issues"></a>Relatar falhas, travamentos e problemas de desempenho
 Às vezes, uma anotação rápida em um rosto triste simplesmente não é suficiente para transmitir o impacto total de algo que você não gosta. Para os horários quando você tiver um problema de desempenho, falha ou travamento, você pode compartilhar facilmente etapas de reprodução, os despejos de memória e arquivos de rastreamento usando a caixa de diálogo é exibida depois que você envia um rosto triste.

 Primeiro, envie um rosto triste, conforme descrito acima. Na caixa de diálogo pop-up, você pode marcar seus comentários com qualquer uma das marcas padrão ou criar sua própria marca. Marcas nos ajudam a encaminhar seus comentários para a equipe de recursos apropriado. No **escolher uma categoria** lista suspensa, selecione a opção que representa o problema que você está relatando, siga as etapas para reproduzir o problema. Etapas detalhadas sobre como usar o Visual Studio para fornecer comentários também estão disponíveis. Para obter mais informações, consulte [Visual Studio enviar um Smiley instruções](http://msdn.microsoft.com/library/5cc9b67a-54d0-41b0-aa8f-80dff4475a6b).

## <a name="see-also"></a>Consulte também
* [Crie aplicativos de plataforma cruzada com o Apache Cordova](http://msdn.microsoft.com/library/34d3c1be-22b3-4812-97fb-10b4e8ad2134)
* [Criar aplicativos com interface do usuário nativa usando o Xamarin no Visual Studio](./cross-platform/build-apps-with-native-ui-using-xamarin-in-visual-studio.md)
* [Compilar aplicativos de plataforma cruzada com o Visual C++](./misc/build-cross-platform-mobile-apps-with-visual-cpp.md)
* [Gerar testes de unidade para seu código com IntelliTest](./test/generate-unit-tests-for-your-code-with-intellitest.md)
* [Trabalhar com várias contas de usuário](./ide/work-with-multiple-user-accounts.md)
* [Criar layouts de janela personalizados](./misc/create-custom-window-layouts.md)
* [Realizar ações rápidas com lâmpadas](./ide/perform-quick-actions-with-light-bulbs.md)
* [Novidades no Visual Studio 2017](/visualstudio/ide/how-to-report-a-problem-with-visual-studio-2017)