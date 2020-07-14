---
title: Iniciar uma sessão de depuração para um aplicativo UWP | Microsoft Docs
ms.custom: seodec18
ms.date: 11/20/2018
ms.topic: how-to
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
manager: jillfra
ms.workload:
- uwp
ms.openlocfilehash: c4e025603fef11e278aee21b3c44f8d35d7cd34b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85536546"
---
# <a name="start-a-debugging-session-for-a-uwp-app"></a>Iniciar uma sessão de depuração de um aplicativo UWP

Este artigo descreve como iniciar uma sessão de depuração do Visual Studio para um aplicativo Plataforma Universal do Windows (UWP). Os aplicativos UWP podem ser escritos em XAML e C++, XAML e C#/Visual Basic. Para iniciar a depuração de um aplicativo UWP, configure a sessão de depuração e escolha a maneira de iniciar o aplicativo.

::: moniker range=">=vs-2019"
> [!NOTE]
> A partir do Visual Studio 2019, os aplicativos UWP para HTML e JavaScript não têm mais suporte.
::: moniker-end
::: moniker range="vs-2017"
No Visual Studio 2017, a maioria dos comandos e opções mostrados neste artigo também se aplica aos aplicativos UWP para HTML e JavaScript. Onde os comandos são diferentes entre os aplicativos gerenciados e C++, os aplicativos JavaScript normalmente são os mesmos comandos para aplicativos UWP do C++.
::: moniker-end

## <a name="start-debugging-from-the-visual-studio-toolbar"></a><a name="BKMK_The_easy_way_to_start_debugging"></a>Iniciar a depuração na barra de ferramentas do Visual Studio

A maneira mais fácil de configurar e iniciar a depuração é da barra de ferramentas padrão do Visual Studio.

![Depurar da barra de ferramentas](../debugger/media/vsrun_select_target_device.png)

1. Na lista suspensa **configuração** na barra de ferramentas **padrão** , selecione **depurar**.

1. Na lista suspensa **plataforma** , selecione a plataforma de destino para a qual Compilar.

1. No menu suspenso ao lado da seta verde, selecione o destino de depuração. Você pode escolher um computador local, um dispositivo conectado diretamente, um simulador do Visual Studio local, um dispositivo remoto ou um emulador.

1. Para iniciar a depuração, selecione a seta de **início** verde na barra de ferramentas ou selecione **depurar**  >  **Iniciar Depuração**ou pressione **F5**.

   O Visual Studio compila e inicia o aplicativo com o depurador anexado.

A depuração continua até que um ponto de interrupção seja atingido, você suspende a execução manualmente, uma exceção sem tratamento ou o aplicativo termina.

### <a name="deployment-target-options"></a><a name="BKMK_Choose_the_deployment_target"></a>Opções de destino de implantação

Você pode definir o destino de depuração na barra de ferramentas do Visual Studio ou na página de propriedades de depuração do projeto. Selecione uma das seguintes opções:

|Nome|Descrição|
|-|-|
|**Computador local**|Depura o aplicativo na sessão atual no computador local.|
|**Simula**|Depure o aplicativo no simulador do Visual Studio para aplicativos UWP. O simulador é uma janela da área de trabalho que simula funções de dispositivo, como gestos de toque e rotação de dispositivo, que podem não existir no computador local. A opção simulador estará disponível somente se a plataforma de destino do aplicativo **min. Version** for menor ou igual ao sistema operacional no computador local. Para obter mais informações, consulte [executar aplicativos UWP no simulador](../debugger/run-windows-store-apps-in-the-simulator.md).|
|**Computador remoto**|Depure o aplicativo em um dispositivo conectado ao computador local por meio de uma rede ou um cabo Ethernet. O Ferramentas Remotas para Visual Studio deve estar instalado e em execução no dispositivo remoto. Para obter mais informações, consulte [executar aplicativos UWP em um computador remoto](../debugger/run-windows-store-apps-on-a-remote-machine.md).|
|**Dispositivo**|Depure o aplicativo em um dispositivo conectado por USB. O dispositivo deve ser desbloqueado por desenvolvedor e ter a tela desbloqueada.|
|**Emulador móvel**|Inicialize o emulador especificado no nome do emulador, implante o aplicativo e inicie a depuração. Os emuladores estão disponíveis apenas em computadores habilitados para Hyper-V.|

## <a name="configure-debugging-in-the-project-property-page"></a><a name="BKMK_Open_the_debugging_property_page_for_the_project"></a>Configurar a depuração na página de propriedades do projeto

Para configurar opções de depuração adicionais, use a página de propriedades de depuração do projeto.

**Para abrir as propriedades de depuração:**

1. Em **Gerenciador de soluções**, selecione o projeto e, em seguida, selecione o ícone **Propriedades** ou clique com o botão direito do mouse no projeto e selecione **Propriedades**.

1. No lado esquerdo do painel **Propriedades** :

   - Para aplicativos C# e Visual Basic, selecione **depurar**.

     ![Página de propriedades de depuração de projeto do C# e do Visual Basic](../debugger/media/dbg_csvb_debugpropertypage.png)

   - Para aplicativos C++, selecione **Propriedades de configuração**  >  **depuração**.

     ![Página de propriedades de depuração de aplicativo UWP C++](../debugger/media/dbg_cpp_debugpropertypage.png)

### <a name="choose-the-debugger-to-use"></a><a name="BKMK_Choose_the_debugger_to_use"></a> Escolher o depurador a ser usado

Para aplicativos C# e Visual Basic, o Visual Studio decodifica código gerenciado por padrão. Você pode optar por depurar outros tipos de código ou de códigos adicionais. Você também pode definir valores de **tipo de depurador** para todas as tarefas em segundo plano que fazem parte do projeto.

Em aplicativos C++, o Visual Studio decorre o código nativo por padrão. Você pode optar por depurar tipos específicos de código em vez de, ou além de, código nativo.

**Para especificar tipos de código a serem depurados:**

- Para aplicativos C# e Visual Basic, selecione um dos seguintes depuradores nos menus suspensos tipo de **aplicativo** e **tipo de processo em segundo plano** em **tipo de depurador** na página de propriedades **depurar** .

- Para aplicativos C++, selecione um dos seguintes depuradores na lista suspensa **tipo de depurador** na página de propriedades **depuração** .

|Nome|Descrição|
|-|-|
|**Somente Gerenciado**|Depura o código gerenciado no aplicativo. O código JavaScript e o código C/C++ nativo são ignorados.|
|**Somente nativo**|Depura o código C/C++ nativo no aplicativo. O código gerenciado e o código JavaScript são ignorados.|
|**Misto (Gerenciado e Nativo)**|Depura o código C/C++ nativo e o código gerenciado no aplicativo. O código JavaScript é ignorado. Em projetos C++, essa opção é chamada **de Managed e Native**.|
|**Script**|Depura o código JavaScript no aplicativo. O código gerenciado e o código nativo são ignorados.|
|**Nativo com Script**|Depurar código C/C++ nativo e código JavaScript em seu aplicativo. O código gerenciado é ignorado. Disponível apenas em projetos C++ ou tarefas em segundo plano.|
|**Somente GPU (C++ AMP)**|Depurar o código C++ nativo que é executado em uma GPU (unidade de processamento gráfico). Disponível somente em projetos C++.|

### <a name="disable-network-loopbacks-optional"></a><a name="BKMK__Optional__Disable_network_loopbacks"></a>Desabilitar loopbacks de rede (opcional)

 Por segurança, um aplicativo UWP que é instalado da maneira padrão não pode fazer chamadas de rede para o dispositivo no qual ele está instalado. O Visual Studio isenta os aplicativos implantados dessa regra por padrão, para que você possa testar os procedimentos de comunicação em um único computador. Antes de liberar seu aplicativo, você deve testar seu aplicativo sem a isenção.

**Para remover a isenção de loopback de rede:**

- Para aplicativos em C# e Visual Basic, desmarque a caixa de seleção **permitir loopback de rede local** em **Opções de início** na página de propriedades de **depuração** .

- Para aplicativos C++, selecione **não** na lista suspensa **permitir loopback de rede local** na página de propriedades **depuração** .

### <a name="reinstall-the-app-when-you-start-debugging-optional"></a><a name="BKMK__Optional__Reinstall_the_app_when_you_start_debugging"></a>Reinstalar o aplicativo quando você iniciar a depuração (opcional)
 Para diagnosticar problemas de instalação com um aplicativo C# ou Visual Basic, selecione **desinstalar e reinstale o meu pacote** na página de propriedades de **depuração** . Essa opção recria a instalação original quando você inicia a depuração. Essa opção não está disponível para projetos C++.

### <a name="set-authentication-options-for-remote-debugging"></a><a name="BKMK__Optional__Disable_authentication_requirement_to_start_the_remote_debugger"></a>Definir opções de autenticação para depuração remota

Por padrão, você deve fornecer credenciais do Windows para executar o depurador remoto ao selecionar **computador remoto** como o destino de implantação. Você pode alterar o requisito de autenticação.

O modo de autenticação **Universal (protocolo não criptografado)** destina-se a dispositivos IOT, Xbox e HoloLens, bem como a atualização do criador ou computadores Windows 10 posteriores.

**Para alterar o método de autenticação:**

- Para aplicativos C# e Visual Basic, na página de propriedades de **depuração** , selecione **computador remoto** como o **dispositivo de destino**. Em seguida, selecione **nenhum** ou **Universal (protocolo não criptografado)** para o **modo de autenticação**.

- Para aplicativos C++, selecione **computador remoto** em **depurador para iniciar** na página de propriedades **depuração** . Em seguida, selecione **sem autenticação** ou **Universal (protocolo não criptografado)** para o **tipo de autenticação**.

> [!CAUTION]
> Não há segurança de rede quando você executa o depurador remoto em modos **nenhum** ou **Universal (protocolo não criptografado)** . Escolha esses modos somente em redes confiáveis que você tem certeza de que não estão em risco de código mal-intencionado ou tráfego hostil.

## <a name="debugging-start-options"></a><a name="BKMK_Start_the_debugging_session"></a>Opções de inicialização de depuração

Quando você seleciona **depurar**  >  **Iniciar Depuração** ou pressionar **F5**, o Visual Studio inicia o aplicativo com o depurador anexado. A execução continua até que um ponto de interrupção seja alcançado, você suspenda a execução manualmente, ocorra uma exceção sem tratamento ou o aplicativo chegue ao fim.

### <a name="start-debugging-but-delay-app-start"></a><a name="BKMK_Start_debugging__F5__but_delay_the_app_start"></a>Iniciar Depuração, mas atrasar início do aplicativo

Por padrão, o Visual Studio inicia o aplicativo imediatamente quando você inicia a depuração. Você também pode definir o aplicativo para ser executado no modo de depuração, mas iniciar o aplicativo fora do depurador. Por exemplo, você pode desejar depurar a inicialização do aplicativo no menu **Iniciar** do Windows ou depurar um processo em segundo plano no aplicativo. Se você escolher essa opção, o aplicativo será iniciado no depurador na inicialização.

**Para desabilitar a inicialização automática do aplicativo:**

- Para aplicativos C# e Visual Basic, selecione não **Iniciar, mas, em seguida, depurar meu código quando começar** em **Iniciar opções** na página de propriedades de **depuração** .

- Para aplicativos C++, selecione **não** na lista suspensa **Iniciar aplicativo** na página de propriedades **depuração** .

Para obter mais informações sobre como depurar tarefas em segundo plano, consulte [disparar eventos de suspensão, retomada e segundo plano para aplicativos UWP](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md).

### <a name="debug-an-installed-or-running-uwp-app"></a><a name="BKMK_Start_an_installed_app_in_the_debugger"></a>Depurar um aplicativo UWP instalado ou em execução

Você pode usar **depurar pacote do aplicativo instalado** para depurar um aplicativo UWP que já está instalado ou em execução em um dispositivo local ou remoto. O aplicativo pode ter sido instalado do Microsoft Store ou pode não ser um projeto do Visual Studio. Por exemplo, o aplicativo pode ter um sistema de compilação personalizado que não usa o Visual Studio.

Você pode iniciar o aplicativo instalado imediatamente ou pode defini-lo para ser executado no depurador quando iniciado com outro método. Para obter mais informações, consulte [disparar eventos de suspensão, retomada e segundo plano para aplicativos UWP)](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md).

Para iniciar um aplicativo UWP instalado ou em execução no depurador, selecione **depurar**  >  **outros destinos de depuração**  >  **depurar pacote do aplicativo instalado**. Para obter mais instruções, consulte [depurar um pacote do aplicativo instalado](../debugger/debug-installed-app-package.md).

### <a name="attach-the-debugger-to-a-running-windows-8x-app"></a><a name="BKMK_Attach_the_debugger_to_a_running_app_"></a>Anexar o depurador a um aplicativo do Windows 8. x em execução

Para anexar o depurador a um aplicativo [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)], você deve usar o Gerenciador de Pacotes Depuráveis para definir a execução do aplicativo no modo de depuração. O Gerenciador de pacotes do depurável é instalado com o Ferramentas Remotas para Visual Studio.

1. Instale o Ferramentas Remotas para Visual Studio no dispositivo em que o aplicativo está instalado. Para obter mais informações, consulte [instalando as ferramentas remotas](../debugger/remote-debugging.md).

1. Na tela **Iniciar** do Windows, procure e inicie o **Gerenciador de pacotes do depurável**.

   É exibida uma janela do PowerShell corretamente configurada para o cmdlet AppxDebug.

1. Especifique o identificador PackageFullName do aplicativo.

   1. Para exibir uma lista que inclui o PackageFullName de todos os aplicativos, digite `Get-AppxPackage` no prompt do PowerShell.

   1. No prompt do PowerShell, insira `Enable-AppxDebug <PackageFullName>` , em que \<PackageFullName> é o identificador PackageFullName do aplicativo.

1. Selecione **depuração**  >  **anexar ao processo**.

1. Na caixa de diálogo **anexar ao processo** , especifique o dispositivo remoto na caixa **destino da conexão** .

   Você pode inserir o nome do dispositivo, selecioná-lo na lista suspensa na caixa **destino da conexão** ou selecionar **Localizar** para localizar o dispositivo na caixa de diálogo **conexões remotas** .

1. Para especificar o tipo de código que você deseja depurar, ao lado da caixa **anexar a** , selecione **selecionar**.

1. Na caixa de diálogo **Selecionar tipo de código** , selecione:
   - **Determinar automaticamente o tipo de código a ser depurado**ou
   - **Depure esses tipos de código**e selecione um ou mais tipos de código na lista.

1. Na lista **processos disponíveis** , selecione o processo do aplicativo a ser depurado.

1. Selecionar **Anexar**.

 O Visual Studio anexa o depurador ao processo. A execução continua até que um ponto de interrupção seja alcançado, você suspenda a execução manualmente, ocorra uma exceção sem tratamento ou o aplicativo chegue ao fim.

::: moniker range="vs-2017"
> [!NOTE]
> Os aplicativos JavaScript são executados em uma instância do processo de *wwahost.exe* . Se mais de um aplicativo JavaScript estiver em execução, você precisará saber a identificação do processo numérico (PID) do processo de *wwahost.exe* do seu aplicativo para anexá-lo a ele.
>
> A maneira mais fácil de anexar ao aplicativo JavaScript é fechar todos os outros aplicativos JavaScript. Ou, você pode observar os PIDs de processos de *wwahost.exe* em execução no Gerenciador de tarefas do Windows antes de iniciar seu aplicativo. Quando você inicia seu aplicativo, seu *wwahost.exe* PID será aquele que for diferente daqueles que você anotou anteriormente.
::: moniker-end

## <a name="see-also"></a>Confira também

- [Depurar aplicativos no Visual Studio](../debugger/debugging-windows-store-and-windows-universal-apps.md)