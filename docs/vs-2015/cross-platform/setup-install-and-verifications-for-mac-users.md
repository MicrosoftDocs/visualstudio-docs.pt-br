---
title: Configuração, instalação e verificações para usuários do Mac | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 22725520-59ba-4f6f-80e4-097b1287a34b
caps.latest.revision: 14
ms.author: crdun
manager: crdun
ms.openlocfilehash: fca4f8ef2d3fb1272dc835b4bedd7dcdcc83725f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51772827"
---
# <a name="setup-install-and-verifications-for-mac-users"></a>Configuração, instalação e verificações para usuários do Mac
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Este tópico destina-se a desenvolvedores que trabalham principalmente em um Mac e que usarão opcionalmente o Visual Studio dentro de uma máquina virtual do Windows no Mac. Se você for um desenvolvedor que trabalhe principalmente em um computador Windows e precisará configurar um Mac secundário para o direcionamento do iOS, consulte o tópico principal [Instalação e Configuração](../cross-platform/setup-and-install.md).  
  
 Para trabalhar com o Xamarin em um Mac, você precisará do seguinte:  
  
- Uma Conta do Xamarin. Vá para [ https://www.xamarin.com/ ](https://www.xamarin.com/) e clique em **Sign In** no canto superior direito da página, em seguida, clique em **criar uma nova conta** na página que aparece. Selecione um endereço de email e senha para sua conta do Xamarin.  
  
- Um Mac com OSX Yosemite (10.10) ou acima, com Xcode 7 e Xamarin 4 instalados.  
  
- Uma das seguintes configurações:  
  
  -   **Para executar o Xamarin Studio diretamente no Mac:** o Xamarin Studio é o ambiente de desenvolvimento do Xamarin que dá suporte à criação aplicativos Android, iOS e Windows usando C#.  Para obter uma visão geral rápida do Xamarin Studio, consulte a [Visão geral do Xamarin Studio](https://xamarin.com/studio) (xamarin.com).  
  
  -   **Se você já tiver o Parallels ou VMWare configurado em seu Mac:** execute o Windows com o Visual Studio 2015 e Xamarin 4 no Parallels ou VMWare.  Com essa configuração, o Xamarin é uma extensão que é instalada com o Visual Studio e que oferece a capacidade de usar o Visual Studio como ambiente de desenvolvimento para a criação de aplicativos Android, iOS e WinPhone usando C#.  Observe que você pode obter uma assinatura de 3 meses gratuita do Parallels como parte do programa Visual Studio Developer Essentials. Consulte [Microsoft Visual Studio Dev Essentials Incluirá Parallels Desktop Pro e Parallels Access](http://blog.parallels.com/blog/2015/11/18/visual-studio-dev-essentials/) (blog Parallels).  
  
  Este tópico fornece instruções para esses requisitos.  Enquanto o processo de instalação está em execução, você pode examinar o tópico [Saiba mais sobre desenvolvimento móvel com Xamarin](../cross-platform/learn-about-mobile-development-with-xamarin.md) para ler e inspecionar o material básico necessário.  
  
  **Neste tópico:**  
  
- [Configuração do Mac (Apple ID, Xcode e Xamarin)](#mac)  
  
- [Instalação do Windows no Parallels (Visual Studio e Xamarin)](#windows)  
  
- [Verifique o seu ambiente](#verify)  
  
##  <a name="mac"></a> Configuração do Mac (Apple ID, Xcode e Xamarin)  
  
1.  Crie uma ID Apple gratuita em [Minha ID Apple](https://appleid.apple.com/) se você não tiver uma. Isso é necessário para instalar e entrar no Xcode.  
  
2.  Baixe e instale o Xcode de [ https://developer.apple.com/xcode/ ](https://developer.apple.com/xcode/).  
  
3.  Baixe e instale o Xamarin, seguindo as instruções em [Instalando e configurando o Xamarin.iOS](http://developer.xamarin.com/guides/ios/getting_started/installation/mac/) (xamarin.com).  
  
4.  Depois de concluir a instalação do Xamarin em computadores Windows e Mac, siga as instruções em [Conectando-se ao Mac usando XMA](http://developer.xamarin.com/guides/ios/getting_started/installation/windows/#Connecting_to_the_Mac_Using_XMA) (xamarin.com) para que você possa trabalhar com iOS e Mac do Visual Studio no computador Windows.  
  
##  <a name="windows"></a> Instalação do Windows no Parallels (Visual Studio e Xamarin)  
  
1.  Usando a área de trabalho do Windows que você configurou no Parallels/VMWare, [baixe e inicie o instalador para qualquer edição do Visual Studio 2015](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) (Community, Professional ou Enterprise). O Visual Studio 2015 Community é a versão gratuita; as edições Professional e Enterprise poderão ser usadas em uma base de avaliação por 30 dias.  
  
2.  No instalador, selecione uma instalação **Personalizada**:  
  
     ![Escolhendo a opção Personalizada na instalação do Visual Studio](../cross-platform/media/cross-plat-xamarin-setup-1.png "Instalação 1 entre várias plataformas do Xamarin")  
  
3.  Marque/desmarque as seguintes caixas:  
  
    1.  Marque **Desenvolvimento Móvel Multiplataforma > C#/.NET (Xamarin)**. Isso também selecionará automaticamente várias ferramentas Android em Ferramentas Comuns e Kits de desenvolvimento de Software.  
  
         ![Selecione a opção Xamarin em Desenvolvimento Móvel de Multiplataforma](../cross-platform/media/cross-plat-xamarin-setup-2.png "Instalação 2 entre várias plataformas do Xamarin")  
  
    2.  Desmarque **Desenvolvimento Móvel Entre Plataformas > Emulador do Microsoft Visual Studio para Android**.  
  
4.  Clique no botão Instalar e permita que o processo seja executado. Novamente, isso levará algum tempo para ser concluído; durante esse período, você pode continuar com este tópico e analisar [Saiba mais sobre desenvolvimento móvel com Xamarin](../cross-platform/learn-about-mobile-development-with-xamarin.md).  
  
5.  Depois que a instalação for concluída, inicie o Visual Studio e entre com sua conta da Microsoft se solicitado (é a mesma conta que você usa com o Windows). Em seguida, verifique se há atualizações do Xamarin em **Ferramentas > Opções > Xamarin** ou **Ferramentas > Opções > Xamarin > Outros**, em que você encontrará um link **Verificar Agora**:  
  
     ![Verificando atualizações do Xamarin em Opções do Visual Studio](../cross-platform/media/cross-plat-xamarin-setup-3.png "Instalação 3 entre várias plataformas do Xamarin")  
  
    > [!NOTE]
    >  Certifique-se de atualizar o Xamarin para a versão 4.0.3.214 ou superior para evitar problemas com licenças anteriores do Xamarin.  Se você tentar verificar se há atualizações e vir um erro sobre as ferramentas de build Microsoft, consulte o thread nos [Fóruns do Xamarin](http://forums.xamarin.com/discussion/69015/xamarin-update-on-vs-2013-says-i-need-the-build-tools-for-vs-2015).
  
6.  Depois de concluir a instalação do Xamarin em computadores Windows e Mac, siga as instruções em [Conectando-se ao Mac usando XMA](http://developer.xamarin.com/guides/ios/getting_started/installation/windows/#Connecting_to_the_Mac_Using_XMA) (xamarin.com) para que você possa trabalhar com iOS do Visual Studio.  
  
##  <a name="verify"></a> Verifique o seu ambiente  
 Depois de ter concluído os instaladores, reserve alguns minutos para verificar se tudo está pronto para experimentar o desenvolvimento do Xamarin.  
  
### <a name="xamarin-studio"></a>Xamarin Studio  
 Primeiro, certifique-se de que quando você navegar para links fornecidos a opção **Xamarin Studio** estará selecionada no canto superior direito para que você veja a versão correta da documentação do Xamarin:  
  
 ![Selecionando Xamarin Studio para ver a documentação correta em Xamarin.com](../cross-platform/media/crossplat-xamarin-mac-1.png "CrossPlat Xamarin Mac 1")  
  
 **Android**  
  
1. Valide a criação de um projeto Android, seguindo as instruções em [Criar um projeto Android](http://developer.xamarin.com/recipes/android/general/projects/create_an_android_project/) (xamarin.com).  
  
2. Valide a depuração no Android Player por meio de [Android Player > Integração com a Documentação do Xamarin Studio](https://developer.xamarin.com/guides/android/getting_started/installation/android-player/#Integration_with_Xamarin_Studio) (xamarin.com).  
  
   **iOS**  
  
3. Validar a criação de um projeto iOS, seguindo as instruções em [Criar um iOS](http://developer.xamarin.com/recipes/ios/general/projects/create_an_ios_project/) (xamarin.com).  
  
4. Valide a depuração no simulador iOS por meio de [Depuração na documentação do simulador](https://developer.xamarin.com/guides/ios/deployment,_testing,_and_metrics/debugging_in_xamarin_ios/#Debugging_on_the_Simulator) (xamarin.com).  
  
### <a name="visual-studio"></a>Visual Studio  
 Primeiro, certifique-se de que quando você navegar para links fornecidos a opção **Visual Studio** estará selecionada no canto superior direito para que você veja a versão correta da documentação do Xamarin:  
  
 ![Selecionando Visual Studio para ver a documentação correta em Xamarin.com](../cross-platform/media/crossplat-xamarin-mac-2.png "CrossPlat Xamarin Mac 2")  
  
 Também entre na sua conta de Xamarin por meio de **Ferramentas > Conta do Xamarin...**.  
  
 **Android**  
  
1. Valide a criação de um projeto Android, seguindo as instruções em [Criar um projeto Android](http://developer.xamarin.com/recipes/android/general/projects/create_an_android_project/) (xamarin.com).  
  
2. Valide o designer Android: no projeto do Android no Gerenciador de Soluções, abra **Recursos > Layout > arquivo Main.axml**.  
  
   -   Se você receber um erro informando que "O SDK do Android instalado é muito antigo", clique em **abrir SDK do Android** na mensagem e selecione a versão do SDK mais recente disponível. Observe que você deve estar executando o Visual Studio como administrador para atualizar o SDK.  
  
3. Valide que você pode se conectar do Visual Studio ao emulador que está instalado no seu Mac.  O resultado disso é que você verá o Xamarin Player na lista de emuladores que você pode selecionar no Visual Studio para depuração.  Para fazer isso, siga as instruções em [Conectando o Visual Studio ao Xamarin Android Player](http://developer.xamarin.com/guides/android/deployment,_testing,_and_metrics/android-player-with-visual-studio-in-vm/) (xamarin.com).  
  
   **iOS**  
  
4. Verifique se seu Mac está disponível na rede e emparelhado com o Visual Studio, conforme descrito em [Conectando-se ao Mac usando XMA](http://developer.xamarin.com/guides/ios/getting_started/installation/windows/#Connecting_to_the_Mac_Using_XMA) (xamarin.com).  
  
5. Validar a criação de um projeto iOS, seguindo as instruções em [Criar um iOS](http://developer.xamarin.com/recipes/ios/general/projects/create_an_ios_project/) (xamarin.com).  
  
6. Valide o designer do storyboard: no projeto do iOS no Gerenciador de Soluções, abra o arquivo **MainStoryboard.storyboard**. Aqui, o Visual Studio hospeda o designer que executará remotamente o Mac.  
  
7. Validar compilação e depuração:  
  
   1.  Clique com o botão direito do mouse no projeto do iOS no Gerenciador de Soluções e selecione **Definir como projeto de inicialização**.  
  
   2.  Selecione o destino do **iPhoneSimulator** na lista suspensa do build do Visual Studio, conforme mostrado abaixo. Se nenhum simulador estiver listado, inicie o Xcode no Mac, selecione **Xcode->Preferências** e clique em **Baixar**. Em **Componentes** você deve ver as versões de simulador que estão disponíveis para download. Instruções adicionais para depuração podem ser encontradas na página [Depuração](https://developer.xamarin.com/guides/ios/deployment,_testing,_and_metrics/debugging_in_xamarin_ios/#Debugging_on_the_Simulator) do Xamarin (xamarin.com).  
  
        ![Selecionando o destino de build do iPhoneSimulator](../cross-platform/media/crossplat-xamarin-verify-5.png "CrossPlat Xamarin Verificação 5")  
  
   3.  Selecione um destino do iPhone na lista suspensa de depuração do Visual Studio conforme mostrado abaixo e inicie o depurador pressionando F5. Isso inicia o simulador no Mac em que você poderá interagir com o aplicativo enquanto a depuração acontecer no Visual Studio.  
  
        ![Selecionando um destino de depuração do iPhone](../cross-platform/media/crossplat-xamarin-verify-6.png "CrossPlat Xamarin Verificação 6")

