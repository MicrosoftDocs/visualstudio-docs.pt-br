---
title: Criar um aplicativo de Atividade Nativa do Android | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-mobile
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 884014b1-5208-45ec-b0da-ad0070d2c24d
author: corob-msft
ms.author: corob
manager: douge
ms.workload:
- xplat-cplusplus
ms.openlocfilehash: 0b8a2622c0b4d55376ecb0f3bc6641d41c524962
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49845411"
---
# <a name="create-an-android-native-activity-app"></a>Criar um aplicativo de Atividade Nativa do Android
Ao instalar o Visual C++ para a opção de Desenvolvimento Móvel Multiplataforma, o Visual Studio 2015 pode ser usado para criar aplicativos de Atividade Nativa do Android totalmente funcionais. O NDK (Kit de Desenvolvimento Nativo) do Android é um conjunto de ferramentas que permite implementar a maior parte de seu aplicativo Android usando um código C/C++ puro. Algum código JNI do Java atua como uma cola para permitir que o código C/C++ interaja com o Android. O NDK do Android introduziu a capacidade de criar aplicativos de Atividade Nativa com a API do Android Nível 9. O código de Atividade Nativa é popular para a criação de aplicativos de jogos e de uso intensivo de elementos gráficos que usam o Unreal Engine ou o OpenGL. Este tópico descreverá a criação de um aplicativo de Atividade Nativa simples que usa o OpenGL. Os tópicos adicionais descrevem o ciclo de vida do desenvolvedor referente à edição, build, depuração e implantação do código de Atividade Nativa.  
  
 [Requisitos](#req)   
 [Criar um novo projeto de Atividade Nativa](#Create)   
 [Compilar e executar o aplicativo de Atividade Nativa padrão do Android](#BuildHello)  
  
##  <a name="req"></a> Requisitos  
 Antes de criar um aplicativo de Atividade Nativa do Android, é necessário verificar se todos os requisitos do sistema foram atendidos e se a opção Desenvolvimento Móvel do Visual C++ foi instalada no Visual Studio 2015. Para obter mais informações, consulte [Instalar o Visual C++ para Desenvolvimento Móvel Multiplataforma](../cross-platform/install-visual-cpp-for-cross-platform-mobile-development.md). Verifique se os SDKs e as ferramentas de terceiros necessários estão incluídos na instalação e se o Emulador do Microsoft Visual Studio para Android está instalado.  
  
##  <a name="Create"></a> Criar um novo projeto de Atividade Nativa  
 Neste tutorial, primeiro você criará um novo projeto de Atividade Nativa do Android e, em seguida, compilará e executará o aplicativo padrão no Emulador do Visual Studio para Android.  
  
#### <a name="to-create-a-new-project"></a>Para criar um novo projeto  
  
1. Abra o Visual Studio. Na barra de menus, selecione **Arquivo** > **Novo** > **Projeto**.  
  
2. Na caixa de diálogo **Novo Projeto**, em **Modelos**, escolha **Visual C++** > **Multiplataforma** e, em seguida, escolha o modelo **Aplicativo de Atividade Nativa (Android)**.  
  
3. Nomeie o aplicativo como `MyAndroidApp` e, em seguida, escolha **OK**.  
  
    ![Criar um projeto de Atividade Nativa](../cross-platform/media/cppmdd_newproject.PNG "CppMDD_NewProject")  
  
    O Visual Studio cria a nova solução e abre o Gerenciador de Soluções.  
  
    ![Projeto de Atividade Nativa no Gerenciador de Soluções](../cross-platform/media/cppmdd_rc_na_solutionexp.PNG "CPPMDD_RC_NA_SolutionExp")  
  
   A nova solução de aplicativo de Atividade Nativa do Android inclui dois projetos:  
  
-   `MyAndroidApp.NativeActivity` contém as referências e o código de cola para que seu aplicativo seja executado como uma Atividade Nativa no Android. A implementação dos pontos de entrada do código de cola está em *main.cpp*. Os cabeçalhos pré-compilados estão em *pch.h*. Esse projeto de aplicativo de Atividade Nativa é compilado em um arquivo *.so* de biblioteca compartilhada que é obtido pelo projeto de Empacotamento.  
  
-   `MyAndroidApp.Packaging` cria o arquivo *.apk* para implantação em um emulador ou dispositivo Android. Isso contém os recursos e o arquivo *AndroidManifest.xml* no qual as propriedades do manifesto são definidas. Também contém o arquivo *build.xml* que controla o processo de build Ant. Ele é definido como o projeto de inicialização por padrão, para que possa ser implantado e executado diretamente no Visual Studio.  
  
##  <a name="BuildHello"></a> Compilar e executar o aplicativo de Atividade Nativa padrão do Android  
 Compile e execute o aplicativo gerado pelo modelo para verificar a instalação e a configuração. Para esse teste inicial, execute o aplicativo em um dos perfis de dispositivo instalados pelo Emulador do Visual Studio para Android. Se você preferir testar seu aplicativo em outro destino, poderá carregar o emulador de destino ou conectar o dispositivo ao computador.  
  
#### <a name="to-build-and-run-the-default-native-activity-app"></a>Para compilar e executar o aplicativo de Atividade Nativa padrão  
  
1.  Se ainda não estiver selecionado, escolha **x86** na lista suspensa **Plataformas da Solução**.  
  
     ![Seleção suspensa do x86 de Plataformas da Solução](../cross-platform/media/cppmdd_rc_na_solution_x86.png "CPPMDD_RC_NA_Solution_x86")  
  
     Se a lista **Plataformas da Solução** não estiver visível, escolha **Plataformas da Solução** na lista **Adicionar/Remover Botões** e, em seguida, escolha sua plataforma.  
  
2.  Na barra de menus, escolha **Compilar** > **Compilar Solução**.  
  
     A Janela de Saída exibe a saída do processo de build dos dois projetos na solução.  
  
3.  Escolha um dos perfis de Telefone Android do Emulador do VS (x86) como o destino de implantação.  
  
     Se você tiver instalado outros emuladores ou conectado um dispositivo Android, poderá escolhê-los na lista suspensa de destino de implantação.  
  
4.  Pressione **F5** para iniciar a depuração ou Shift+F5 para iniciar sem depuração.  
  
     Esta é a aparência do aplicativo padrão no Emulador do Visual Studio para Android.  
  
     ![O emulador que executa o aplicativo](../cross-platform/media/cppmdd_emulator_running_app.PNG "CppMDD_Emulator_Running_App")  
  
     O Visual Studio inicia o emulador, que leva alguns segundos para carregar e implantar o código. Quando o aplicativo tiver sido iniciado, você poderá definir pontos de interrupção e usar o depurador para executar o código em etapas, examinar os locais e inspecionar os valores.  
  
5.  Pressione **Shift**+**F5** para parar a depuração.  
  
     O emulador é um processo separado que continua sendo executado. É possível editar, compilar e implantar o código várias vezes no mesmo emulador.