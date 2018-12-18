---
title: Iniciar uma sessão de depuração para um aplicativo da Store no Visual Studio (VB, c#, C++ e XAML) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VC.Project.IVCAppHostRemoteDebugPageObject.MachineName
- VC.Project.IVCAppHostRemoteDebugPageObject.BreakpointBehavior
- VC.Project.IVCAppHostLocalDebugPageObject.GPUDebuggerTargetType
- VC.Project.IVCAppHostTetheredDebugPageObject.DebuggerType
- VC.Project.IVCAppHostLocalDebugPageObject.BreakpointBehavior
- VC.Project.IVCAppHostRemoteDebugPageObject.LaunchApplication
- VC.Project.IVCAppHostRemoteDebugPageObject.GPUDebuggerTargetType
- VC.Project.IVCAppHostLocalDebugPageObject.DebuggerType
- VC.Project.IVCAppHostSimulatorDebugPageObject.DebuggerType
- ImmersiveProjects.Properties.Debug
- VC.Project.IVCAppHostTetheredDebugPageObject.LaunchApplication
- VC.Project.IVCAppHostSimulatorDebugPageObject.LaunchApplication
- VC.Project.IVCAppHostSimulatorDebugPageObject.GPUDebuggerTargetType
- VC.Project.IVCAppHostLocalDebugPageObject.LaunchApplication
- VC.Project.IVCAppHostLocalDebugPageObject.AllowLocalNetworkLoopback
- AppPackage.Properties.Debug
- VC.Project.IVCAppHostRemoteDebugPageObject.Authentication
- VC.Project.IVCAppHostRemoteDebugPageObject.DebuggerType
- VC.Project.IVCAppHostSimulatorDebugPageObject.BreakpointBehavior
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 66ec0e79-8261-4c19-a618-3fd1b3f71bbd
caps.latest.revision: 23
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: cb49d00d069a86be83ec02b92efe4ac93fc706b3
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51802571"
---
# <a name="start-a-debugging-session-for-a-store-app-in-visual-studio-vb-c-c-and-xaml"></a>Iniciar uma sessão de depuração de um aplicativo da Store no Visual Studio (VB, C#, C++ e XAML)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Aplica-se ao Windows e Windows Phone] (... /Image/windows_and_phone_content.png "windows_and_phone_content")  

 Este tópico descreve como iniciar uma sessão de depuração para aplicativos da Windows Store escritos em XAML e Visual C++, Visual C# ou Visual Basic. Depurar um aplicativo envolve configurar a sessão de depuração e escolher a maneira de iniciar o aplicativo.  

> [!NOTE]
>  Para aplicativos escritos em JavaScript e HTML, consulte [iniciar uma sessão de depuração (JavaScript)](../debugger/start-a-debugging-session-for-store-apps-in-visual-studio-javascript.md).  

##  <a name="BKMK_In_this_topic"></a> Neste tópico  
 [A maneira fácil de iniciar a depuração](#BKMK_The_easy_way_to_start_debugging)  

 [Configurar a sessão de depuração](#BKMK_Configure_the_debugging_session)  

- [Abra a página de propriedades de depuração para o projeto](#BKMK_Open_the_debugging_property_page_for_the_project)  

- [Escolher opções de configuração de compilação](#BKMK_Choose_the_build_configuration_options)  

- [Escolha o destino de implantação](#BKMK_Choose_the_deployment_target)  

- [Escolha o depurador a ser usado](#BKMK_Choose_the_debugger_to_use)  

- [(Opcional) Atrasar o início de sessão de depuração](#BKMK__Optional__Delay_starting_the_debug_session)  

- [(Opcional) Desabilitar loopbacks de rede](#BKMK__Optional__Disable_network_loopbacks)  

- [(Opcional) Reinstale o aplicativo ao iniciar a depuração](#BKMK__Optional__Reinstall_the_app_when_you_start_debugging)  

- [(Opcional) Desabilitar a requisição de autenticação para iniciar o depurador remoto](#BKMK__Optional__Disable_authentication_requirement_to_start_the_remote_debugger)  

  [Iniciar a sessão de depuração](#BKMK_Start_the_debugging_session)  

- [Iniciar a depuração (F5)](#BKMK_Start_debugging__F5_)  

- [Iniciar a depuração (F5), mas atrasar o início do aplicativo](#BKMK_Start_debugging__F5__but_delay_the_app_start)  

- [Iniciar um aplicativo instalado no depurador](#BKMK_Start_an_installed_app_in_the_debugger)  

- [Anexar o depurador a um aplicativo em execução](#BKMK_Attach_the_debugger_to_a_running_app_)  

  -   [Defina o aplicativo seja executado no modo de depuração](#BKMK_Set_the_app_to_run_in_debug_mode)  

  -   [Anexar o depurador](#BKMK_Attach_the_debugger)  

##  <a name="BKMK_The_easy_way_to_start_debugging"></a> A maneira fácil de iniciar a depuração  

1. Abra a solução do aplicativo no Visual Studio.  

2. Selecione F5.  

   O Visual Studio compila e inicia o aplicativo com o depurador anexado. A execução continua até que um ponto de interrupção seja alcançado, você suspenda a execução manualmente, ocorra uma exceção sem tratamento ou o aplicativo chegue ao fim. Para obter mais informações, consulte [navegar por uma sessão de depuração (Xaml e c#)](../debugger/navigate-a-debugging-session-in-visual-studio-xaml-and-csharp.md) .  

##  <a name="BKMK_Configure_the_debugging_session"></a> Configurar a sessão de depuração  

###  <a name="BKMK_Open_the_debugging_property_page_for_the_project"></a> Abra a página de propriedades de depuração para o projeto  

1.  No Gerenciador de Soluções, selecione o projeto. No menu de atalho, escolha **propriedades**.  

2.  Faça isso para abrir a página de propriedades de depuração do projeto:  

    -   Para aplicativos do Visual c# e Visual Basic, escolha **depurar**.  

         ![C&#35; &#47; página de propriedades de depuração de projeto do VB](../debugger/media/dbg-csvb-debugpropertypage.png "DBG_CsVb_DebugPropertyPage")  

    -   Para aplicativos do Visual C++, expanda o **propriedades de configuração** nó e, em seguida, escolha **depuração**.  

         ![C&#43; &#43; página de propriedades de depuração do aplicativo de Windows Store](../debugger/media/dbg-cpp-debugpropertypage.png "DBG_CPP_DebugPropertyPage")  

###  <a name="BKMK_Choose_the_build_configuration_options"></a> Escolher opções de configuração de compilação  

1.  Dos **Configuration** , escolha **Debug** ou **(ativo) depurar**.  

2.  Do **plataforma** lista escolha para compilar para a plataforma de destino. Na maioria dos casos, **qualquer CPU** (**todas as plataformas** no Visual C++) é a melhor opção.  

###  <a name="BKMK_Choose_the_deployment_target"></a> Escolha o destino de implantação  
 ![Se aplica somente ao Windows](../debugger/media/windows-only-content.png "windows_only_content")  

 Você pode implantar e depurar um aplicativo da Windows Store no computador com Visual Studio, no simulador do Visual Studio no computador local ou em um dispositivo remoto.  

- Para aplicativos c# e Visual Basic, escolha o destino na **dispositivo de destino** lista os **depurar** página de propriedades para o projeto.  

- Para aplicativos em C++, escolha o destino do **depurador a iniciar** lista os **depuração** página de propriedades:  

  Escolha uma destas opções:  

|||  
|-|-|  
|**Computador local**|Depura o aplicativo na sessão atual no computador local. Ver [aplicativos de execução Windows Store na máquina local](../debugger/run-windows-store-apps-on-the-local-machine.md).|  
|**Simulador**|Depura o aplicativo no simulador do Visual Studio para aplicativos [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)]. O simulador é uma janela da área de trabalho que permite depurar recursos, como gestos de toque e rotação de dispositivos, que não estão disponíveis no computador local. Ver [aplicativos de execução Windows Store no simulador](../debugger/run-windows-store-apps-in-the-simulator.md).|  
|**Computador remoto**|Depura o aplicativo em um dispositivo conectado ao computador local por uma intranet ou diretamente por meio de um cabo Ethernet. Para depurar remotamente, as Ferramentas Remotas do Visual Studio devem estar instaladas e em execução no dispositivo remoto. Ver [aplicativos de execução Windows Store em um computador remoto](../debugger/run-windows-store-apps-on-a-remote-machine.md).|  

 Se você escolher **máquina remota**, especifique o nome ou endereço IP do computador remoto em uma das seguintes maneiras:  

- Digite o nome ou endereço IP do computador remoto.  

  -   Para aplicativos c# e Visual Basic, insira o nome ou endereço IP na **máquina remota** caixa.  

  -   Para aplicativos em C++, insira o nome ou endereço IP na **nome da máquina** caixa.  

- Escolha o computador remoto a partir de **Selecionar Conexão de depurador remoto** caixa de diálogo.  

   Para abrir a caixa de diálogo:  

  - Para aplicativos c# e Visual Basic, escolha **localizar**.  

  - Para aplicativos do C++, escolha a seta para baixo na **nome da máquina** caixa e escolha  **\<localizar... >**.  

    ![Marque a caixa de diálogo Conexão de depurador remoto](../debugger/media/vsrun-selectremotedebuggerdlg.png "VSRUN_SelectRemoteDebuggerDlg")  

  > [!NOTE]
  >  O **Selecionar Conexão de depurador remoto** caixa de diálogo exibe computadores que estão na sub-rede local e os computadores que estão diretamente conectados ao computador do Visual Studio por um cabo Ethernet. Para especificar outro computador, digite o nome na **nome da máquina** caixa.  

  ![Se aplica somente ao Windows Phone](../debugger/media/phone-only-content.png "phone_only_content")  

  Você pode implantar e depurar um aplicativo da Windows Phone Store em um dispositivo ou em um dos emuladores de telefone do Visual Studio. Selecione o dispositivo ou emulador dos **dispositivo de destino** lista.  

###  <a name="BKMK_Choose_the_debugger_to_use"></a> Escolha o depurador a ser usado  
 Por padrão, o Visual Studio depura o código gerenciado nos aplicativos em C# e Visual Basic.  

 Para aplicativos em C# e Visual Basic, você pode optar por depurar o código gerenciado e o código C/C++ nativo. Selecione o **habilitar a depuração de código não gerenciado** caixa de seleção para incluir o código nativo na sessão de depuração.  

 Por padrão, o Visual Studio depura o código nativo no aplicativo em C++.  

 Para aplicativos em C++, você pode escolher depurar tipos específicos de código que estão em componentes do seu aplicativo em vez do código nativo ou além dele. Especifique o código para depurar na **tipo de depurador** lista o **depuração** página de propriedades do projeto de aplicativo.  

 Escolha um destes depuradores do **processo de aplicativo** lista:  

|||  
|-|-|  
|**Somente script**|Depura o código JavaScript no aplicativo. O código gerenciado e o código nativo são ignorados.|  
|**Somente nativo**|Depura o código C/C++ nativo no aplicativo. O código gerenciado e o código JavaScript são ignorados.|  
|**Somente gerenciado**|Depura o código gerenciado no aplicativo. O código JavaScript e o código C/C++ nativo são ignorados.|  
|**Misto (gerenciado e nativo)**|Depura o código C/C++ nativo e o código gerenciado no aplicativo. O código JavaScript é ignorado.|  
|**Somente GPU**|Depurar o código C++ nativo que é executado em uma GPU (unidade de processamento gráfico).|  

 ![Se aplica somente ao Windows Phone](../debugger/media/phone-only-content.png "phone_only_content")  

 Para aplicativos da Windows Store Phone, você também pode escolher o depurador a ser usado para processos em segundo plano do **processo de tarefa em segundo plano**.  

###  <a name="BKMK__Optional__Delay_starting_the_debug_session"></a> (Opcional) Atrasar o início de sessão de depuração  
 Por padrão, o Visual Studio inicia o aplicativo imediatamente quando você começa a depuração. Você também pode iniciar uma sessão de depuração, mas atrasar o início do seu aplicativo. Quando você escolhe essa opção, o aplicativo é iniciado no depurador quando é executado na tela inicial ou por um contrato de ativação ou quando é iniciado por outro processo ou método. Você também atrasa o início do aplicativo quando deseja depurar uma tarefa em segundo plano quando o aplicativo em si não está em execução.  

 Para atrasar a inicialização do aplicativo, você pode fazer o seguinte:  

-   Para aplicativos do Visual c# e Visual Basic, selecione **não iniciar, mas depurar meu código quando ele é iniciado** sobre o **depurar** página de propriedades.  

-   Para aplicativos do Visual C++, escolha **Sim** da **Iniciar aplicativo** lista os **depuração** página de propriedades.  

###  <a name="BKMK__Optional__Disable_network_loopbacks"></a> (Opcional) Desabilitar loopbacks de rede  
 ![Se aplica somente ao Windows](../debugger/media/windows-only-content.png "windows_only_content")  

 Por motivos de segurança, um aplicativo da Windows Store instalado da maneira padrão não pode efetuar chamadas de rede para o dispositivo em que está instalado. Por padrão, a implantação do Visual Studio cria uma isenção dessa regra para o aplicativo implantado. Essa isenção permite que você teste procedimentos de comunicação em um único computador. Antes de enviar seu aplicativo para o Windows Store, você deve testá-lo sem a isenção.  

 Para remover a isenção de loopback de rede:  

-   Para aplicativos do Visual c# e Visual Basic, desmarque a **permitir Loopback de rede** caixa de seleção a **depurar** página de propriedades.  

-   Para aplicativos do Visual C++, escolha **não** da **permitir Loopback de rede** lista os **depuração** página de propriedades.  

###  <a name="BKMK__Optional__Reinstall_the_app_when_you_start_debugging"></a> (Opcional) Reinstale o aplicativo ao iniciar a depuração  
 Para diagnosticar problemas com a instalação e configuração inicial do seu aplicativo em Visual C# ou Visual Basic, escolha **desinstalar e reinstalar meu pacote** sobre o **depurar** página de propriedades para recriar um instalação original ao iniciar a depuração. Essa opção não está disponível para projetos do Visual C++.  

###  <a name="BKMK__Optional__Disable_authentication_requirement_to_start_the_remote_debugger"></a> (Opcional) Desabilitar a requisição de autenticação para iniciar o depurador remoto  
 ![Se aplica somente ao Windows](../debugger/media/windows-only-content.png "windows_only_content")  

 Por padrão, você deve fornecer credenciais para executar o depurador remoto.  

> [!IMPORTANT]
>  Você também pode optar por executar o depurador remoto no Modo Sem Autenticação, mas isso é altamente desaconselhável. Nesse modo não há nenhuma segurança de rede. Escolha o Modo Sem Autenticação somente se você tiver certeza de que a rede não corre risco de tráfego mal-intencionado ou hostil.  

 Para remover a requisição de autenticação:  

1. Para aplicativos do Visual c# e Visual Basic, desmarque a **usar autenticação do** caixa de seleção a **depurar** página de propriedades.  

2. Para aplicativos do Visual C++, escolha **não** da **exigir autenticação** lista os **depuração** página de propriedades.  

   [Neste tópico](#BKMK_In_this_topic)  

##  <a name="BKMK_Start_the_debugging_session"></a> Iniciar a sessão de depuração  

###  <a name="BKMK_Start_debugging__F5_"></a> Iniciar a depuração (F5)  
 Quando você escolhe **iniciar depuração** (teclado: F5) sobre o **depurar** menu, o Visual Studio inicia o aplicativo com o depurador anexado. A execução continua até que um ponto de interrupção seja alcançado, você suspenda a execução manualmente, ocorra uma exceção ou o aplicativo chegue ao fim.  

###  <a name="BKMK_Start_debugging__F5__but_delay_the_app_start"></a> Iniciar a depuração (F5), mas atrasar o início do aplicativo  
 Você pode definir que o aplicativo seja executado no modo de depuração, mas inicie-o por outro método que não seja o depurador. Por exemplo, convém depurar a inicialização do aplicativo no menu Iniciar ou depurar um processo em segundo plano do aplicativo sem iniciá-lo. Para atrasar o início do aplicativo, faça o seguinte:  

- Sobre o **Debugging** página de propriedades do aplicativo (**depurar** no Visual C++)  

  -   Para aplicativos do Visual c# e Visual Basic, escolha **não iniciar, mas depurar meu código quando iniciar**.  

  -   Para aplicativos do Visual C++, escolha **Yes** da **Iniciar aplicativo** lista.  

- Escolha **iniciar depuração** sobre o **depurar** menus (teclado: F5).  

- Inicie o aplicativo pelo menu Iniciar, por um contrato de execução ou por outro procedimento.  

  O aplicativo é iniciado no modo de depuração. A execução continua até que um ponto de interrupção seja alcançado, você suspenda a execução manualmente, ocorra uma exceção sem tratamento ou o aplicativo chegue ao fim.  

  . Para obter mais informações sobre como depurar tarefas em segundo plano, consulte [disparador de suspender, continuar e eventos para Windows Store em segundo plano)](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md).  

###  <a name="BKMK_Start_an_installed_app_in_the_debugger"></a> Iniciar um aplicativo instalado no depurador  
 Quando você inicia a depuração usando F5, o Visual Studio compila e implanta o aplicativo, define que ele seja executado no modo de depuração e, em seguida, inicia-o. Para iniciar um aplicativo que já está instalado em um dispositivo, use a caixa de diálogo Depurar Pacote do Aplicativo Instalado. Esse procedimento é útil quando você precisa depurar um aplicativo instalado da Windows Store ou quando você tem os arquivos de origem do aplicativo, mas não tem um projeto do Visual Studio para o aplicativo. Por exemplo, você pode ter um sistema de build personalizado que não use projetos ou soluções do Visual Studio.  

 O aplicativo pode ser instalado no dispositivo local ou pode estar localizado em um dispositivo remoto.  É possível iniciar o aplicativo imediatamente ou defini-lo para ser executado no depurador quando for iniciado por outro processo ou método, por exemplo, no menu Iniciar ou por um contrato de ativação. Você também pode definir o aplicativo para ser executado no modo de depuração quando quiser depurar um processo em segundo plano sem iniciar o aplicativo. Para obter mais informações, consulte [disparador de suspender, continuar e eventos para Windows Store em segundo plano)](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md).  

 Para definir um aplicativo instalado para ser executado no modo de depuração, faça o seguinte:  

> [!NOTE]
>  O aplicativo não deve estar em execução quando você iniciar este procedimento.  

1. Sobre o **Debug** menu, escolha **depurar pacote do aplicativo instalado**  

2. Escolha uma destas opções na lista:  


   |                    |                                                                                                                                                                                                                                                                                                                                                                                                           |
   |--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | **Computador local**  |                                                                                                                Depura o aplicativo na sessão atual no computador local. Ver [aplicativos de execução Windows Store na máquina local](../debugger/run-windows-store-apps-on-the-local-machine.md).                                                                                                                 |
   |   **Simulador**    | Depura o aplicativo no simulador do Visual Studio para aplicativos [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)]. O simulador é uma janela da área de trabalho que permite depurar recursos, como gestos de toque e rotação de dispositivos, que não estão disponíveis no computador local. Ver [aplicativos de execução Windows Store no simulador](../debugger/run-windows-store-apps-in-the-simulator.md). |
   | **Computador remoto** |                          Depura o aplicativo em um dispositivo conectado ao computador local por uma intranet ou diretamente por meio de um cabo Ethernet. Para depurar remotamente, as Ferramentas Remotas do Visual Studio devem estar instaladas e em execução no dispositivo remoto. Ver [aplicativos de execução Windows Store em um computador remoto](../debugger/run-windows-store-apps-on-a-remote-machine.md).                           |


3. Escolha o aplicativo do **pacotes de aplicativos instalado** lista.  

4. Escolha o mecanismo de depuração para usar a partir de **depurar esse tipo de código** lista.  

5. (Opcional). Escolher **não iniciar, mas depurar meu código quando iniciar** para depurar o aplicativo quando ele é iniciado por algum outro método, ou para depurar um processo em segundo plano.  

   Quando você clica em **iniciar**, o aplicativo é iniciado ou definido para ser executado no modo de depuração.  

###  <a name="BKMK_Attach_the_debugger_to_a_running_app_"></a> Anexar o depurador a um aplicativo em execução  
 Para anexar o depurador a um aplicativo [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)], você deve usar o Gerenciador de Pacotes Depuráveis para definir a execução do aplicativo no modo de depuração. Esse recurso é instalado com as Ferramentas Remotas do Visual Studio.  

 Anexar o depurador a um aplicativo é útil quando você precisa depurar um aplicativo já instalado; por exemplo, um que tenha sido instalado da [!INCLUDE[win8_appstore_long](../includes/win8-appstore-long-md.md)]. A anexação é necessária quando você tem os arquivos de origem do aplicativo, mas não tem um projeto do Visual Studio para ele. Por exemplo, você pode ter um sistema de build personalizado que não use projetos ou soluções do Visual Studio.  

 Para anexar o depurador a um aplicativo, são necessárias as seguintes etapas:  

1.  Defina o aplicativo para ser executado no modo de depuração. Isso deve ser feito quando o aplicativo não está em execução.  

2.  Inicie o aplicativo. Você pode fazer isso pela tela inicial, por um contrato de execução ou por outro método.  

3.  Anexe o depurador ao aplicativo em execução.  

####  <a name="BKMK_Set_the_app_to_run_in_debug_mode"></a> Defina o aplicativo seja executado no modo de depuração  

1.  Instale as Ferramentas Remotas do Visual Studio no dispositivo em que o aplicativo está instalado. Ver [instalando as ferramentas remotas](http://msdn.microsoft.com/library/windows/apps/hh441469.aspx#BKMK_Installing_the_Remote_Tools).  

2.  Na tela inicial, procure por `Debuggable Package Manager` e inicie-o.  

     É exibida uma janela do PowerShell corretamente configurada para o cmdlet AppxDebug.  

3.  Para habilitar a depuração de um aplicativo, é preciso especificar o identificador NomeCompletodoPacote do aplicativo. Para ver uma lista de todos os aplicativos que incluem o NomeCompletodoPacote, digite `Get-AppxPackage` no aviso do PowerShell.  

4.  No prompt do PowerShell, digite `Enable-AppxDebug` *PackageFullName* onde *PackageFullName* é o identificador PackageFullName do aplicativo.  

####  <a name="BKMK_Attach_the_debugger"></a> Anexar o depurador  
 Para anexar o depurador:  

1. Sobre o **Debug** menu, escolha **anexar ao processo**.  

    A caixa de diálogo **Anexar ao Processo** é exibida.  

2. Para anexar a um aplicativo em um dispositivo remoto, especifique o dispositivo remoto na **qualificador** caixa. Você pode:  

   -   Digite o nome na **qualificador** caixa.  

   -   Escolha a seta para baixo na **qualificador** caixa e, em seguida, escolha o dispositivo em uma lista de dispositivos que você já anexou antes.  

   -   Escolher **localizar** para selecionar o dispositivo em uma lista de dispositivos em sua sub-rede local.  

3. Especifique o tipo de código que você deseja depurar na **anexar a** caixa.  

    Escolher **selecionar** e, em seguida, faça o seguinte:  

   -   Escolha **determine automaticamente o tipo de código a ser depurado**  

   -   Escolher **depurar esses tipos de código** e, em seguida, escolha um ou mais tipos na lista.  

4. No **processos disponíveis** , escolha o processo do aplicativo.  

5. Escolher **anexar**.  

   O Visual Studio anexa o depurador ao processo. A execução continua até que um ponto de interrupção seja alcançado, você suspenda a execução manualmente, ocorra uma exceção sem tratamento ou o aplicativo chegue ao fim.  

   [Neste tópico](#BKMK_In_this_topic)  

## <a name="see-also"></a>Consulte também  
 [Depurar aplicativos no Visual Studio](../debugger/debug-store-apps-in-visual-studio.md)   
 [Navegar em uma sessão de depuração (XAML e C#)](../debugger/navigate-a-debugging-session-in-visual-studio-xaml-and-csharp.md)



