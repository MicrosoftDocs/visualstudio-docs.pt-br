---
title: Instalar o Visual Studio para Mac
description: Instruções sobre como instalar o Visual Studio para Mac e os componentes adicionais necessários para o desenvolvimento de plataforma cruzada.
author: conceptdev
ms.author: crdun
ms.date: 11/03/2018
ms.technology: vs-ide-install
ms.assetid: 22B1F2CD-32AE-464D-80AC-C8AB4786B015
ms.openlocfilehash: 2a179b5d02a3c50e6942a660e845edd546037d86
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52896478"
---
# <a name="set-up-and-install-visual-studio-for-mac"></a>Configurar e instalar o Visual Studio para Mac

## <a name="requirements"></a>Requisitos

Para começar a desenvolver aplicativos de plataforma cruzada nativos após baixar o Visual Studio para Mac, é necessário preparar-se instalando e configurando alguns itens.

Para trabalhar com iOS no Visual Studio você precisará do seguinte:

* Um Mac com macOS Sierra 10.12 ou superior
* Xcode 8.3 ou posterior. A versão estável mais recente geralmente é recomendada.
* Uma ID da Apple. Se ainda não tiver uma ID da Apple, crie uma nova em https://appleid.apple.com. Será necessário ter uma ID da Apple para instalar e entrar no Xcode.

> [!TIP]
> A versão prévia do Visual Studio 2019 para Mac [agora está disponível](install-preview.md) para teste.

## <a name="install"></a>Instalar o

1. Faça download do Visual Studio para Mac em [https://visualstudio.microsoft.com/](https://visualstudio.microsoft.com/)

2. Depois que o pacote do instalador for baixado, clique no arquivo **VisualStudioInstaller.dmg** para montar o instalador e executá-lo clicando duas vezes no logotipo, conforme ilustrado na imagem a seguir:

   ![Caixa de diálogo do instalador](media/installer-image1.png)

3. Você poderá ver uma caixa de diálogo de alerta semelhante à imagem a seguir. Nesse caso, clique em **Abrir**:

   ![caixa de diálogo de alerta](media/installer-image2.png)

4. O instalador inspeciona seu sistema para verificar quais componentes precisam ser instalados ou atualizados:

   ![Avaliando o seu sistema](media/installer-image3.png)

5. Em seguida, você verá uma caixa de diálogo de alerta solicitando que você confirme os termos de Privacidade e de Licença. Pressione o botão **Continuar** para confirmar os termos:

   ![Caixa de diálogo Licença](media/installer-image4.png)

6. O instalador apresenta uma lista de componentes necessários que estão faltando e que precisa ser baixados e instalados. Selecione os produtos que você deseja baixar aqui:

   ![Selecionar itens](media/installer-image5.png)

   Se você não quiser instalar todas as plataformas, use o guia abaixo como ajuda para decidir quais plataformas serão instaladas:

   * **Aplicativos que usam o Xamarin**:
      - Xamarin.Forms: Selecione as plataformas **Android** e **iOS**.
      - Somente iOS: selecione a plataforma **iOS** (Observe que será necessário instalar o [**Xcode**](https://developer.apple.com/xcode/)).
      - Somente Android: selecione a plataforma **Android** (Observe que você também deve selecionar as dependências relevantes).
      - Somente Mac: selecione a plataforma **macOS** (Observe que será necessário instalar o [**Xcode**](https://developer.apple.com/xcode/)).
      - Aplicativos Xamarin totalmente plataforma cruzada: selecione as plataformas **Android**, **iOS** e **macOS**.
   * **Aplicativos .NET Core**: selecione a plataforma **.NET Core**.
   * **Aplicativos Web ASP.NET Core**: selecione a plataforma **.NET Core**.
   * **Desenvolvimento de jogos em Unity em plataforma cruzada**: nenhuma plataforma adicional precisa ser instalada além do Visual Studio para Mac. Confira o [Guia de instalação do Unity](setup-vsmac-tools-unity.md) para saber mais sobre como instalar a extensão do Unity.

   Esta tela de instalação exibe a versão e o tamanho de cada componente individual. Você pode clicar em cada componente para exibir uma lista de dependências desse componente (para Android), consultar pacotes adicionais que ele baixa (para .NET Core) ou exibir os aplicativos adicionais necessários (iOS e macOS):

   ![Dependências adicionais de Android](media/installer-image6.png)

7. Quando você estiver satisfeito com sua seleção, pressione o botão **Instalar e Atualizar** para iniciar o processo de instalação.

8. O instalador iniciará o processo de download e instalação dos itens selecionados:

   ![Iniciando a instalação](media/installer-image7.png)

   ![Baixando o Xamarin.Mac](media/installer-image8.png)

   ![Concluindo a instalação](media/installer-image9.png)

9. Pode ser solicitado que você eleve as permissões necessárias para os componentes individuais que são necessários para concluir a instalação. Insira suas credenciais de administrador para continuar o processo de instalação:

   ![Insira as permissões para prosseguir com o instalador](media/installer-image10.png)

10. Depois que a instalação for bem-sucedida, você poderá começar a desenvolver aplicativos no Visual Studio pressionando **Iniciar**:

    ![Abrir o Visual Studio](media/installer-image11.png)

> [!NOTE]
> Se você optou por não instalar uma plataforma ou ferramenta durante a instalação original (desmarcando-a na etapa 6), deverá executar o [instalador](https://visualstudio.microsoft.com/vs/) novamente se desejar adicionar os componentes mais tarde.

## <a name="install-visual-studio-for-mac-behind-a-firewall-or-proxy-server"></a>Instalar o Visual Studio para Mac por trás de um firewall ou servidor proxy

Para instalar o Visual Studio para Mac por trás de um firewall, determinados pontos de extremidade devem estar acessíveis para permitir o download das ferramentas necessárias e as atualizações do software.

Configure a rede para permitir o acesso aos seguintes locais:

* [Pontos de extremidade do Visual Studio](/visualstudio/install/install-visual-studio-behind-a-firewall-or-proxy-server)

## <a name="next-steps"></a>Próximas etapas

A instalação do Visual Studio para Mac permite que você comece a escrever código para seus aplicativos. Os guias a seguir são fornecidos para orientar você durante as próximas etapas da criação e implantação de seus projetos.

### <a name="ios"></a>iOS

1. [Hello, iOS](https://developer.xamarin.com/guides/ios/getting_started/hello,_iOS/)
2. [Provisionamento de dispositivo](https://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning) (para executar o aplicativo no dispositivo).

### <a name="android"></a>Android

1. [Usando o Gerenciador de SDK do Xamarin Android](https://developer.xamarin.com/guides/android/getting_started/installation/android-sdk/?ide=xs)
2. [Emulador do SDK do Android](https://developer.xamarin.com/guides/android/getting_started/installation/android-emulator/)
4. [Configurar o dispositivo para desenvolvimento](https://developer.xamarin.com/guides/android/getting_started/installation/set_up_device_for_development/)

### <a name="net-core-apps-aspnet-core-web-apps-unity-game-development"></a>Aplicativos .NET Core, aplicativos Web do ASP.NET Core, desenvolvimento de jogos em Unity

Para outras cargas de trabalho, confira a página [Cargas de trabalho](workloads.md).

## <a name="see-also"></a>Consulte também

- [Instalar o Visual Studio 2017 (no Windows)](/visualstudio/install/install-visual-studio)