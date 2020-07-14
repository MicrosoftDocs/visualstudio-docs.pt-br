---
title: Xamarin
description: 'Usar o Xamarin no Visual Studio para Mac permite que você crie aplicativos multiplataforma voltados para iOS, Mac, Android, tvOS e watchOS '
author: therealjohn
ms.author: johmil
ms.date: 06/18/2019
ms.assetid: 339F6051-5F90-48DC-8237-EBBC8A03A32B
ms.topic: overview
ms.openlocfilehash: e40d9640ca2e62148e4ad166845d8f59854367ff
ms.sourcegitcommit: 5335a9864d5747bc917ed28d4ebeade3076b10e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2020
ms.locfileid: "85950664"
---
# <a name="xamarin-mobile-app-development"></a>Desenvolvimento de aplicativos móveis do Xamarin

O suporte de primeira classe para o [Xamarin](/xamarin) permite que você desenvolva experiências nativas avançadas para Android, macOS, iOS, tvOS e watchOS. Os aplicativos de plataforma cruzada Xamarin.Forms o ajudam a compartilhar o código de interface do usuário baseado em XAML entre macOS, iOS e Android sem limitar o acesso à funcionalidade nativa.

## <a name="xamarinforms"></a>Xamarin.Forms

O Hot recarregamento de XAML para Xamarin. Forms é integrado ao Visual Studio para Mac na versão 8,3 e posteriores. Com esse recurso, as alterações habilitadas são refletidas instantaneamente em seu aplicativo em execução sempre que você salvar o arquivo.

O Hot recarregamento de XAML pode ser habilitado marcando a caixa de seleção **habilitar o WebLoad do xamarin** no **Visual Studio > preferências > projetos > Xamarin Hot recarregar**.

Para obter mais informações sobre a recarga a quente, consulte o [Guia de Hot recarregamento de XAML para Xamarin. Forms](/xamarin/xamarin-forms/xaml/hot-reload) na documentação.

## <a name="android"></a>Android

O Visual Studio para Mac tem seu próprio gerenciador de SDK do Android integrado, permitindo que você acesse os SDKs aos quais deseja que seu aplicativo se destine.

Para aplicativos Android, o Visual Studio para Mac inclui seu próprio designer, que funciona com arquivos Android `.axml` para construir visualmente interfaces do usuário. O Visual Studio para Mac abrirá esses arquivos no seu Android Designer, conforme mostrado nesta imagem:

![Designer de Interface do Usuário Android](media/intro-image31.png)

Para saber mais sobre o Android Designer, veja o guia [Visão geral do Xamarin.Android Designer](/xamarin/android/user-interface/android-designer/index).

## <a name="ios"></a>iOS

O iOS Designer está totalmente integrado com o Visual Studio para Mac e permite a edição visual de arquivos .xib e de Storyboard para criar interfaces do usuário do iOS, tvOS e WatchOS e transições. A interface do usuário pode ser criada usando a funcionalidade do tipo "arrastar e soltar" entre a Caixa de Ferramentas e o Design Surface, usando uma abordagem intuitiva para manipulação de eventos. O Designer do iOS também dá suporte a [controles personalizados](/xamarin/ios/user-interface/designer/ios-designable-controls-overview) com o benefício adicional de renderização em tempo de design.

![Designer de Storyboard do iOS](media/intro-image30.png)

Para obter mais informações sobre como usar o Designer do iOS, consulte os guias do [Designer](/xamarin/ios/user-interface/designer/?tabs=macos).

### <a name="mac"></a>Mac

O Xamarin fornece associações nativas de API do Mac, que permitem criar lindos aplicativos do Mac.

Para obter mais informações sobre como escrever aplicativos do Mac com o Visual Studio para Mac, consulte os guias do [Xamarin.Mac](/xamarin/mac/get-started/index).

## <a name="xamarin-enterprise-features"></a>Recursos do Xamarin Enterprise

> [!Note]
> Esses produtos só podem ser usados com uma assinatura do Visual Studio Enterprise.

### <a name="profiler"></a>Criador de perfil

O Xamarin Profiler tem três instrumentos disponíveis para criação de perfil. O guia [Introdução ao Xamarin Profiler](/xamarin/tools/profiler/index?tabs=macos) explora o que esses instrumentos medem e como eles analisam seu aplicativo e explica o significado dos dados apresentados em cada tela.

### <a name="inspector"></a>Inspetor

O Xamarin Inspector fornece um console C# interativo com ferramentas para os usuários. Ele pode ser usado como um auxílio para depuração ou diagnóstico ao inspecionar aplicativos dinâmicos, como uma ferramenta de ensino, como uma ferramenta de documentação ou uma ferramenta de experimentação.

![Xamarin Inspector](media/intro-inspector.png)

Ele consiste em um aplicativo autônomo que fornece um console C# avançado para várias plataformas de programação (Android, iOS, Mac e Windows), além de integrar-se no fluxo de trabalho de depuração de seus IDEs.

Para saber mais, consulte o guia do [Xamarin Inspector](/xamarin/tools/inspector/).
