---
title: Instalar o Visual C++ para Desenvolvimento Móvel de Multiplataforma | Microsoft Docs
ms.custom: ''
ms.date: 05/21/2018
ms.technology: vs-ide-mobile
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: aaea6b8d-55eb-4427-8185-c050f855c257
author: corob-msft
ms.author: corob
manager: douge
ms.workload:
- xplat-cplusplus
ms.openlocfilehash: 5dffe82511e75889ea588cb23b1f19490f991ab0
ms.sourcegitcommit: 71b307ce86c4079cc7ad686d8d5f96a6a123aadd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2018
ms.locfileid: "39251901"
---
# <a name="install-cross-platform-mobile-development-with-c"></a>Instalar Desenvolvimento Mobile com C++ de plataforma cruzada

Você pode usar C++ no Visual Studio para criar aplicativos de Área de Trabalho do Windows, aplicativos UWP (Plataforma Universal do Windows), aplicativos Linux e, agora, os aplicativos para iOS e Android. A carga de trabalho **Desenvolvimento móvel com C++** é um conjunto de componentes para instalação no Visual Studio que inclui modelos de plataforma cruzada do Visual Studio para iOS, Android e UWP. Ela instala as ferramentas e SDKs de plataforma cruzada que você precisa para começar rapidamente, sem a necessidade de localizar, baixar e configurá-los por conta própria. É possível usar essas ferramentas no Visual Studio para criar, editar, depurar e testar seus projetos de plataforma cruzada com facilidade. Este tópico descreve como instalar as ferramentas e softwares de terceiros necessários para desenvolver aplicativos de plataforma cruzada em C++ usando o Visual Studio. Para obter uma visão geral, confira [Visual C++ para desenvolvimento móvel multiplataforma](https://go.microsoft.com/fwlink/p/?LinkId=536383)

## <a name="requirements"></a>Requisitos

- Para obter os requisitos de instalação, confira [Requisitos do sistema da família de produtos do Visual Studio](/visualstudio/productinfo/vs2017-system-requirements-vs).

   > [!IMPORTANT]
   > Se estiver usando o Windows 7 ou o Windows Server 2008 R2, você poderá desenvolver código para aplicativos de Área de Trabalho do Windows, bibliotecas e aplicativos do tipo Native Acivity do Android e aplicativos e bibliotecas de código para iOS, mas não aplicativos para a Windows Phone ou UWP.

Para compilar aplicativos para plataformas de dispositivo específicas, há alguns requisitos adicionais:

- Emuladores do Windows Phone e o Emulador do Microsoft Visual Studio para Android requerem um computador que possa executar o Hyper-V. O recurso do Hyper-V do Windows deve ser habilitado antes que você possa instalar e executar os emuladores. Para obter mais informações, consulte os [requisitos de sistema](system-requirements-for-the-visual-studio-emulator-for-android.md) do emulador.

- Os emuladores de Android x86 que vêm com o SDK do Android funcionam melhor em computadores que executam o driver Intel HAXM. Este driver requer um processador Intel x64 com VT-x e suporte para Execute Disable Bit. Para saber mais, confira [Intel® HAXM (Hardware Accelerated Execution Manager)](https://go.microsoft.com/fwlink/p/?LinkId=536385).

- Compilar código para iOS requer uma Apple ID, uma conta do Programa de Desenvolvedores de iOS e um computador Mac que possa executar o [Xcode](https://go.microsoft.com/fwlink/p/?LinkId=536387) versão 6 ou posterior em no OS X Mavericks (versão 10.9) ou posteriores. Para obter um link para etapas de instalação, veja [Ferramentas de instalação para iOS](#install-tools-for-ios).

## <a name="get-the-tools"></a>Obtenha as ferramentas

O Desenvolvimento Mobile com C++ Está disponível nas edições Community, Professional e Enterprise do Visual Studio. Para obter o Visual Studio, acesse a página [Downloads do Visual Studio](https://go.microsoft.com/fwlink/p/?linkid=517106). As ferramentas de desenvolvimento móvel em plataforma cruzada estão disponíveis a partir do Visual Studio 2015 Atualização 2 ou posterior.

## <a name="install-the-tools"></a>Instalar as ferramentas

O Instalador do Visual Studio para Visual Studio 2017 inclui uma carga de trabalho **Desenvolvimento Mobile com C++** que instala as ferramentas de linguagem do C++, modelos e componentes necessários para o desenvolvimento para Android e iOS no Visual Studio. Ele instala os conjuntos de ferramentas GCC e Clang necessários para compilação e depuração de Android, e componentes para se comunicar com um Mac para desenvolvimento de iOS. Ele também instala todas as ferramentas de terceiros e kits de desenvolvimento de software que são necessários para dar suporte ao desenvolvimento de aplicativos Android e iOS. A maioria dessas ferramentas de terceiros são softwares livres necessários para dar suporte à plataforma Android.

- O NDK (Kit de Desenvolvimento Nativo) do Android é necessário para compilar código C++ que se destina à plataforma Android.

- O SDK do Android, o Apache Ant e o Java SE Development Kit são necessários para o processo de build do Android.

- O Android Emulator do Google e o Hardware Accelerated Execution Manager da Intel são componentes opcionais, mas recomendados. Você pode desenvolver e depurar diretamente em um dispositivo Android, mas é mais fácil usar um emulador em sua área de trabalho para depuração. A Microsoft também fornece um emulador do Visual Studio para Android que pode ser instalado separadamente.

#### <a name="to-install-the-mobile-development-with-c-workload-in-visual-studio-2017"></a>Para instalar a carga de trabalho Desenvolvimento Mobile com C++ no Visual Studio de 2017

1. Execute o **Instalador do Visual Studio** pelo menu **Iniciar**.

1. Se você já tiver instalado o Visual Studio, escolha o botão **Modificar** para a versão instalada do Visual Studio que você deseja modificar. Caso contrário, escolha **Instalar** para instalar o Visual Studio.

1. Com a guia **Cargas de Trabalho** selecionada, role a tela para baixo e selecione a carga **Desenvolvimento Mobile com C++** no Instalador do Visual Studio. Após a seleção dessa carga de trabalho, outros componentes necessários para desenvolvimento em C++ também serão selecionados. Você também pode escolher outras cargas de trabalho e componentes individuais para instalação simultânea. Para compilar o código de plataforma cruzada que também é direcionado ao UWP, selecione a carga de trabalho **Desenvolvimento na Plataforma Universal do Windows**.

1. No painel **Detalhes da instalação**, expanda **Desenvolvimento Mobile com C++**. Na seção **Opcional**, você pode escolher outras versões do NDK, o Android Emulator do Google, o Hardware Accelerated Execution Manager da Intel e a ferramenta de aceleração de compilação IncrediBuild.

1. Por padrão, um ou mais componentes de instalação do SDK do Android estão incluídos na carga de trabalho. Há outras versões do SDK do Android disponíveis. Para adicionar uma à sua instalação, escolha a guia **Componentes Individuais** e, em seguida, role para baixo até a seção **SDKs, bibliotecas e estruturas** para fazer sua seleção.

1. Escolha o botão **Modificar** ou **Instalar** para instalar a carga de trabalho **Desenvolvimento Mobile com C++** e suas outras cargas de trabalho e componentes selecionados.

   Quando a instalação for concluída, feche o instalador e reinicie o computador. Algumas ações de instalação dos componentes de terceiros não têm efeito até que o computador seja reiniciado.

   > [!IMPORTANT]
   > Você deve reiniciar para certificar-se de que tudo esteja instalado corretamente.

1. Abra o Visual Studio. Se esta for a primeira vez que você executa o Visual Studio, ele poderá levar algum tempo para ser configurado e se conectar. Quando o Visual Studio estiver pronto, verifique se há atualizações e instale-as.

#### <a name="to-install-the-mobile-development-component-and-third-party-tools-in-visual-studio-2015"></a>Para instalar o componente de Desenvolvimento Móvel e ferramentas de terceiros no Visual Studio 2015

Se você estiver usando o Visual Studio 2015, o instalador dele incluirá uma opção para instalar o Visual C++ para Desenvolvimento Móvel Multiplataforma, o que instala as ferramentas de linguagem C++ necessárias, modelos e componentes no Visual Studio 2015.

1. Execute o instalador do Visual Studio 2015. Para instalar componentes opcionais, escolha **Personalizado** como o tipo de instalação. Escolha **Avançar** para selecionar os componentes opcionais a serem instalados.

1. Em **Selecionar recursos**, expanda **Desenvolvimento Móvel de Multiplataforma** e marque **Desenvolvimento Móvel no Visual C++**.

   ![Selecionar Desenvolvimento Móvel no Visual C&#43;&#43;](../cross-platform/media/cppmdd_install_vcmdd.png "CPPMDD_Install_VCMDD")

   Por padrão, quando você seleciona **Desenvolvimento Móvel no Visual C++**, a opção **Linguagens de Programação** é configurada para instalar o **Visual C++** e as opções **Ferramentas comuns e Software Development Kits** são configuradas para instalar componentes de terceiros exigidos. Você pode escolher componentes adicionais se precisar deles. Por padrão, o **Emulador do Microsoft Visual Studio para Android** também é selecionado. Componentes que já estão instalados aparecem inativos na lista.

   Para compilar aplicativos universais do Windows e compartilhar código entre eles e seus projetos Android e iOS, em **Selecionar recursos**, expanda **Desenvolvimento no Windows e na Web** e marque **Ferramentas de Desenvolvimento de Aplicativo Universal do Windows**. Se não planejar compilar aplicativos universais do Windows, você poderá ignorar essa opção.

   Escolha **Avançar** para continuar.

1. Os componentes de terceiros têm seus próprios termos de licença. É possível exibir os termos de licença escolhendo o link **Termos de Licença** ao lado de cada componente. Escolha **Instalar** para adicionar os componentes e instalar o Visual Studio e o Visual C++ para Desenvolvimento Móvel Multiplataforma.

1. Quando a instalação for concluída, feche o instalador e reinicie o computador. Algumas ações de instalação dos componentes de terceiros não têm efeito até que o computador seja reiniciado.

   > [!IMPORTANT]
   > Você deve reiniciar para certificar-se de que tudo esteja instalado corretamente.

   Se a instalação do componente de Emulador do Microsoft Visual Studio para Android falhar, seu computador poderá não ter o Hyper-V habilitado. Use o aplicativo de Painel de Controle **Ativar ou desativar recursos do Windows** para habilitar o Hyper-V e execute o instalador do Visual Studio novamente.

   > [!NOTE]
   > Se o seu computador ou sua versão do Windows não der suporte ao Hyper-V, não será possível usar o componente de Emulador do Microsoft Visual Studio para Android. A Home Edition do Windows não inclui suporte para Hyper-V.

1. Abra o Visual Studio. Se esta for a primeira vez que você executa o Visual Studio, ele poderá levar algum tempo para ser configurado e se conectar. Quando o Visual Studio estiver pronto, no menu **Ferramentas**, selecione **Extensões e Atualizações**, **Atualizações**. Se houver atualizações do Visual Studio disponíveis para o Visual C++ para Desenvolvimento Móvel Multiplataforma ou para o Emulador do Microsoft Visual Studio para Android, instale-as.

## <a name="install-tools-for-ios"></a>Instalar as ferramentas para iOS

É possível usar o Visual C++ para Desenvolvimento Móvel Multiplataforma para editar, depurar e implantar código do iOS no Simulador de IOS ou em um dispositivo iOS, mas devido a restrições de licenciamento, o código deve ser compilado remotamente em um Mac. Para compilar e executar aplicativos iOS usando o Visual Studio, é necessário instalar e configurar o agente remoto em seu Mac. Para obter instruções detalhadas sobre a instalação, os pré-requisitos e as opções de configuração, confira [Instalar e configurar ferramentas de build usando o iOS](../cross-platform/install-and-configure-tools-to-build-using-ios.md). Se não estiver compilando para iOS, você poderá ignorar esta etapa.

## <a name="install-or-update-dependencies-manually"></a>Instalar ou atualizar as dependências manualmente

Se você optar por não instalar uma ou mais dependências de terceiros usando o Instalador do Visual Studio ao instalar a carga de trabalho **Desenvolvimento Mobile com C++** ( ou no Visual Studio 2015, a opção de Desenvolvimento Móvel do Visual C++), poderá instalá-las mais tarde usando as etapas em [Instalar as ferramentas](#install-the-tools). O Instalador do Visual Studio é atualizado regularmente para instalar os componentes mais recentes de produtos de terceiros. Você pode usá-lo para instalar SDKs e NDKs atualizados. Também é possível instalar ou atualizá-las independentemente do Visual Studio.

> [!CAUTION]
> Você pode instalar as dependências em qualquer ordem, exceto o Java. Você precisa instalar e configurar o JDK antes de instalar o SDK do Android.

Leia as informações a seguir e use estes links para instalar as dependências manualmente.

- [Java SE Development Kit](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

   Por padrão, o instalador coloca as ferramentas Java em *C:\Arquivos de Programas (x86)\Java*.

- [SDK do Android](https://developer.android.com/sdk/index.html#command-tools)

   Durante a instalação, atualize as APIs conforme recomendado. Pelo menos o SDK para o Android 5.0 Lollipop (nível de API 21) deve estar instalado. Por padrão, o instalador coloca o SDK do Android em *C:\Arquivos de Programas (x86)\Android\android-sdk*.

   É possível executar o aplicativo Gerenciador de SDK no diretório de SDK do Android novamente para atualizar o SDK e instalar ferramentas opcionais e níveis de API adicionais. A instalação das atualizações pode falhar, a menos que você use **Executar como administrador** para executar o aplicativo Gerenciador de SDK. Se tiver problemas ao compilar um aplicativo Android, verifique o Gerenciador de SDK quanto a atualizações para seus SDKs instalados.

   Para usar alguns dos emuladores de Android que vêm com o SDK do Android, você precisa instalar os drivers opcionais do Intel HAXM. Talvez você precise remover o recurso Hyper-V do Windows para instalar os drivers do Intel HAXM com êxito. Você precisa restaurar o recurso Hyper-V para usar os emuladores do Windows Phone e o Emulador do Microsoft Visual Studio para Android. Para obter mais informações, confira [Aceleração de hardware do Android Emulator](https://docs.microsoft.com/xamarin/android/get-started/installation/android-emulator/hardware-acceleration?tabs=vswin).

- [NDK do Android](https://developer.android.com/tools/sdk/ndk/index.html)

   Por padrão, o instalador coloca o NDK do Android em *C:\ProgramData\Microsoft\AndroidNDK*. Você pode baixar e instalar o NDK do Android novamente para atualizar a instalação do NDK.

- [Apache Ant](https://ant.apache.org/bindownload.cgi)

   Por padrão, o instalador coloca o Apache Ant em *C:\Arquivos de Programas (x86)\Microsoft Visual Studio 14.0\Apps*.

- [Emulador do Microsoft Visual Studio para Android](https://aka.ms/vscomemudownload)

   O Emulador do Microsoft Visual Studio para Android é um emulador opcional útil para testar e depurar seu código. Após o lançamento do Visual Studio Emulator para Android, o Google atualizou o Android Emulator para usar a aceleração de hardware por meio do HAXM da Intel. Recomendamos o uso do emulador acelerado do Google quando possível, pois ele oferece acesso às imagens de sistema operacional mais recentes do Android e serviços do Google Play.

Na maioria dos casos, o Visual Studio detecta as configurações do software de terceiros que você instalou e mantém os caminhos de instalação em variáveis de ambiente internas. É possível substituir os caminhos padrão dessas ferramentas de desenvolvimento de plataforma cruzada no IDE do Visual Studio.

#### <a name="to-set-the-paths-for-third-party-tools"></a>Para definir os caminhos para as ferramentas de terceiros

1. Na barra de menus do Visual Studio, selecione **Ferramentas** > **Opções**.

1. Na caixa de diálogo **Opções**, selecione **Multiplataforma** > **C++** > **Android**.

   ![Opções de caminho da ferramenta Android](../cross-platform/media/cppmdd_options_android.PNG "CPPMDD_Options_Android")

1. Para alterar o caminho usado por uma ferramenta, marque a caixa de seleção ao lado do caminho e edite o caminho da pasta na caixa de texto. Você também pode usar o botão Procurar (**...** ) para abrir uma caixa de diálogo **Selecionar local** para escolher a pasta.

1. Escolha **OK** para salvar os locais de pasta da ferramenta personalizada.

## <a name="see-also"></a>Consulte também

- [Instalar e configurar ferramentas de build usando o iOS](install-and-configure-tools-to-build-using-ios.md)
- [Visual C++ para desenvolvimento móvel multiplataforma](https://go.microsoft.com/fwlink/p/?LinkId=536383)
