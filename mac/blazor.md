---
title: Criar Blazor aplicativos Web
description: Fornece informações sobre o Blazor suporte em aplicativos ASP.NET Core no Visual Studio para Mac.
author: jongalloway
ms.author: jogallow
ms.date: 12/17/2019
ms.technology: vs-ide-general
ms.assetid: D2717D3A-9225-40A8-8155-7D0143B2CA60
no-loc:
- Blazor
- Blazor WebAssembly
ms.topic: how-to
ms.openlocfilehash: 86a8c35d2a379d6afbbe6cf55f53346223e7c462
ms.sourcegitcommit: 5e82a428795749c594f71300ab03a935dc1d523b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2020
ms.locfileid: "86211596"
---
# <a name="create-blazor-web-apps"></a>Criar Blazor aplicativos Web

Este guia oferece uma introdução à criação do seu primeiro Blazor aplicativo Web. Para obter diretrizes mais detalhadas, consulte [introdução ao ASP.NET Core Blazor ](/aspnet/core/blazor/index).

ASP.NET Core Blazor dá suporte a duas opções de hospedagem diferentes; Blazor Servidor e Blazor WebAssembly . O Visual Studio para Mac dá suporte a ambos os modelos de hospedagem. O Visual Studio para Mac 8.4 + dá suporte ao Blazor servidor e Visual Studio para Mac 8.6 + dá suporte a ambos. Para obter mais informações sobre Blazor modelos de hospedagem, consulte [ASP.NET Core modelos de Blazor hospedagem ](https://docs.microsoft.com/aspnet/core/blazor/hosting-models?view=aspnetcore-3.1). O suporte para depuração de Blazor WebAssembly projetos no Visual Studio para Mac será lançado em uma versão posterior a 8,6.

O que é Blazor ? Blazoré uma estrutura para a criação de interface do usuário da Web interativa do lado do cliente com o .NET, que oferece as seguintes vantagens para os desenvolvedores da Web:

* escreva o código em C# em vez de JavaScript.
* Aproveite o ecossistema .NET existente das bibliotecas .NET.
* Compartilhe a lógica de aplicativo entre o servidor e o cliente.
* Beneficie-se do. Desempenho, confiabilidade e segurança da rede.
* Mantenha-se produtivo com o Visual Studio em PC, Linux e macOS.
* Crie um conjunto comum de linguagens, estruturas e ferramentas que são estáveis, com recursos avançados e fáceis de usar.

## <a name="creating-a-new-blazor-server-project"></a>Criando um novo Blazor projeto de servidor

1. Na **janela iniciar**, selecione **novo** para criar um novo projeto:

   ![Visual Studio para Mac janela inicial com a nova seleção realçada](media/blazor-new-project.png)
1. Na caixa de diálogo **novo projeto** , selecione aplicativo do **.NET Core** > **App** > ** Blazor servidor** de aplicativos .NET Core e selecione **Avançar**: ![ escolha um modelo para a caixa de diálogo novo projeto com o Blazor modelo de aplicativo do servidor selecionado](media/blazor-project-template.png)

1. Selecione .NET Core 3,1 como a estrutura de destino e, em seguida, selecione **Avançar**. 
   ![Configurar a Blazor caixa de diálogo novo aplicativo de servidor exibida com a estrutura de destino selecionada para o .NET Core 3,1](media/blazor-select-target-framework.png)

1. Escolha um nome para seu projeto e adicione o suporte do git, se desejado. Selecione **Criar** para criar o cluster.
   ![BConfigure a Blazor caixa de diálogo novo aplicativo do servidor exibida ao inserir o nome do projeto](media/blazor-name-project.png)

   Visual Studio para Mac abre seu projeto na janela de layout de código.
1. Selecione **executar**  >  **Iniciar sem depuração** para executar o aplicativo.

   O Visual Studio inicia o [Kestrel](/aspnet/core/fundamentals/servers/kestrel), abre um navegador para `https://localhost:5001` e exibe seu Blazor aplicativo Web.

   ![Blazoraplicativo Web no Safari](media/blazor-new-app-in-edge.png)

## <a name="blazor-support-in-visual-studio-for-mac"></a>Blazorsuporte no Visual Studio para Mac

Visual Studio para Mac (a partir da versão 8,4) inclui novos recursos para ajudá-lo a criar novos Blazor projetos de servidor. Além de isso, ele fornece o suporte padrão que você esperaria, como compilar, executar e depurar Blazor projetos. No Visual Studio para Mac suporte 8,6 para criação, compilação e execução de Blazor WebAssembly projetos foi adicionado.

No passo a passos acima, vimos como o Blazor modelo de projeto de aplicativo de servidor ajuda você a criar um novo Blazor projeto de aplicativo de servidor. Vamos dar uma olhada em alguns dos recursos adicionais do Visual Studio para Mac para dar suporte ao Blazor desenvolvimento de projetos.

### <a name="editor-support-for-razor-files"></a>Suporte do editor para arquivos *. Razor*
O Visual Studio para Mac inclui suporte para edição de arquivos. Razor-maioria dos arquivos que você usará ao criar Blazor aplicativos. A versão do Windows e Mac do IDE compartilham o mesmo editor para arquivos. Razor. Você verá a colorização completa e o suporte de conclusão para seus arquivos. Razor, incluindo as conclusões dos componentes do Razor declarados no projeto.

![Janela do editor de Visual Studio para Mac mostrando o IntelliSense paraBlazor](media/blazor-intellisense.png)

### <a name="publishing-blazor-applications-to-azure-app-service"></a>Publicando Blazor aplicativos no serviço Azure app
Você também pode publicar Blazor aplicativos diretamente no serviço Azure app. Se você não tiver uma conta do Azure para executar seu Blazor aplicativo no Azure, você sempre poderá [se inscrever para obter uma aqui gratuita](https://azure.microsoft.com/free) que também vem de 12 meses de serviços populares gratuitos, $200 créditos gratuitos do Azure e mais de 25 serviços sempre gratuitos.

![Visual Studio para Mac mostrando a experiência de publicação do Azure](media/blazor-azure-publish.png)

## <a name="project-anatomy"></a>Anatomia do projeto

Blazoros aplicativos Web incluem alguns diretórios e arquivos por padrão. Como você está começando, aqui estão os principais que você precisará estar familiarizados com:

### <a name="pages-folder"></a>Pasta Páginas

Esta pasta contém as páginas da Web de um projeto, que usam uma extensão de arquivo *. Razor* .

### <a name="shared-folder"></a>Pasta compartilhada

Essa pasta inclui componentes compartilhados, também usando a extensão *. Razor* . Você verá que isso inclui o *MainLayout. Razor*, que é usado para definir o layout comum em todo o aplicativo. Ele também inclui o componente *NavMenu. Razor* compartilhado, que é usado em todas as páginas. Se você estiver criando componentes reutilizáveis, eles irão para a pasta **compartilhada** .

### <a name="app-settings"></a>Configurações de aplicativo

O *appSettings.jsno* arquivo contém dados de configuração, como cadeias de conexão.

Para obter mais informações sobre a configuração, consulte a [configuração no guia do ASP.net](/aspnet/core/fundamentals/configuration/index).

### <a name="wwwroot-folder"></a>Pasta wwwroot

Essa pasta contém arquivos estáticos, como HTML, JavaScript e arquivos CSS. Saiba mais em [Arquivos estáticos no ASP.NET Core](/aspnet/core/fundamentals/static-files).

### <a name="programcs"></a>Module.vb

Esse arquivo contém o ponto de entrada para o programa. Saiba mais em [Host da Web do ASP.NET Core](/aspnet/core/fundamentals/host/web-host).

### <a name="startupcs"></a>Startup.cs

Esse arquivo contém um código que configura o comportamento do aplicativo, como se o aplicativo requer consentimento para cookies. Saiba mais em [Inicialização de aplicativos no ASP.NET Core](/aspnet/core/fundamentals/startup).

## <a name="summary"></a>Resumo
Neste tutorial, você viu como criar um novo Blazor aplicativo de servidor no Visual Studio para Mac e aprendeu sobre alguns dos recursos que Visual Studio para Mac oferece para ajudá-lo a criar Blazor aplicativos.

## <a name="see-also"></a>Confira também

Para obter um guia mais abrangente para a criação de Blazor aplicativos Web, consulte [introdução ao ASP.NET Core Blazor ](/aspnet/core/blazor/index).
