---
title: Introdução do Visual Studio para Mac
description: Este artigo apresenta os recursos do Visual Studio para Mac
author: conceptdev
ms.author: crdun
ms.date: 11/03/2018
ms.assetid: 3A130EC1-DD8C-4125-9034-B08D7AF7EA65
ms.openlocfilehash: 10b27c26fcef622687b64f225dd04ae966f43cd5
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895672"
---
# <a name="introducing-visual-studio-for-mac"></a>Introdução do Visual Studio para Mac

O Visual Studio para Mac é um IDE moderno e sofisticado com muitos recursos para criar aplicativos Web, da área de trabalho e móveis. Ele é compatível com os seguintes tipos de desenvolvimento:

* Móvel com .NET: Android, iOS, tvOS, watchOS
* Aplicativos da área de trabalho Mac
* Aplicativos .NET Core
* Aplicativos Web ASP.NET Core
* Jogos Unity de plataforma cruzada

Inclui funcionalidades como um editor avançado, depuração, integração de plataforma nativa com iOS, Mac e Android e controle do código-fonte integrado.

Este artigo apresenta uma pesquisa de várias seções do Visual Studio para Mac e recursos que o tornam uma ferramenta avançada para criar aplicativos multiplataforma.

> [!TIP]
> A versão prévia do Visual Studio 2019 para Mac agora está disponível para teste. Siga estas [instruções de instalação](install-preview.md) e confira o [tour do IDE](ide-tour.md).

## <a name="installation"></a>Instalação

Siga as etapas no guia de [Instalação](install-preview.md) para baixar e instalar o Visual Studio para Mac.

## <a name="language-support"></a>Suporte a linguagens

O Visual Studio para Mac dá suporte ao desenvolvimento em C# e F#, por padrão.

### <a name="c"></a>C#

C# é a linguagem mais usada para criar aplicativos multiplataforma no Visual Studio para Mac. O IDE tem suporte total para todos os recursos de C# 7.

### <a name="f"></a>F#

F# é uma linguagem de programação funcional fortemente tipada projetada para execução no .NET. Está disponível como uma linguagem de programação para usuários do Visual Studio para Mac no Android, no Mac e no iOS. Para obter mais informações sobre como usar F# e exibir amostras criadas na linguagem, acesse os guias de [F#](https://developer.xamarin.com/guides/cross-platform/fsharp/).

## <a name="platform-support"></a>Suporte de plataforma

## <a name="net-core"></a>.NET Core

O [.NET Core](https://www.microsoft.com/net/core#macos) é uma plataforma para criar aplicativos executados no Windows, Linux e Mac. O Visual Studio para Mac tem suporte para carregar, criar, executar e depurar projetos do .NET Core. 

Para executar projetos do .NET Core, o SDK do .NET Core deve ser baixado e instalado.

O suporte do .NET Core inclui:

* IntelliSense de C# e F#.
* Modelos de projeto do .NET Core para aplicativos da Web, de biblioteca e de console.
* Suporte total à depuração, incluindo pontos de interrupção, pilha de chamadas, janela de inspeção, etc.
* Restauração com base em MSBuild e NuGet PackageReferences.
* Suporte integrado a teste de unidade para executar e depurar testes com a Plataforma de Testes do Visual Studio incluída no SDK do .NET Core.
* Migração do formato antigo project.json.

Para começar, confira o [laboratório prático](https://github.com/Microsoft/vs4mac-labs/tree/master/Web/Getting-Started) dos aplicativos Web ASP.NET Core.

## <a name="xamarin"></a>Xamarin

O suporte de primeira classe para o [Xamarin](https://developer.xamarin.com/) permite que você desenvolva experiências nativas avançadas para Android, macOS, iOS, tvOS e watchOS. Os aplicativos de plataforma cruzada Xamarin.Forms o ajudam a compartilhar o código de interface do usuário baseado em XAML entre macOS, iOS e Android sem limitar o acesso à funcionalidade nativa.

Para começar, confira o [laboratório prático](https://github.com/Microsoft/vs4mac-labs/tree/master/Mobile/Getting-Started) dos aplicativos móveis.

### <a name="android"></a>Android

O Visual Studio tem seu próprio gerenciador de SDK do Android integrado.

Para aplicativos Android, o Visual Studio para Mac inclui seu próprio designer, que funciona com arquivos Android `.axml` para construir visualmente interfaces do usuário. O Visual Studio para Mac abrirá esses arquivos no seu Designer Android, conforme mostrado nesta imagem:

![Designer de Interface do Usuário Android](media/intro-image31.png)

Para saber mais sobre o Designer Android, veja o documento [Visão geral do designer](https://developer.xamarin.com/Android/Guides/User_Interface/Designer_Overview).

### <a name="ios"></a>iOS

O iOS Designer está totalmente integrado com o Visual Studio para Mac e permite a edição visual de arquivos .xib e de Storyboard para criar interfaces do usuário do iOS, tvOS e WatchOS e transições. A interface do usuário pode ser criada usando a funcionalidade do tipo "arrastar e soltar" entre a Caixa de Ferramentas e o Design Surface, usando uma abordagem intuitiva para manipulação de eventos. O Designer do iOS também dá suporte a [controles personalizados](https://developer.xamarin.com/guides/ios/user_interface/designer/ios_designable_controls_overview/) com o benefício adicional de renderização em tempo de design.

![Designer de Storyboard do iOS](media/intro-image30.png)

Para saber mais sobre como usar o Designer do iOS, consulte os documentos do [Designer](https://developer.xamarin.com/guides/ios/user_interface/designer).

### <a name="mac"></a>Mac

O Xamarin fornece associações nativas de API do Mac, que permitem criar lindos aplicativos do Mac.

Para obter mais informações sobre como escrever aplicativos do Mac com o Visual Studio para Mac, consulte a documentação do [Xamarin.Mac](https://developer.xamarin.com/guides/#mac).

## <a name="gaming"></a>Jogos

O Visual Studio para Mac dá suporte ao desenvolvimento de jogos multiplataforma com o Unity 5.6.1.

Para começar, confira o [laboratório prático](https://github.com/Microsoft/vs4mac-labs/tree/master/Unity/Getting-Started) do Unity.

## <a name="enterprise-features"></a>Recursos do Enterprise

> [!Note]
> Esses produtos só podem ser usados com uma assinatura do Visual Studio Enterprise.

### <a name="profiler"></a>Criador de Perfil

O Xamarin Profiler tem três instrumentos disponíveis para criação de perfil. O guia [Introdução ao Xamarin Profiler](https://developer.xamarin.com/guides/cross-platform/deployment,_testing,_and_metrics/xamarin-profiler/) explora o que esses instrumentos medem e como eles analisam seu aplicativo e explica o significado dos dados apresentados em cada tela.

### <a name="inspector"></a>Inspector

O Xamarin Inspector fornece um console C# interativo com ferramentas para os usuários. Ele pode ser usado como um auxílio para depuração ou diagnóstico ao inspecionar aplicativos dinâmicos, como uma ferramenta de ensino, como uma ferramenta de documentação ou uma ferramenta de experimentação.

![Xamarin Inspector](media/intro-inspector.png)

Ele consiste em um aplicativo autônomo que fornece um console C# avançado para várias plataformas de programação (Android, iOS, Mac e Windows), além de integrar-se no fluxo de trabalho de depuração de seus IDEs. 

Para saber mais, consulte o guia do [Xamarin Inspector](https://developer.xamarin.com/guides/cross-platform/inspector/).

## <a name="next-steps"></a>Próximas etapas

* **Faça o tour** – para obter uma visão geral de vários dos principais recursos do Visual Studio para Mac, consulte o [Tour do IDE](ide-tour.md) do Visual Studio para Mac.
* **Instalação** – para saber mais sobre como baixar e instalar o Visual Studio, consulte o guia de [Instalação](installation.md).
* **Tutoriais do Xamarin** – para saber mais sobre como desenvolver um código com o Xamarin, acesse o Xamarin [Developer Center](https://developer.xamarin.com).
* **Vídeos** – para saber mais sobre outros recursos e aspectos do Visual Studio para Mac, confira os vídeos no site da [Xamarin University](https://university.xamarin.com).
* **Laboratórios práticos** – para começar a trabalhar com várias cargas de trabalho incluídas no Visual Studio para Mac, confira os [laboratórios práticos](https://github.com/Microsoft/vs4mac-labs).
