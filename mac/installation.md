---
title: Instalar o Visual Studio 2019 para Mac
description: Instruções sobre como instalar o Visual Studio 2019 para Mac e os componentes adicionais necessários para o desenvolvimento de multiplataforma.
author: heiligerdankgesang
ms.author: dominicn
ms.date: 09/18/2019
ms.technology: vs-ide-install
ms.assetid: 22B1F2CD-32AE-464D-80AC-C8AB4786B015
ms.custom: video
ms.topic: how-to
ms.openlocfilehash: 4e38084d4dc1e5095581846d0810ad44b742bcdf
ms.sourcegitcommit: 2ce59c2ffeba5ba7f628c2e6c75cba4731deef8a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2020
ms.locfileid: "85938958"
---
# <a name="install-visual-studio-2019-for-mac"></a>Instalar o Visual Studio 2019 para Mac

Para começar a desenvolver aplicativos nativos de multiplataforma do .NET no macOS, instale o Visual Studio 2019 para Mac seguindo as etapas abaixo.

 > [!div class="button"]
 > [Baixar o Visual Studio para Mac](https://visualstudio.microsoft.com/vs/mac/)

## <a name="requirements"></a>Requisitos

- Um Mac com macOS High Sierra 10.12 ou posterior.

Para criar aplicativos Xamarin para iOS ou macOS, você também precisará de:

- Xcode 10.0 ou posterior. A versão estável mais recente geralmente é recomendada.
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

    [![Escolha quais recursos de carga de trabalho opcionais você deseja instalar](media/install-selection.png)](media/install-selection.png#lightbox)

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
|**Desenvolvimento de jogos do Unity de plataforma cruzada**|         |Nenhuma plataforma adicional precisa ser instalada além Visual Studio para Mac.| Confira o [Guia de instalação do Unity](/visualstudio/mac/setup-vsmac-tools-unity) para saber mais sobre como instalar a extensão do Unity.|


7. Após você ter feito suas seleções, pressione o botão **Instalar**.
8. O instalador exibirá o andamento conforme o download acontece e instalará o Visual Studio para Mac e as cargas de trabalho selecionadas. Você será solicitado a inserir sua senha para conceder os privilégios necessários para a instalação.:

    [![Escolha quais recursos de carga de trabalho opcionais você deseja instalar](media/installation-progress.png)](media/installation-progress.png#lightbox)

9. Uma vez instalado, o Visual Studio para Mac solicitará que você personalize sua instalação entrando e selecionando as associações de chave que você gostaria de usar:

    [![Entrar no IDE](media/ide-tour-2019-start-signin.png)](media/ide-tour-2019-start-signin.png#lightbox)

    [![Escolha quais atalhos de teclado você gostaria de usar](media/ide-tour-2019-keyboard-shortcut.png)](media/ide-tour-2019-keyboard-shortcut.png#lightbox)

Se você tiver problemas de rede durante a instalação em um ambiente corporativo, examine as instruções em [instalação por trás de um firewall ou proxy](/visualstudio/mac/installation#install-visual-studio-for-mac-behind-a-firewall-or-proxy-server).

Saiba mais sobre as novidades nas [notas sobre a versão](/visualstudio/releasenotes/vs2019-mac-relnotes).

> [!NOTE]
> Se optou por não instalar uma plataforma ou ferramenta durante a instalação original (desmarcando-a na etapa 6), você deverá executar o instalador novamente se quiser adicionar os componentes mais tarde.

## <a name="install-visual-studio-for-mac-behind-a-firewall-or-proxy-server"></a>Instalar o Visual Studio para Mac por trás de um firewall ou servidor proxy

Para instalar o Visual Studio para Mac por trás de um firewall, determinados pontos de extremidade devem estar acessíveis para permitir o download das ferramentas necessárias e as atualizações do software.

Configure a rede para permitir o acesso aos seguintes locais:

- [Pontos de extremidade do Visual Studio](/visualstudio/mac/install-behind-a-firewall-or-proxy-server)

## <a name="next-steps"></a>Próximas etapas

A instalação do Visual Studio para Mac permite que você comece a escrever código para seus aplicativos. Os guias a seguir são fornecidos para orientar você durante as próximas etapas da criação e implantação de seus projetos.

### <a name="ios"></a>iOS

1. [Hello, iOS](https://developer.xamarin.com/guides/ios/getting_started/hello,_iOS/)
2. [Provisionamento de dispositivo](https://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning) (para executar o aplicativo no dispositivo).

### <a name="android"></a>Android

1. [Como usar o Gerenciador de SDK do Xamarin Android](https://developer.xamarin.com/guides/android/getting_started/installation/android-sdk/?ide=xs)
2. [Emulador do SDK do Android](https://developer.xamarin.com/guides/android/getting_started/installation/android-emulator/)
4. [Configurar o dispositivo para desenvolvimento](https://developer.xamarin.com/guides/android/getting_started/installation/set_up_device_for_development/)

### <a name="net-core-apps-aspnet-core-web-apps-unity-game-development"></a>Aplicativos .NET Core, aplicativos Web do ASP.NET Core, desenvolvimento de jogos em Unity

Para outras cargas de trabalho, confira a página [Cargas de trabalho](workloads.md).

## <a name="related-video"></a>Vídeo relacionados

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Acquisition/player]

## <a name="see-also"></a>Confira também

- [Instalar o Visual Studio (no Windows)](/visualstudio/install/install-visual-studio)
