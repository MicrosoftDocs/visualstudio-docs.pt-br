---
title: Compilar um aplicativo OpenGL ES em Android e iOS | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-mobile
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 76a67886-df57-4a81-accb-2e3c2eaf607b
author: corob-msft
ms.author: corob
manager: douge
ms.workload:
- xplat-cplusplus
ms.openlocfilehash: 59faf6a1995cefe84d7f1a00bd881f52a457b20d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49911857"
---
# <a name="build-an-opengl-es-application-on-android-and-ios"></a>Criar um aplicativo OpenGL ES no Android e iOS
Ao instalar a opção Visual C++ para Desenvolvimento Móvel Multiplataforma, você pode criar soluções e projetos do Visual Studio para aplicativos iOS e Android que compartilhem código comum. Este tópico o conduz pelo modelo de solução que cria tanto um aplicativo iOS simples quanto um aplicativo de Atividade Nativa do Android. Os aplicativos têm código C++ em comum que usa o OpenGL ES para exibir o mesmo cubo de rotação animado em cada plataforma. O OpenGL ES (GLES [OpenGL para Sistemas Incorporados]) é uma API gráfica 2D e 3D que tem suporte em vários dispositivos móveis.  
  
 [Requisitos](#req)   
 [Criar um novo projeto de Aplicativo OpenGLES](#Create)   
 [Compilar e executar o aplicativo Android](#BuildAndroid)   
 [Compilar e executar o aplicativo iOS](#BuildIOS)   
 [Personalizar seus aplicativos](#Customize)  
  
##  <a name="req"></a> Requisitos  
 Antes de criar um aplicativo OpenGL ES para iOS e Android, você precisará garantir que tenha atendido a todos os requisitos do sistema. Você deve instalar a opção o Visual C++ para Desenvolvimento Móvel Multiplataforma no Visual Studio 2015. Verifique se os SDKs e as ferramentas de terceiros necessários estão incluídos na instalação e se o Emulador do Visual Studio para Android está instalado. Para saber mais e obter instruções detalhadas, confira [Instalar o Visual C++ para desenvolvimento móvel de plataforma cruzada](../cross-platform/install-visual-cpp-for-cross-platform-mobile-development.md). Para compilar e testar o aplicativo iOS, você precisará de um computador Mac configurado de acordo com as instruções de instalação. Para saber mais sobre como configurar para desenvolvimento do iOS, confira [Instalar e configurar ferramentas para compilar usando iOS](../cross-platform/install-and-configure-tools-to-build-using-ios.md)  
  
##  <a name="Create"></a> Criar um novo projeto de Aplicativo OpenGLES  
 Neste tutorial, primeiro você criará um novo projeto de Aplicativo OpenGL ES e, em seguida, compilará e executará o aplicativo padrão no Emulador do Visual Studio para Android. Em seguida, compilará o aplicativo para iOS e executará o aplicativo no simulador de iOS.  
  
#### <a name="to-create-a-new-project"></a>Para criar um novo projeto  
  
1. Abra o Visual Studio. Na barra de menus, escolha **Arquivo**, **Novo**, **Projeto**.  
  
2. Na caixa de diálogo **Novo Projeto**, em **Modelos**, escolha **Visual C++**, **Multiplataforma** e, em seguida, escolha o modelo **Aplicativo OpenGLES (Android, iOS)**.  
  
3. Nomeie o aplicativo como `MyOpenGLESApp` e, em seguida, escolha **OK**.  
  
    ![Novo projeto de Aplicativo OpenGLES](../cross-platform/media/cppmdd_opengles_newproj.PNG "CPPMDD_OpenGLES_NewProj")  
  
    O Visual Studio cria a nova solução e abre o Gerenciador de Soluções.  
  
    ![MyOpenGLESApp no Gerenciador de Soluções](../cross-platform/media/cppmdd_opengles_solexpl.PNG "CPPMDD_OpenGLES_SolExpl")  
  
   A nova solução de Aplicativo OpenGL ES inclui três projetos de biblioteca e dois projetos de aplicativo. A pasta de Bibliotecas inclui um projeto de código compartilhado e dois projetos específicos da plataforma que fazem referência ao código compartilhado:  
  
- `MyOpenGLESApp.Android.NativeActivity` contém as referências e o código de cola que implementa seu aplicativo como uma Atividade Nativa no Android. A implementação dos pontos de entrada do código de associação está em *main.cpp*, que inclui o código compartilhado comum em `MyOpenGLESApp.Shared`. Os cabeçalhos pré-compilados estão em *pch.h*. Esse projeto de aplicativo de Atividade Nativa é compilado em um arquivo (*.so*) de biblioteca compartilhada que é obtido pelo projeto de `MyOpenGLESApp.Android.Packaging`.  
  
- `MyOpenGLESApp.iOS.StaticLibrary` cria um arquivo (*.a*) da biblioteca estática do iOS que contém o código compartilhado no `MyOpenGLESApp.Shared`. Ele está vinculado ao aplicativo criado pelo projeto `MyOpenGLESApp.iOS.Application`.  
  
- `MyOpenGLESApp.Shared` contém o código compartilhado que funciona em várias plataformas. Ele utiliza macros de pré-processador para compilação condicional do código específico da plataforma. O código compartilhado é escolhido pela referência de projeto no `MyOpenGLESApp.Android.NativeActivity` e no `MyOpenGLESApp.iOS.StaticLibrary`.  
  
  A solução tem dois projetos para compilar aplicativos para as plataformas Android e iOS:  
  
- `MyOpenGLESApp.Android.Packaging` cria o arquivo *.apk* para implantação em um emulador ou dispositivo Android. Isso contém os recursos e o arquivo AndroidManifest.xml no qual as propriedades do manifesto são definidas. Também contém o arquivo *build.xml* que controla o processo de build Ant. Ele é definido como o projeto de inicialização por padrão, para que possa ser implantado e executado diretamente no Visual Studio.  
  
- **MyOpenGLESApp.iOS.Application** contém os recursos e o código de associação Objective-C para criar um aplicativo iOS vinculado ao código de biblioteca estática C++ em `MyOpenGLESApp.iOS.StaticLibrary`. Esse projeto cria um pacote de build que é transferido para seu Mac pelo Visual Studio e pelo agente remoto. Quando você compila este projeto, o Visual Studio envia os arquivos e os comandos para compilar e implantar seu aplicativo no Mac.  
  
##  <a name="BuildAndroid"></a> Compilar e executar o aplicativo Android  
 A solução criada pelo modelo define o aplicativo Android como o projeto padrão.  Você pode compilar e executar esse aplicativo para verificar sua instalação e configuração. Para um teste inicial, execute o aplicativo em um dos perfis de dispositivo instalados pelo Emulador do Visual Studio para Android. Se você preferir testar seu aplicativo em outro destino, poderá carregar o emulador de destino ou conectar o dispositivo ao computador.  
  
#### <a name="to-build-and-run-the-android-native-activity-app"></a>Para compilar e executar o aplicativo de Atividade Nativa Android  
  
1. Se ainda não estiver selecionado, escolha **x86** na lista suspensa **Plataformas da Solução**.  
  
    ![Definir a Plataforma de Solução como x86](../cross-platform/media/cppmdd_opengles_solutionplat.png "CPPMDD_OpenGLES_SolutionPlat")  
  
    Use x86 para ter o Emulador do Android para Windows como destino. Se você tiver um dispositivo como destino, escolha a plataforma de solução com base no processador do dispositivo. Se a lista **Plataformas da Solução** não for exibida, escolha **Plataformas da Solução** na lista **Adicionar/Remover Botões** e, em seguida, escolha sua plataforma.  
  
2. No **Gerenciador de Soluções**, abra o menu de atalho do projeto `MyOpenGLESApp.Android.Packaging` e, em seguida, escolha **Compilar**.  
  
    ![Compilar um projeto de empacotamento Android](../cross-platform/media/cppmdd_opengles_andbuild.png "CPPMDD_OpenGLES_AndBuild")  
  
    A janela Saída exibe a saída do processo de build para a biblioteca compartilhado Android e o aplicativo Android.  
  
    ![Saída de build para projetos Android](../cross-platform/media/cppmdd_opengles_andoutput.png "CPPMDD_OpenGLES_AndOutput")  
  
3. Escolha um dos perfis de Telefone Android do Emulador do VS (x86) como o destino de implantação.  
  
    ![Escolha o destino da implantação](../cross-platform/media/cppmdd_opengles_pickemulator.png "CPPMDD_OpenGLES_PickEmulator")  
  
    Se você tiver instalado outros emuladores ou conectado um dispositivo Android, poderá escolhê-los na lista suspensa de destino de implantação. Para executar o aplicativo, a Plataforma de Solução compilada deverá corresponder à plataforma do dispositivo de destino.  
  
4. Pressione F5 para iniciar a depuração ou Shift+F5 para iniciar sem depuração.  
  
    O Visual Studio inicia o emulador, que leva vários segundos para carregar e implantar o código. É assim que o aplicativo aparece no Emulador do Visual Studio para Android.  
  
    ![Aplicativo em execução no Emulador do Android](../cross-platform/media/cppmdd_opengles_andemulator.png "CPPMDD_OpenGLES_AndEmulator")  
  
    Quando o aplicativo tiver sido iniciado, você poderá definir pontos de interrupção e usar o depurador para executar o código em etapas, examinar os locais e inspecionar os valores.  
  
5. Pressione **Shift**+**F5** para parar a depuração.  
  
    O emulador é um processo separado que continua sendo executado. É possível editar, compilar e implantar o código várias vezes no mesmo emulador. Seu aplicativo aparece na coleção de aplicativo no emulador e pode ser iniciado diretamente de lá.  
  
   Os projetos de biblioteca e o aplicativo de Atividade Nativa do Android gerados colocam o código C++ compartilhados em uma biblioteca dinâmica que inclui o código de "associação" para fazer interface com a plataforma Android. Isso significa que a maioria do código do aplicativo está na biblioteca e o manifesto, os recursos e as instruções de build estão no projeto de empacotamento. O código compartilhado é chamado de main.cpp no projeto NativeActivity. Para obter mais informações sobre como programar uma Atividade Nativa do Android, consulte a página [Conceitos](https://developer.android.com/ndk/guides/concepts.html) do NDK do Android Developer.  
  
   O Visual Studio compila projetos de Atividade Nativa do Android usando o NDK do Android, que usa Clang como o conjunto de ferramentas de plataforma. O Visual Studio mapeia as propriedades no projeto NativeActivity para as opções de linha de comando e as opções usadas para compilar, vincular e depurar na plataforma de destino. Para obter detalhes, abra a caixa de diálogo **Páginas de Propriedade** para o projeto MyOpenGLESApp.Android.NativeActivity. Para obter mais informações sobre as opções de linha de comando, consulte o [Manual do usuário do compilador Clang](http://clang.llvm.org/docs/UsersManual.html).  
  
##  <a name="BuildIOS"></a> Compilar e executar o aplicativo iOS  
 O projeto de aplicativo iOS é criado e editado no Visual Studio, porém, devido a restrições de licença, deve ser compilado e implantado em um Mac. O Visual Studio comunica-se com um agente remoto em execução no Mac para transferir arquivos de projeto e executar comandos de build, implantação e depuração. Você deve instalar e configurar seu Mac e o Visual Studio para comunicação antes de compilar o aplicativo iOS. Para obter instruções detalhadas, confira [Instalar e configurar as ferramentas para compilar usando iOS](../cross-platform/install-and-configure-tools-to-build-using-ios.md). Depois que o agente remoto estiver em execução e o Visual Studio estiver emparelhado com o Mac, você poderá compilar e executar o aplicativo do iOS para verificar sua instalação e configuração.  
  
#### <a name="to-build-and-run-the-ios-app"></a>Para compilar e executar o aplicativo iOS  
  
1. Verifique se o agente remoto está em execução no seu Mac e se o Visual Studio está emparelhado com o agente remoto. Para iniciar o agente remoto, abra uma janela do aplicativo Terminal e digite `vcremote`. Para obter mais informações, consulte [Configurar o agente remoto no Visual Studio](../cross-platform/install-and-configure-tools-to-build-using-ios.md#ConfigureVS).  
  
    ![Janela do Terminal Mac executando vcremote](../cross-platform/media/cppmdd_common_vcremote.png "CPPMDD_common_vcremote")  
  
2. Se ainda não estiver selecionado, escolha **x86** na lista suspensa **Plataformas da Solução**.  
  
    ![Definir a Plataforma de Solução como x86](../cross-platform/media/cppmdd_opengles_solutionplat.png "CPPMDD_OpenGLES_SolutionPlat")  
  
    Use x86 para ter o Simulador de iOS como destino. Se você tiver um dispositivo iOS como destino, escolha a plataforma da solução com base no processador do dispositivo (normalmente, um processador ARM). Se a lista **Plataformas da Solução** não for exibida, escolha **Plataformas da Solução** na lista **Adicionar/Remover Botões** e, em seguida, escolha sua plataforma.  
  
3. No Gerenciador de Soluções, abra o menu de atalho para o projeto MyOpenGLESApp.iOS.Application e escolha **Compilar**.  
  
    ![Compilar o projeto de Aplicativo iOS](../cross-platform/media/cppmdd_opengles_iosbuild.png "CPPMDD_OpenGLES_iOSBuild")  
  
    A janela Saída exibe a saída do processo de build para a biblioteca estática do iOS e o aplicativo iOS. No Mac, a janela Terminal executando o agente remoto mostra a atividade de comando e transferência de arquivo.  
  
    No computador Mac, você será solicitado a aceitar uma solicitação de assinatura de código. Escolha **Permitir** para continuar.  
  
4. Escolha **Simulador de iOS** na barra de ferramentas para executar o aplicativo no Simulador de iOS no Mac. Pode demorar um pouco para o simulador ser iniciado. Poderá ser necessário trazer o simulador para o primeiro plano no Mac para ver a saída dele.  
  
    ![Aplicativo em execução no Simulador de iOS](../cross-platform/media/cppmdd_opengles_iossimulator.png "CPPMDD_OpenGLES_iOSSimulator")  
  
    Quando seu aplicativo tiver sido iniciado, você poderá definir pontos de interrupção e usar o depurador do Visual Studio para examinar locais, consultar a pilha de chamadas e inspecionar os valores.  
  
    ![Depurador no ponto de interrupção no aplicativo iOS](../cross-platform/media/cppmdd_opengles_iosdebug.png "CPPMDD_OpenGLES_iOSDebug")  
  
5. Pressione **Shift**+**F5** para parar a depuração.  
  
    O Simulador de iOS é um processo separado que continua a ser executado no Mac. É possível editar, compilar e implantar o código várias vezes para a mesma instância do Simulador de iOS. Você também pode executar o código diretamente no simulador após ele ter sido implantado.  
  
   Os projetos de aplicativo e biblioteca do iOS gerados colocam o código C++ em uma biblioteca estática que implementa somente o código compartilhado. A maior parte do código do aplicativo esta no projeto de `Application`. As chamadas para o código de biblioteca compartilhada neste projeto de modelo são feitas no arquivo *GameViewController.m*. Para compilar seu aplicativo iOS, o Visual Studio usa o conjunto de ferramentas de plataforma do Xcode, que exige a comunicação com um cliente remoto em execução em um Mac.  
  
   O Visual Studio transfere os arquivos de projeto e envia comandos para o cliente remoto para compilar o aplicativo usando Xcode. O cliente remoto envia informações de status de build de volta ao Visual Studio. Quando o aplicativo tiver sido compilado com êxito, você poderá usar o Visual Studio para enviar comandos para executar e depurar o aplicativo. O depurador do Visual Studio controla o aplicativo em execução no Simulador de iOS em execução no Mac ou em um dispositivo iOS anexado. O Visual Studio mapeia as propriedades no projeto StaticLibrary para as opções de linha de comando e as opções usadas para compilar, vincular e depurar na plataforma iOS de destino. Para obter detalhes de opção de linha de comando do compilador, abra a caixa de diálogo **Páginas de Propriedade** para o projeto MyOpenGLESApp.iOS.StaticLibrary.  
  
##  <a name="Customize"></a> Personalizar seus aplicativos  
 Você pode modificar o código C++ compartilhado para adicionar ou alterar funcionalidade comum. Você deve alterar as chamadas para o código compartilhado para corresponder aos projetos `MyOpenGLESApp.Android.NativeActivity` e `MyOpenGLESApp.iOS.Application`. Você pode usar macros de pré-processador para especificar seções específicas de plataforma no seu código comum. A macro do pré-processador `__ANDROID__` é predefinida ao compilar para Android. A macro do pré-processador `__APPLE__` é predefinida ao compilar para iOS.  
  
 Para ver o IntelliSense para uma plataforma de projeto específica, escolha o projeto na lista suspensa do seletor de contexto na barra de Navegação na parte superior da janela do editor.  
  
 ![Lista suspensa do Seletor de Contexto do Projeto no Editor](../cross-platform/media/cppmdd_opengles_contextswitcher.png "CPPMDD_OpenGLES_ContextSwitcher")  
  
 Problemas do IntelliSense no projeto atual são marcados com uma linha ondulada vermelha. Problemas em outros projetos são marcados com uma linha ondulada roxa. Por padrão, o Visual Studio não dá suporte a coloração de código nem a arquivos IntelliSense para Java ou Objective-C. No entanto, você ainda pode modificar os arquivos de origem e alterar os recursos para definir o nome, o ícone e outros detalhes de implementação do aplicativo.