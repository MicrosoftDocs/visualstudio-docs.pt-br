---
title: Instalar o Visual C++ para Desenvolvimento Móvel de Multiplataforma | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- tgt-pltfrm-cross-plat
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- C++
ms.assetid: aaea6b8d-55eb-4427-8185-c050f855c257
caps.latest.revision: 17
author: corob-msft
ms.author: corob
manager: ghogen
ms.openlocfilehash: 0c8cbe8992a1035e2fb4a26feb9a77b5546bfa56
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51786009"
---
# <a name="install-visual-c-for-cross-platform-mobile-development"></a>Instalar o Visual C++ para Desenvolvimento Móvel Multiplataforma
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Visual C++ para desenvolvimento móvel de plataforma cruzada] (http://go.microsoft.com/fwlink/p/?LinkId=536383) é um componente instalável do Visual Studio 2015. Ele inclui modelos de plataforma cruzada do Visual Studio e instala as ferramentas e SDKs de plataforma cruzada para começar rapidamente, sem a necessidade de localizar, baixar e configurá-los. É possível usar essas ferramentas no Visual Studio para criar, editar, depurar e testar projetos de plataforma cruzada com facilidade. Este tópico descreve como instalar as ferramentas e softwares de terceiros necessários para desenvolver aplicativos de plataforma cruzada usando o Visual Studio. Para obter uma visão geral do componente, consulte [Visual C++ Móvel de Multiplataforma](http://go.microsoft.com/fwlink/p/?LinkId=536387)  
  
 [Requisitos](#Requirements)   
 [Obter as ferramentas](#GetTheTools)   
 [Instalar as ferramentas](#InstallTheTools)   
 [Instalar ferramentas para iOS](#InstallForiOS)   
 [Instalar ou atualizar as dependências manualmente](#ThirdParty)  
  
##  <a name="Requirements"></a> Requisitos  
  
- Para ver os requisitos de instalação, consulte [Requisitos de sistema do Visual Studio 2015](https://www.visualstudio.com/visual-studio-2015-system-requirements-vs).  
  
  > [!IMPORTANT]
  >  Se estiver usando o Windows 7 ou o Windows Server 2008 R2, você poderá desenvolver código para aplicativos clássicos do Windows, bibliotecas e aplicativos do tipo Native Acivity do Android e aplicativos e bibliotecas de código para iOS, mas não aplicativos para a Windows Store ou aplicativos universais do Windows.  
  
  Para compilar aplicativos para plataformas de dispositivo específicas, há alguns requisitos adicionais:  
  
- Emuladores do Windows Phone e o Emulador do Microsoft Visual Studio para Android requerem um computador que possa executar o Hyper-V. O recurso do Hyper-V do Windows deve ser habilitado antes que você possa instalar e executar os emuladores. Para obter mais informações, consulte os [requisitos de sistema](http://msdn.microsoft.com/en-us/4d5bb438-231a-4cd2-84b7-e9660b0e3baf) do emulador.  
  
- Os emuladores de Android x86 que vêm com o SDK do Android funcionam melhor em computadores que executam o driver Intel HAXM. Este driver requer um processador Intel x64 com VT-x e suporte para Execute Disable Bit. Para obter mais informações, consulte [Installation Instructions for Intel® Hardware Accelerated Execution Manager - Microsoft Windows](http://go.microsoft.com/fwlink/p/?LinkId=536385) (Instruções para instalação do Intel® Hardware Accelerated Execution Manager – Microsoft Windows).  
  
- Compilar código para iOS requer uma Apple ID, uma conta do Programa de Desenvolvedores de iOS e um computador Mac que possa executar o [Xcode 6](http://go.microsoft.com/fwlink/p/?LinkId=536387) ou posterior versões OS X Mavericks ou posteriores. Para ver etapas de instalação simples, consulte [Instalar ferramentas para iOS](#InstallForiOS).  
  
##  <a name="GetTheTools"></a> Obter as ferramentas  
 O Visual C++ para Desenvolvimento Móvel de Multiplataforma é um componente instalável incluído nas edições Enterprise, Professional e Community do Visual Studio. Para obter o Visual Studio, vá até a página de [Downloads do Visual Studio 2015](http://go.microsoft.com/fwlink/p/?linkid=517106) e baixe o Visual Studio 2015 com a Atualização 2 ou posterior.  
  
##  <a name="InstallTheTools"></a> Instalar as ferramentas  
 O instalador do Visual Studio 2015 inclui uma opção para instalar o Visual C++ para Desenvolvimento Móvel de Multiplataforma. Isso instala os modelos, componentes e ferramentas de linguagem C++ necessários para o Visual Studio, os conjuntos de ferramentas GCC e Clang necessários para compilação e depuração de Android, e componentes para se comunicar com um Mac para desenvolvimento de iOS. Ele também instala todas as ferramentas de terceiros e kits de desenvolvimento de software que são necessários para dar suporte ao desenvolvimento de aplicativos Android e iOS. A maioria dessas ferramentas de terceiros são softwares livres necessários para dar suporte à plataforma Android.  
  
-   O NDK (Kit de Desenvolvimento Nativo) do Android é necessário para compilar código C++ que se destina à plataforma Android.  
  
-   O SDK do Android, o Apache Ant e o Java SE Development Kit são necessários para o processo de build do Android.  
  
-   O Emulador do Microsoft Visual Studio para Android é um emulador de alto desempenho opcional útil para testar e depurar seu código.  
  
#### <a name="to-install-visual-c-for-cross-platform-mobile-development-and-the-third-party-tools"></a>Para instalar o Visual C++ para Desenvolvimento Móvel de Multiplataforma e as ferramentas de terceiros  
  
1.  Execute o instalador do Visual Studio 2015 que você baixou seguindo o link [Obter as ferramentas](#GetTheTools). Para instalar componentes opcionais, escolha **Personalizado** como o tipo de instalação. Escolha **Avançar** para selecionar os componentes opcionais a serem instalados.  
  
2.  Em Selecionar recursos, expanda **Desenvolvimento Móvel de Multiplataforma** e marque **Desenvolvimento Móvel no Visual C++**.  
  
     ![Selecionar Desenvolvimento Móvel no Visual C&#43;&#43;](../cross-platform/media/cppmdd-install-vcmdd.png "CPPMDD_Install_VCMDD")  
  
     Por padrão, quando você seleciona **Desenvolvimento Móvel no Visual C++**, a opção **Linguagens de Programação** é configurada para instalar o **Visual C++** e as opções **Ferramentas comuns e Software Development Kits** são configuradas para instalar componentes de terceiros exigidos. Você pode escolher componentes adicionais se precisar deles. Por padrão, o **Emulador do Microsoft Visual Studio para Android** também é selecionado. Componentes que já estão instalados aparecem inativos na lista.  
  
     Para compilar aplicativos universais do Windows e compartilhar código entre eles e seus projetos Android e iOS, em **Selecionar recursos**, expanda **Desenvolvimento no Windows e na Web** e marque **Ferramentas de Desenvolvimento de Aplicativo Universal do Windows**. Se não planejar compilar aplicativos universais do Windows, você poderá ignorar essa opção.  
  
     Escolha **Avançar** para continuar.  
  
3.  Os componentes de terceiros têm seus próprios termos de licença. É possível exibir os termos de licença escolhendo o link **Termos de Licença** ao lado de cada componente. Escolha **Instalar** para adicionar os componentes e instalar o Visual Studio e o Visual C++ para Desenvolvimento Móvel Multiplataforma.  
  
4.  Quando a instalação for concluída, feche o instalador e reinicie o computador. Algumas ações de instalação dos componentes de terceiros não têm efeito até que o computador seja reiniciado.  
  
    > [!IMPORTANT]
    >  Você deve reiniciar para certificar-se de que tudo esteja instalado corretamente.  
  
     Se a instalação do componente de Emulador do Microsoft Visual Studio para Android falhar, seu computador poderá não ter o Hyper-V habilitado. Use o aplicativo de Painel de Controle **Ativar ou desativar recursos do Windows** para habilitar o Hyper-V e execute o instalador do Visual Studio novamente.  
  
    > [!NOTE]
    >  Se o seu computador ou sua versão do Windows não der suporte ao Hyper-V, não será possível usar o componente de Emulador do Microsoft Visual Studio para Android. A Home Edition do Windows não inclui suporte para Hyper-V.  
  
5.  Abra o Visual Studio. Se esta for a primeira vez que você executa o Visual Studio, ele poderá levar algum tempo para ser configurado e se conectar. Quando o Visual Studio estiver pronto, no menu **Ferramentas**, selecione **Extensões e Atualizações**, **Atualizações**. Se houver atualizações do Visual Studio disponíveis para o Visual C++ para Desenvolvimento Móvel Multiplataforma ou para o Emulador do Microsoft Visual Studio para Android, instale-as.  
  
##  <a name="InstallForiOS"></a> Instalar ferramentas para iOS  
 É possível usar o Visual C++ para Desenvolvimento Móvel Multiplataforma para editar, depurar e implantar código do iOS no Simulador de IOS ou em um dispositivo iOS, mas devido a restrições de licenciamento, o código deve ser compilado remotamente em um Mac. Para compilar e executar aplicativos iOS usando o Visual Studio, é necessário instalar e configurar o agente remoto em seu Mac. Para obter instruções detalhadas sobre a instalação, pré-requisitos e opções de configuração, consulte [Instalar e configurar ferramentas para compilar usando iOS](../cross-platform/install-and-configure-tools-to-build-using-ios.md). Se não estiver compilando para iOS, você poderá ignorar esta etapa.  
  
##  <a name="ThirdParty"></a> Instalar ou atualizar as dependências manualmente  
 Se você optar por não instalar uma ou mais dependências de terceiros usando o instalador do Visual Studio quando instalar a opção de Desenvolvimento Móvel do Visual C++, você poderá instalá-las mais tarde usando as etapas em [Instalar as ferramentas](#InstallTheTools). Também é possível instalar ou atualizá-las independentemente do Visual Studio.  
  
> [!CAUTION]
>  Você pode instalar as dependências em qualquer ordem, exceto o Java. Você precisa instalar e configurar o JDK antes de instalar o SDK do Android.  
  
 Leia as informações a seguir e use estes links para instalar as dependências manualmente.  
  
- [Java SE Development Kit](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)  
  
   Por padrão, o instalador coloca as ferramentas Java em C:\Arquivos de Programas (x86) \Java.  
  
- [SDK do Android](https://developer.android.com/sdk/index.html#Other)  
  
   Durante a instalação, atualize as APIs conforme recomendado. Pelo menos o SDK para o Android 5.0 Lollipop (nível de API 21) deve estar instalado. Por padrão, o instalador coloca o SDK do Android em C:\Arquivos de Programas (x86) \Android\android-sdk.  
  
   É possível executar o aplicativo Gerenciador de SDK no diretório de SDK do Android novamente para atualizar o SDK e instalar ferramentas opcionais e níveis de API adicionais. A instalação das atualizações pode falhar, a menos que você use **Executar como administrador** para executar o aplicativo Gerenciador de SDK. Se tiver problemas ao compilar um aplicativo Android, verifique o Gerenciador de SDK quanto a atualizações para seus SDKs instalados.  
  
   Para usar alguns dos emuladores de Android que vêm com o SDK do Android, você precisa instalar os drivers opcionais do Intel HAXM. Talvez você precise remover o recurso Hyper-V do Windows para instalar os drivers do Intel HAXM com êxito. Você precisa restaurar o recurso Hyper-V para usar os emuladores do Windows Phone e o Emulador do Microsoft Visual Studio para Android.  
  
- [NDK do Android](https://developer.android.com/tools/sdk/ndk/index.html)  
  
   Por padrão, o instalador coloca o NDK do Android em C:\ProgramData\Microsoft\AndroidNDK. Você pode baixar e instalar o NDK do Android novamente para atualizar a instalação do NDK.  
  
- [Apache Ant](http://ant.apache.org/bindownload.cgi)  
  
   Por padrão, o instalador coloca o Apache Ant em C:\Arquivos de Programas (x86)\Microsoft Visual Studio 14.0\Apps.  
  
- [Emulador do Microsoft Visual Studio para Android](http://go.microsoft.com/fwlink/p/?LinkId=536390)  
  
   Você pode instalar e atualizar o Emulador do Microsoft Visual Studio para Android da Galeria do Visual Studio.  
  
  Na maioria dos casos, o Visual Studio detecta as configurações do software de terceiros que você instalou e mantém os caminhos de instalação em variáveis de ambiente internas. É possível substituir os caminhos padrão dessas ferramentas de desenvolvimento de plataforma cruzada no IDE do Visual Studio.  
  
#### <a name="to-set-the-paths-for-third-party-tools"></a>Para definir os caminhos para as ferramentas de terceiros  
  
1.  Na barra de menus do Visual Studio, selecione **Ferramentas**, **Opções**.  
  
2.  Na caixa de diálogo **Opções**, expanda **Multiplataforma**, **C++** e selecione **Android**.  
  
     ![Opções de caminho da ferramenta Android](../cross-platform/media/cppmdd-options-android.PNG "CPPMDD_Options_Android")  
  
3.  Para alterar o caminho usado por uma ferramenta, marque a caixa de seleção ao lado do caminho e edite o caminho da pasta na caixa de texto. Você também pode usar o botão Procurar (**...** ) para abrir uma caixa de diálogo **Selecionar local** para escolher a pasta.  
  
4.  Escolha **OK** para salvar os locais de pasta da ferramenta personalizada.  
  
## <a name="see-also"></a>Consulte também  
 [Instalar e configurar ferramentas para criação usando iOS](../cross-platform/install-and-configure-tools-to-build-using-ios.md)   
 [Visual C++ em plataforma cruzada móvel](https://www.visualstudio.com/explore/cplusplus-mdd-vs.aspx)

