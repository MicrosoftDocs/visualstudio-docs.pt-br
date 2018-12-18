---
title: Iniciar uma sessão de depuração para um aplicativo UWP | Microsoft Docs
ms.custom: seodec18
ms.date: 11/20/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
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
- vs.debug.installedapppackagelauncher
- vs.debug.error.wwahost_scriptdebuggingdisabled
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- uwp
ms.openlocfilehash: 181dec6bfa6ebe96528c39b74d68375b8eb7fcb8
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53062403"
---
# <a name="start-a-debugging-session-for-a-uwp-app"></a>Iniciar uma sessão de depuração de um aplicativo UWP
  
Este artigo descreve como iniciar uma sessão de depuração do Visual Studio para um aplicativo da plataforma Universal do Windows (UWP). Aplicativos UWP podem ser escritos em XAML e C++, XAML e C#/Visual Basic, ou HTML e JavaScript. Para iniciar a depuração de um aplicativo UWP, configure a sessão de depuração e escolher a maneira de iniciar o aplicativo.  
  
##  <a name="BKMK_The_easy_way_to_start_debugging"></a>Iniciar a depuração na barra de ferramentas do Visual Studio 
  
É a maneira mais fácil de configurar e iniciar a depuração na barra de ferramentas do Visual Studio standard. 

![Na barra de ferramentas de depuração](../debugger/media/vsrun_select_target_device.png)  
  
1. Do **Configuration** lista suspensa a **padrão** barra de ferramentas, selecione **depurar**.  
  
1. Dos **plataforma** lista suspensa, selecione a plataforma de destino para criar para. 
   
1. Na lista suspensa ao lado da seta verde, selecione o destino de depuração. Você pode escolher uma máquina local, o dispositivo diretamente conectados, o local simulador do Visual Studio, o dispositivo remoto ou o emulador. 
   
1. Para iniciar a depuração, selecione o verde **inicie** seta na barra de ferramentas, ou selecione **Debug** > **iniciar depuração**, ou pressione **F5**. 
   
   O Visual Studio compila e inicia o aplicativo com o depurador anexado. 

Depuração continua até que um ponto de interrupção é atingido, você suspenda a execução manualmente, ocorra uma exceção sem tratamento ou o aplicativo seja encerrado.  
  
###  <a name="BKMK_Choose_the_deployment_target"></a> Opções de implantação de destino 
  
Você pode definir o destino de depuração na barra de ferramentas do Visual Studio ou página de propriedades de depuração do projeto. Selecione uma destas opções:

|||  
|-|-|  
|**Computador Local**|Depura o aplicativo na sessão atual no computador local.|  
|**Simulador**|Depura o aplicativo no simulador do Visual Studio para aplicativos UWP. O simulador é uma janela da área de trabalho que simula as funções do dispositivo, como a rotação do dispositivo, que pode não existir no computador local e gestos de toque. A opção simulador está disponível somente se seu aplicativo **mínima da plataforma de destino. Versão** é menor que ou igual ao sistema operacional no computador local. Para obter mais informações, consulte [executar aplicativos UWP no simulador](../debugger/run-windows-store-apps-in-the-simulator.md).|  
|**Computador Remoto**|Depura o aplicativo em um dispositivo conectado ao computador local em uma rede ou um cabo Ethernet. Ferramentas remotas para Visual Studio deve ser instalado e em execução no dispositivo remoto. Para obter mais informações, consulte [executar aplicativos UWP em um computador remoto](../debugger/run-windows-store-apps-on-a-remote-machine.md).|  
|**Dispositivo**|Depura o aplicativo em um dispositivo USB conectado. O dispositivo deve ser desbloqueados pelo desenvolvedor e ter a tela desbloqueada.|  
|**Emulador móvel**|Inicializar o emulador especificado no nome do emulador, implantar o aplicativo e iniciar a depuração. Emuladores estão disponíveis apenas em máquinas do Hyper-V habilitado.|  

##  <a name="BKMK_Open_the_debugging_property_page_for_the_project"></a> Configurar a depuração na página de propriedade do projeto 

Para configurar opções de depuração adicionais, use a página de propriedades de depuração do projeto. 

**Para abrir as propriedades de depuração:**

1. No **Gerenciador de soluções**, selecione o projeto e, em seguida, selecione o **Properties** ícone, ou clique com botão direito no projeto e selecione **propriedades**.  
   
1. No lado esquerdo do **propriedades** painel:
   
   - Para C# e aplicativos do Visual Basic, selecionados **depurar**.  
     
     ![C#e a página de propriedades de depuração de projeto do Visual Basic](../debugger/media/dbg_csvb_debugpropertypage.png)  
   
   - Para aplicativos de C++ e JavaScript, selecione **propriedades de configuração** > **depuração**.  
     
     ![Página de propriedades de depuração do aplicativo de UWP em C++](../debugger/media/dbg_cpp_debugpropertypage.png)  

###  <a name="BKMK_Choose_the_debugger_to_use"></a> Escolher o depurador a ser usado  

Para C# e aplicativos do Visual Basic, Visual Studio depura o código gerenciado por padrão. Você pode optar por depurar tipos de código de outros ou adicionais. Você também pode definir **tipo de depurador** valores para quaisquer tarefas em segundo plano que fazem parte do projeto.

Aplicativos em C++, Visual Studio depura o código nativo por padrão. Em aplicativos JavaScript, o Visual Studio depura o script por padrão. Você pode optar por depurar tipos específicos de código em vez de ou além do código nativo. 

**Para especificar os tipos de código para depurar:**

- Para C# e aplicativos do Visual Basic, selecione uma das seguintes depuradores do **tipo de aplicativo** e **tipo de processo do plano de fundo** menus suspensos em **tipo de depurador** em o **depurar** página de propriedades.  
  
- Para C + + c++ /CLI aplicativos JavaScript, selecione uma das seguintes depuradores do **tipo de depurador** lista suspensa a **depuração** página de propriedades.

|||  
|-|-|  
|**Somente Gerenciador**|Depura o código gerenciado no aplicativo. O código JavaScript e o código C/C++ nativo são ignorados.|  
|**Somente nativo**|Depura o código C/C++ nativo no aplicativo. O código gerenciado e o código JavaScript são ignorados.|  
|**Misto (Gerenciado e Nativo)**|Depura o código C/C++ nativo e o código gerenciado no aplicativo. O código JavaScript é ignorado. Em projetos do C++, essa opção é chamada **nativo e gerenciado**.|  
|**script**|Depura o código JavaScript no aplicativo. O código gerenciado e o código nativo são ignorados.|  
|**Nativo com Script**|Depure código C/C++ nativo e o código JavaScript em seu aplicativo. O código gerenciado é ignorado. Disponível em projetos do C++ ou apenas para tarefas em segundo plano.|  
|**Somente GPU (C++ AMP)**|Depurar o código C++ nativo que é executado em uma GPU (unidade de processamento gráfico). Disponível em projetos do C++ somente.|  

  
###  <a name="BKMK__Optional__Disable_network_loopbacks"></a> Desabilitar loopbacks de rede (opcional) 
  
 Para segurança, um aplicativo UWP que é instalado da maneira padrão não pode fazer chamadas de rede para o dispositivo que está instalado. Isenções do Visual Studio implantado aplicativos dessa regra por padrão, para que você possa testar procedimentos de comunicação em um único computador. Antes de liberar seu aplicativo, você deve testar seu aplicativo sem a isenção.  
  
**Para remover a isenção de loopback de rede:**  
  
-   Para C# e aplicativos do Visual Basic, desmarque o **permitir loopback de rede local** caixa de seleção em **opções de inicialização** sobre o **depurar** página de propriedades.  
  
-   Para aplicativos do Visual C++ e JavaScript, selecione **não** da **permitir Loopback de rede Local** lista suspensa a **depuração** página de propriedades.  
  
###  <a name="BKMK__Optional__Reinstall_the_app_when_you_start_debugging"></a> Reinstale o aplicativo ao iniciar a depuração (opcional) 
 Para diagnosticar problemas de instalação com um C# ou o aplicativo Visual Basic, selecione **desinstalar e reinstalar meu pacote** no **depurar** página de propriedades. Essa opção recria a instalação original ao iniciar a depuração. Essa opção não está disponível para projetos C++ e JavaScript.  
  
###  <a name="BKMK__Optional__Disable_authentication_requirement_to_start_the_remote_debugger"></a> Definir opções de autenticação para a depuração remota  
  
Por padrão, você deve fornecer as credenciais do Windows para executar o depurador remoto quando você seleciona **máquina remota** como o destino de implantação. Você pode alterar o requisito de autenticação. 

O **Universal (protocolo não criptografado)** modo de autenticação é para dispositivos IoT, Xbox e HoloLens e o atualização do criador ou posterior PCs com Windows 10.  

**Para alterar o método de autenticação:**  

- Para C# e aplicativos do Visual Basic, sobre o **depurar** página de propriedades, selecione **máquina remota** como o **dispositivo de destino**. Em seguida, selecione **None** ou **Universal (protocolo não criptografado)** para **modo de autenticação**. 
  
- Para aplicativos de C++ e JavaScript, selecione **máquina remota** sob **depurador a iniciar** sobre o **depuração** página de propriedades. Em seguida, selecione **sem autenticação** ou **Universal (protocolo não criptografado)** para **tipo de autenticação**. 
  
> [!CAUTION]
> Há nenhuma segurança de rede, quando você executar o depurador remoto no **None** ou **Universal (protocolo não criptografado)** modos. Escolha esses modos somente em redes confiáveis que você está claro que não estão em risco de um código mal-intencionado ou tráfego hostil.  
  
##  <a name="BKMK_Start_the_debugging_session"></a> Opções de início de depuração  
  
Quando você seleciona **Debug** > **iniciar depuração** ou pressione **F5**, Visual Studio inicia o aplicativo com o depurador anexado. A execução continua até que um ponto de interrupção seja alcançado, você suspenda a execução manualmente, ocorra uma exceção sem tratamento ou o aplicativo chegue ao fim.  
  
###  <a name="BKMK_Start_debugging__F5__but_delay_the_app_start"></a> Iniciar a depuração, mas a inicialização do aplicativo de atraso  

Por padrão, o Visual Studio inicia o aplicativo imediatamente quando você iniciar a depuração. Você também pode definir o aplicativo seja executado no modo de depuração, mas a iniciar o aplicativo fora do depurador. Por exemplo, convém depurar a inicialização de aplicativo a partir do Windows **iniciar** menu ou depurar um processo em segundo plano no aplicativo. Se você escolher essa opção, o aplicativo é iniciado no depurador na inicialização. 

**Para desabilitar a inicialização automática do aplicativo:**  
  
- Para C# e aplicativos do Visual Basic, selecionados **não iniciar, mas depurar meu código quando ele é iniciado** sob **opções de inicialização** sobre o **depurar** página de propriedades.  
   
- Para aplicativos de C++ e JavaScript, selecione **não** da **Iniciar aplicativo** lista suspensa a **depuração** página de propriedades.  
  
Para obter mais informações sobre como depurar tarefas em segundo plano, consulte [disparador de suspender, continuar e eventos para aplicativos UWP em segundo plano](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md).  
  
###  <a name="BKMK_Start_an_installed_app_in_the_debugger"></a> Depurar um aplicativo UWP instalado ou em execução 

Você pode usar **depurar pacote do aplicativo instalado** para depurar um aplicativo UWP que já está instalado ou em execução em um dispositivo local ou remoto. O aplicativo pode ter sido instalado da Microsoft Store, ou talvez não seja um projeto do Visual Studio. Por exemplo, o aplicativo pode ter um sistema de compilação personalizada que não usa o Visual Studio.  
  
Você pode iniciar o aplicativo instalado imediatamente, ou você pode defini-lo para ser executado no depurador quando iniciado com outro método. Para obter mais informações, consulte [disparador de suspender, continuar e eventos para aplicativos UWP em segundo plano)](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md).  
  
Para iniciar um aplicativo UWP instalado ou em execução no depurador, selecione **Debug** > **outros destinos de depuração** > **depurar pacote do aplicativo instalado**. Para obter mais instruções, consulte [depurar pacote de aplicativo instalado](../debugger/debug-installed-app-package.md).

###  <a name="BKMK_Attach_the_debugger_to_a_running_app_"></a> Anexar o depurador a um aplicativo de 8.x do Windows em execução

Para anexar o depurador a um aplicativo [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)], você deve usar o Gerenciador de Pacotes Depuráveis para definir a execução do aplicativo no modo de depuração. O Gerenciador de pacotes depurável é instalado com as ferramentas remotas para Visual Studio.  
  
1. Instale as ferramentas remotas para Visual Studio no dispositivo onde o aplicativo está instalado. Para obter mais informações, consulte [instalando as ferramentas remotas](../debugger/remote-debugging.md).  
   
1. No Windows **inicie** tela, pesquise e inicie **Gerenciador de pacotes depurável**.  
   
   É exibida uma janela do PowerShell corretamente configurada para o cmdlet AppxDebug.  
   
1. Especifique o identificador PackageFullName do aplicativo. 
   
   1. Para exibir uma lista que inclui o PackageFullName de todos os aplicativos, digite `Get-AppxPackage` no prompt do PowerShell.  
   
   1. No prompt do PowerShell, digite `Enable-AppxDebug <PackageFullName>`, onde \<PackageFullName > é o identificador PackageFullName do aplicativo.  
   
1. Selecione **Depurar** > **Anexar ao Processo**.  
   
1. No **anexar ao processo** caixa de diálogo, especifique o dispositivo remoto na **destino de Conexão** caixa. 
   
   Você pode inserir o nome do dispositivo, selecione-o na lista suspensa a **destino de Conexão** caixa ou selecione **localizar** para encontrar o dispositivo na **conexões remotas** caixa de diálogo.  
   
1. Para especificar o tipo de código que você deseja depurar, ao lado de **anexar** caixa, selecione **selecione**.  
   
1. No **Select Code Type** caixa de diálogo caixa, selecione:
   - **Determine automaticamente o tipo de código para depurar**, ou 
   - **Depurar esses tipos de código**e, em seguida, selecione um ou mais tipos de código na lista.  
   
1. No **processos disponíveis** , selecione o processo do aplicativo para depuração.  
   
1. Selecione **anexar**.  
  
 O Visual Studio anexa o depurador ao processo. A execução continua até que um ponto de interrupção seja alcançado, você suspenda a execução manualmente, ocorra uma exceção sem tratamento ou o aplicativo chegue ao fim.

> [!NOTE]
> Os aplicativos JavaScript são executados em uma instância do processo *wwahost.exe*. Se estiver executando mais de um aplicativo JavaScript, você precisará saber a id do processo numérico (PID) do seu aplicativo *wwahost.exe* processo para anexar a ele.  
> 
> A maneira mais fácil para anexar ao seu aplicativo JavaScript é fechar todos os outros aplicativos de JavaScript. Ou, você pode observar os PIDs Running *wwahost.exe* processos no Windows Gerenciador de tarefas antes de iniciar seu aplicativo. Quando você inicia seu aplicativo, seus *wwahost.exe* PID será aquele que é diferente daquelas que você anotou anteriormente.  

## <a name="see-also"></a>Consulte também  
 [Depurar aplicativos no Visual Studio](../debugger/debug-store-apps-in-visual-studio.md)   