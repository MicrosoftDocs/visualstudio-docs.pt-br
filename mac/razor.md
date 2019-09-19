---
title: Criar aplicativos Web Razor
description: Fornece informações sobre o suporte do Razor em aplicativos ASP.NET Core no Visual Studio para Mac.
author: sayedihashimi
ms.author: sayedha
ms.date: 05/03/2018
ms.technology: vs-ide-general
ms.assetid: F898CB6E-05ED-44CD-8DB6-427B2592CCC6
ms.openlocfilehash: 964b949d20d63a4564615fef0e719b85ae41762d
ms.sourcegitcommit: 53bc4c11b82882ab658e34c65ae374060f823531
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71128375"
---
# <a name="create-razor-web-apps"></a>Criar aplicativos Web Razor

Este guia oferece uma introdução à criação de seu primeiro aplicativo Web Razor. Para obter diretrizes mais detalhadas, consulte [introdução ao Razor pages no ASP.NET Core](https://docs.microsoft.com/aspnet/core/razor-pages/index).

O Visual Studio para Mac oferece suporte à edição de Razor, inclusive IntelliSense e realce de sintaxe em arquivos *.cshtml*.

![Edição de Razor no Visual Studio para Mac](media/razor-editor.png)

## <a name="creating-a-new-razor-project"></a>Como criar um novo projeto do Razor

1. Na tela de boas-vindas, selecione **novo** para criar um novo projeto:

     ![Novo projeto do Visual Studio para Mac](media/razor-new.png)

1. Na caixa de diálogo **novo projeto** , vá para**aplicativo Web** do**aplicativo** >  **.NET Core** > e selecione **Avançar**:

     ![Modelo de projeto do Razor](media/razor-new-project1.png)

1. Selecione a estrutura de destino do .NET Core (recomendamos a versão 2,2 ou posterior) e, em seguida, selecione **Avançar**. Escolha um nome para seu projeto e adicione o suporte do git, se necessário. Selecione **criar** para criar o projeto.

     ![Nome do projeto do Razor](media/razor-new-project2.png)

   Visual Studio para Mac abre seu projeto na janela de layout de código.

1. Execute o projeto sem depuração usando **Command + Option + F5**.

   O Visual Studio inicia o [Kestrel](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel), abre um `https://localhost:5001`navegador para e exibe seu primeiro aplicativo Web Razor.

   ![Aplicativo Web do Razor no Safari](media/razor-webapp.png)

## <a name="project-anatomy"></a>Anatomia do projeto

Os aplicativos Web do Razor incluem os componentes a seguir.

### <a name="pages-folder"></a>Pasta Páginas

Esta pasta contém as páginas da Web de um projeto, juntamente com o code-behind para cada uma:
* Um arquivo * *.cshtml* para a marcação HTML e sintaxe Razor.
* Um arquivo * *.cshtml.cs* para seu code-behind C# para manipular eventos de página.

Arquivos de suporte têm nomes que começam com um sublinhado. Por exemplo, o arquivo _Layout.cshtml configura os elementos de interface do usuário comuns a todas as páginas. Esse arquivo configura o menu de navegação na parte superior da página e o aviso de direitos autorais na parte inferior. Saiba mais em [Layout no ASP.NET Core](https://docs.microsoft.com/aspnet/core/mvc/views/layout).

### <a name="launch-settings"></a>Configurações de inicialização

O arquivo *launchSettings. JSON* contém as configurações do IIS, a URL do aplicativo e outras configurações relacionadas.

### <a name="app-settings"></a>Configurações do aplicativo

O arquivo *appSettings. JSON* contém dados de configuração, como cadeias de conexão.

Para obter mais informações sobre a configuração, consulte a [configuração no guia do ASP.net](https://docs.microsoft.com/aspnet/core/fundamentals/configuration/index).

### <a name="wwwroot-folder"></a>Pasta wwwroot

Essa pasta contém arquivos estáticos, como HTML, JavaScript e arquivos CSS. Saiba mais em [Arquivos estáticos no ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/static-files).

### <a name="programcs"></a>Module.vb

Esse arquivo contém o ponto de entrada para o programa. Saiba mais em [Host da Web do ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/host/web-host).

### <a name="startupcs"></a>Startup.cs

Esse arquivo contém um código que configura o comportamento do aplicativo, como se o aplicativo requer consentimento para cookies. Saiba mais em [Inicialização de aplicativos no ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/startup).

## <a name="see-also"></a>Consulte também

Para obter um guia mais abrangente para a criação de aplicativos Web do Razor, consulte [Introduction to Razor pages in ASP.NET Core](https://docs.microsoft.com/aspnet/core/razor-pages/index).
