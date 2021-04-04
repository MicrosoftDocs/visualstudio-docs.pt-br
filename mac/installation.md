---
title: Instalar o Visual Studio 2019 para Mac
description: Instruções sobre como instalar o Visual Studio 2019 para Mac e os componentes adicionais necessários para o desenvolvimento de multiplataforma.
author: heiligerdankgesang
ms.author: dominicn
ms.date: 03/04/2021
ms.technology: vs-ide-install
ms.assetid: 22B1F2CD-32AE-464D-80AC-C8AB4786B015
ms.custom: video
ms.topic: how-to
ms.openlocfilehash: 653e653a0574da52c0030b06c7a8c13b436ed686
ms.sourcegitcommit: 4bf7d82eb3a837ad5d1ae5c110039cbf74258f18
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/03/2021
ms.locfileid: "106273408"
---
# <a name="install-visual-studio-2019-for-mac"></a>Instalar o Visual Studio 2019 para Mac

Para começar a desenvolver aplicativos nativos de multiplataforma do .NET no macOS, instale o Visual Studio 2019 para Mac seguindo as etapas abaixo.

 > [!div class="button"]
 > [Baixar o Visual Studio para Mac](https://visualstudio.microsoft.com/vs/mac/)

## <a name="requirements"></a>Requisitos

- Um Mac com macOS High Sierra 10.13 ou superior.

Para criar aplicativos Xamarin para iOS ou macOS, você também precisará de:

- Um Mac compatível com a versão mais recente do Xcode. Consulte a [documentação de requisitos mínimos](https://developer.apple.com/support/xcode/) da Apple
- A versão mais recente do [Xcode](https://developer.apple.com/xcode). Pode ser possível [usar uma versão mais antiga do Xcode](https://docs.microsoft.com/xamarin/ios/troubleshooting/questions/old-version-xcode) se o seu Mac não for compatível com a versão mais recente.
- Uma ID da Apple. Se ainda não tiver uma ID da Apple, crie uma nova em https://appleid.apple.com. Será necessário ter uma ID da Apple para instalar e entrar no Xcode.

## <a name="installation-instructions"></a>Instruções de instalação

1. Baixe o instalador da [página de download do Visual Studio para Mac](https://visualstudio.microsoft.com/vs/mac/).
2. Depois que o download for concluído, clique no **VisualStudioforMacInstaller.dmg** para montar o instalador e, em seguida, execute-o clicando duas vezes no logotipo de seta:

    [![Clique na seta grande para iniciar a instalação](media/install-installer-sml.png)](media/install-installer.png#lightbox)

3. Poderá ser apresentado a você um aviso de que o aplicativo está sendo baixado da Internet. Clique em **Abrir**.
4. Aguarde enquanto o instalador verifica seu sistema:

    [![O instalador verifica o sistema em busca de componentes instalados](media/install-checking-sml.png)](media/install-checking.png#lightbox)

5. Um alerta será exibido solicitando que você reconheça os termos de licença e privacidade. Siga os links para lê-los e, em seguida, pressione **Continuar** se você concordar com eles:

    [![Siga os links para a privacidade e os termos e continue se concordar](media/install-privacy.png)](media/install-privacy.png#lightbox)

6. A lista de cargas de trabalho disponíveis é exibida. Selecione os componentes que você deseja usar:

    [![Captura de tela de "o que você deseja instalar?" no instalador do Mac do Visual Studio, mostrando uma lista de componentes disponíveis para instalação.](media/install-selection.png)](media/install-selection.png#lightbox)

   Se você não quiser instalar todas as plataformas, use o guia abaixo como ajuda para decidir quais plataformas serão instaladas:

   |Tipo de aplicativo  |Destino  |Seleção  |Observações  |
   |---------|---------|---------|---------|
   |**Aplicativos usando o Xamarin**| Xamarin.Forms|Selecionar plataformas **Android** e **Ios** |Será necessário instalar o [ **Xcode**](https://developer.apple.com/xcode/) |
   ||Somente iOS|Selecionar plataforma **Ios**|Será necessário instalar o [ **Xcode**](https://developer.apple.com/xcode/)|
   ||Somente Android|Selecionar plataforma **Android**|Observe que você também deve selecionar as dependências relevantes|
   ||Somente Mac|Selecione a plataforma **MacOS (Cocoa)**|Será necessário instalar o [ **Xcode**](https://developer.apple.com/xcode/)|
   |**Aplicativos .NET Core**|         |Selecione plataforma **.NET Core** .|         |
   |**Aplicativos Web ASP.NET Core**|         |Selecione plataforma **.NET Core** .|         |
   |**Azure Functions**|         |Selecione plataforma **.NET Core** .|         |
   |**Desenvolvimento de jogos do Unity de plataforma cruzada**|         |Nenhuma plataforma adicional precisa ser instalada além Visual Studio para Mac.| Confira o [Guia de instalação do Unity](./setup-vsmac-tools-unity.md) para saber mais sobre como instalar a extensão do Unity.|

7. Após você ter feito suas seleções, pressione o botão **Instalar**.
8. O instalador exibirá o andamento conforme o download acontece e instalará o Visual Studio para Mac e as cargas de trabalho selecionadas. Você será solicitado a inserir sua senha para conceder os privilégios necessários para a instalação.:

    [![Captura de tela do instalador do Mac do Visual Studio mostrando uma tela de progresso da instalação para o .NET Developer Toolkit para Mac.](media/installation-progress.png)](media/installation-progress.png#lightbox)

9. Uma vez instalado, o Visual Studio para Mac solicitará que você personalize sua instalação entrando e selecionando as associações de chave que você gostaria de usar:

    [![Entrar no IDE](media/ide-tour-2019-start-signin.png)](media/ide-tour-2019-start-signin.png#lightbox)

    [![Escolha quais atalhos de teclado você gostaria de usar](media/ide-tour-2019-keyboard-shortcut.png)](media/ide-tour-2019-keyboard-shortcut.png#lightbox)

Se você tiver problemas de rede durante a instalação em um ambiente corporativo, examine as instruções em [instalação por trás de um firewall ou proxy](#install-visual-studio-for-mac-behind-a-firewall-or-proxy-server).

Saiba mais sobre as novidades nas [notas sobre a versão](/visualstudio/releasenotes/vs2019-mac-relnotes).

> [!NOTE]
> Se optou por não instalar uma plataforma ou ferramenta durante a instalação original (desmarcando-a na etapa 6), você deverá executar o instalador novamente se quiser adicionar os componentes mais tarde.

## <a name="install-visual-studio-for-mac-behind-a-firewall-or-proxy-server"></a>Instalar o Visual Studio para Mac por trás de um firewall ou servidor proxy

Para instalar o Visual Studio para Mac por trás de um firewall, determinados pontos de extremidade devem estar acessíveis para permitir o download das ferramentas necessárias e as atualizações do software.

Configure a rede para permitir o acesso aos seguintes locais:

- [Pontos de extremidade do Visual Studio](./install-behind-a-firewall-or-proxy-server.md)

## <a name="next-steps"></a>Próximas etapas

A instalação do Visual Studio para Mac permite que você comece a escrever código para seus aplicativos. Os guias a seguir são fornecidos para orientar você durante as próximas etapas da criação e implantação de seus projetos.

### <a name="ios"></a>iOS

1. [Hello, iOS](https://docs.microsoft.com//xamarin/ios/get-started/hello-ios/)
2. [Provisionamento de dispositivo](https://docs.microsoft.com/xamarin/ios/get-started/installation/device-provisioning/) (para executar o aplicativo no dispositivo).

### <a name="android"></a>Android

1. [Hello, Android](https://docs.microsoft.com/xamarin/android/get-started/hello-android/)
2. [Como usar o Gerenciador de SDK do Xamarin Android](https://docs.microsoft.com/xamarin/android/get-started/installation/android-sdk?tabs=macos)
3. [Emulador do SDK do Android](https://docs.microsoft.com/xamarin/android/get-started/installation/android-emulator/)
4. [Configurar o dispositivo para desenvolvimento](https://docs.microsoft.com/xamarin/android/get-started/installation/set-up-device-for-development)

### <a name="xamarinforms"></a>Xamarin.Forms

Crie aplicativos nativos de plataforma cruzada com o Xamarin. Forms:

1. [Guias de início rápido do Xamarin. Forms](https://docs.microsoft.com/xamarin/get-started/quickstarts/)

### <a name="net-core-apps-aspnet-core-web-apps-unity-game-development"></a>Aplicativos .NET Core, aplicativos Web do ASP.NET Core, desenvolvimento de jogos em Unity

Para outras cargas de trabalho, confira a página [Cargas de trabalho](workloads.md).

## <a name="related-video"></a>Vídeo relacionados

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Acquisition/player]

## <a name="see-also"></a>Confira também

- [Instalar o Visual Studio (no Windows)](/visualstudio/install/install-visual-studio)
