---
title: Iniciar uma sessão de depuração para aplicativos da Store (JavaScript) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.installedapppackagelauncher
- vs.debug.error.wwahost_scriptdebuggingdisabled
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: fb91203f-2cf4-44d3-8ed9-93bc5aaa50b8
caps.latest.revision: 27
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 634051d47b3462e2462c5592448b20f70d09ae71
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85531931"
---
# <a name="start-a-debugging-session-for-store-apps-in-visual-studio-javascript"></a>Iniciar uma sessão de depuração para aplicativos da Store no Visual Studio (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Aplica-se ao Windows e Windows Phone] (.. /Imagem/windows_and_phone_content.png "windows_and_phone_content")

 Este tópico descreve como iniciar uma sessão de depuração para os aplicativos da Windows Store gravados em JavaScript e HTML5. Você pode iniciar a depuração com um único pressionamento de tecla ou configurar a sessão de depuração para cenários específicos e escolher a maneira de iniciar o aplicativo.

> [!NOTE]
> Para aplicativos escritos em XAML e Visual C#, Visual C++ ou Visual Basic, consulte [iniciar uma sessão de depuração (VB, C#, C++ e XAML)](../debugger/start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md)

## <a name="in-this-topic"></a><a name="BKMK_In_this_topic"></a>Neste tópico
 [Neste tópico](#BKMK_In_this_topic)

 [{1&amp;gt;A maneira fácil de iniciar a depuração&amp;lt;1}](#BKMK_The_easy_way_to_start_debugging)

 [Configurar a sessão de depuração](#BKMK_Configure_the_debugging_session)

- [Abrir a página de propriedades de depuração do projeto](#BKMK_Open_the_debugging_property_page_for_the_project)

- [Escolher as opções de configuração de build](#BKMK_Choose_the_build_configuration_options)

- [{1&amp;gt;Escolher o destino de implantação&amp;lt;1}](#BKMK_Choose_the_deployment_target)

- [Escolha o depurador a ser usado](#BKMK_Choose_the_debugger_to_use)

- [(Opcional) Atrasar o início do aplicativo na sessão de depuração](#BKMK__Optional__Delay_starting_app_in_the_debug_session)

- [(Opcional) Desabilitar loopbacks de rede](#BKMK__Optional__Disable_network_loopbacks)

  [Iniciar a sessão de depuração](#BKMK_Start_the_debugging_session)

- [{1&amp;gt;Iniciar a depuração (F5)&amp;lt;1}](#BKMK_Start_debugging__F5_)

- [{1&amp;gt;{2&amp;gt;Iniciar a depuração (F5), mas atrasar o início do aplicativo&amp;lt;2}&amp;lt;1}](#BKMK_Start_debugging__F5__but_delay_the_app_start)

  [{1&amp;gt;Iniciar um aplicativo instalado no depurador&amp;lt;1}](#BKMK_Start_an_installed_app_in_the_debugger)

  [Anexar o depurador a um aplicativo em execução](#BKMK_Attach_the_debugger_to_a_running_app_)

- [Definir o aplicativo para ser executado no modo de depuração](#BKMK_Set_the_app_to_run_in_debug_mode)

- [Anexar o depurador](#BKMK_Attach_the_debugger)

## <a name="the-easy-way-to-start-debugging"></a><a name="BKMK_The_easy_way_to_start_debugging"></a>A maneira fácil de iniciar a depuração
 ![Aplica-se somente ao Windows](../debugger/media/windows-only-content.png "windows_only_content")

1. Abra a solução do aplicativo no Visual Studio.

2. Se a solução contém projetos para aplicativos da Windows Store e Windows Phone Store, verifique se o projeto que você quer depurar é o projeto de inicialização. Em explorar solução, selecione o projeto e, em seguida, escolha **definir como projeto de inicialização** no menu de contexto.

3. Pressione F5.

   ![Aplica-se somente a Windows Phone](../debugger/media/phone-only-content.png "phone_only_content")

   O Visual Studio compila e inicia o aplicativo com o depurador anexado. A execução continua até que um ponto de interrupção seja alcançado, você suspenda a execução manualmente, ocorra uma exceção sem tratamento ou o aplicativo chegue ao fim. Para obter mais informações, consulte [início rápido: Depurar HTML e CSS](../debugger/quickstart-debug-html-and-css.md).

## <a name="configure-the-debugging-session"></a><a name="BKMK_Configure_the_debugging_session"></a>Configurar a sessão de depuração
 Como o script não está compilado, a configuração de compilação e as configurações da plataforma não se aplicam. Se você estiver depurando um C++ ou um componente gerenciado, defina a **configuração** para **depurar** e escolha a plataforma de destino na caixa de diálogo de **configuração** .

### <a name="open-the-debugging-property-page-for-the-project"></a><a name="BKMK_Open_the_debugging_property_page_for_the_project"></a>Abrir a página de propriedades de depuração para o projeto

1. No Gerenciador de Soluções, selecione o projeto. No menu de atalho, escolha **Propriedades**.

2. Expanda o nó **Propriedades de configuração** e escolha **depuração**

### <a name="choose-the-build-configuration-options"></a><a name="BKMK_Choose_the_build_configuration_options"></a>Escolher as opções de configuração de compilação

1. Na lista de **configurações** , escolha **depurar** ou **depuração (ativa)**.

2. Na lista **plataforma** , escolha a plataforma de destino para a qual Compilar. Na maioria dos casos, **qualquer CPU** é a melhor opção.

### <a name="choose-the-deployment-target"></a><a name="BKMK_Choose_the_deployment_target"></a>Escolher o destino de implantação
 Você pode implantar e depurar um aplicativo no computador com o Visual Studio, no simulador do Visual Studio do computador local ou de um computador remoto. Você escolhe o destino na lista **depurador para iniciar** na página de propriedades **depuração** do projeto.

 ![Aplica-se somente ao Windows](../debugger/media/windows-only-content.png "windows_only_content")

 Para um aplicativo da Windows Store, escolha uma destas opções na lista de **dispositivos de destino** :

|Opção|Descrição|
|-|-|
|**Computador local**|Depura o aplicativo na sessão atual no computador local. Consulte [executar aplicativos da Windows Store no computador local](../debugger/run-windows-store-apps-on-the-local-machine.md).|
|**Simula**|Depura o aplicativo no simulador do Visual Studio para aplicativos [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)]. O simulador é uma janela da área de trabalho que permite depurar recursos, como gestos de toque e rotação de dispositivos, que não estão disponíveis no computador local. Consulte [executar aplicativos da Windows Store no simulador](../debugger/run-windows-store-apps-in-the-simulator.md).|
|**Computador remoto**|Depura o aplicativo em um dispositivo conectado ao computador local por uma intranet ou diretamente por meio de um cabo Ethernet. Para depurar remotamente, as Ferramentas Remotas do Visual Studio devem estar instaladas e em execução no dispositivo remoto. Consulte [executar aplicativos da Windows Store em um computador remoto](../debugger/run-windows-store-apps-on-a-remote-machine.md).|

 Se você escolher **computador remoto**, especifique o nome ou o endereço IP do computador remoto de uma das seguintes maneiras:

- Insira o nome ou endereço IP do computador remoto na caixa **nome da máquina** .

- Escolha a seta para baixo na caixa **nome da máquina** e escolha **\<Locate...>** . Em seguida, escolha o computador remoto na caixa de diálogo **selecionar conexão remota do depurador** .

   ![Selecionar conexão do depurador remoto](../debugger/media/vsrun-pro-selectremotedebuggerdlg.png "VSRUN_PRO_SelectRemoteDebuggerDlg")

  > [!NOTE]
  > A caixa de diálogo Selecionar Conexão de Depurador Remoto exibe os computadores que estão na sub-rede local e os computadores que estão diretamente conectados ao computador com o Visual Studio por um cabo Ethernet. Para especificar outro computador, digite o nome na caixa **nome da máquina** .

  ![Aplica-se somente a Windows Phone](../debugger/media/phone-only-content.png "phone_only_content")

  Para um aplicativo de telefone da Windows Store, escolha **dispositivo** ou um dos emuladores da lista de **dispositivos de destino** .

### <a name="choose-the-debugger-to-use"></a><a name="BKMK_Choose_the_debugger_to_use"></a> Escolher o depurador a ser usado
 Por padrão, o depurador se anexa ao código JavaScript do aplicativo. Você pode escolher depurar o código C++ nativo e gerenciado dos componentes do aplicativo em vez do código JavaScript. Especifique o código a ser depurado na lista **tipo de depurador** na página de propriedades **depuração** do projeto de aplicativo.

 Escolha um desses depuradores na lista **tipo de depurador** :

|Type|Description|
|-|-|
|**{1&amp;gt;Somente Script&amp;lt;1}**|Depura o código JavaScript no aplicativo. O código gerenciado e o código nativo são ignorados.|
|**Somente nativo**|Depura o código C/C++ nativo no aplicativo. O código gerenciado e o código JavaScript são ignorados.|
|**Nativo com Script**|Depura o código C++ nativo e o código JavaScript no aplicativo.|
|**Somente Gerenciado**|Depura o código gerenciado no aplicativo. O código JavaScript e o código C/C++ nativo são ignorados.|
|**Misto (Gerenciado e Nativo)**|Depura o código C/C++ nativo e o código gerenciado no aplicativo. O código JavaScript é ignorado.|

### <a name="optional-delay-starting-the-app-in-the-debug-session"></a><a name="BKMK__Optional__Delay_starting_app_in_the_debug_session"></a>Adicional Atraso ao iniciar o aplicativo na sessão de depuração
 Por padrão, o Visual Studio inicia o aplicativo imediatamente quando você começa a depuração. Você também pode iniciar uma sessão de depuração, mas atrasar o início do seu aplicativo. O aplicativo é iniciado no depurador quando é iniciado do menu Iniciar ou por um contrato de ativação ou quando é iniciado por outro processo ou método. Você também pode usar o início atrasado para depurar eventos em segundo plano no aplicativo que você quer que ocorram quando o aplicativo não está em execução.

 Você especifica se deve atrasar a inicialização do seu aplicativo na lista **Iniciar aplicativo** na página de propriedades **depuração** do projeto do aplicativo. Escolha uma destas opções:

- Escolha **não** para atrasar a inicialização do seu aplicativo.

- Escolha **Sim** para iniciar o aplicativo imediatamente.

### <a name="optional-disable-network-loopbacks"></a><a name="BKMK__Optional__Disable_network_loopbacks"></a>Adicional Desabilitar loopbacks de rede
 ![Aplica-se somente ao Windows](../debugger/media/windows-only-content.png "windows_only_content")

 Por motivos de segurança, um aplicativo da Windows Store instalado da maneira padrão não pode efetuar chamadas de rede para o dispositivo em que está instalado. Por padrão, a implantação do Visual Studio cria uma isenção dessa regra para o aplicativo implantado. Essa isenção permite que você teste procedimentos de comunicação em um único computador. Antes de enviar seu aplicativo para o Windows Store, você deve testá-lo sem a isenção.

 Para remover a isenção de auto-retorno de rede, escolha **não** na lista **permitir loopback de rede** na página de propriedades **depuração** .

## <a name="start-the-debugging-session"></a><a name="BKMK_Start_the_debugging_session"></a>Iniciar a sessão de depuração

### <a name="start-debugging-f5"></a><a name="BKMK_Start_debugging__F5_"></a>Iniciar Depuração (F5)
 Quando você escolhe **Iniciar Depuração** no menu **depurar** (teclado: F5), o Visual Studio inicia o aplicativo com o depurador anexado. A execução continua até que um ponto de interrupção seja alcançado, você suspenda a execução manualmente, ocorra uma exceção sem tratamento ou o aplicativo chegue ao fim.

### <a name="start-debugging-f5-but-delay-the-app-start"></a><a name="BKMK_Start_debugging__F5__but_delay_the_app_start"></a>Iniciar Depuração (F5), mas atrasar o início do aplicativo
 Você pode definir o aplicativo para ser executado no modo de depuração, mas inicie-o por outro método que não seja o depurador. Por exemplo, convém depurar a inicialização do aplicativo no menu Iniciar ou depurar um processo em segundo plano do aplicativo sem iniciá-lo. Para atrasar o início do aplicativo, faça o seguinte:

1. Na página de **depuração** das propriedades do projeto de aplicativo, escolha **não** na lista **Iniciar aplicativo** .

2. Escolha **Iniciar Depuração** no menu **depurar** (teclado: F5).

3. Inicie o aplicativo pelo menu Iniciar, por um contrato de execução ou por outro procedimento.

   O aplicativo é iniciado no modo de depuração. A execução continua até que um ponto de interrupção seja alcançado, você suspenda a execução manualmente, ocorra uma exceção sem tratamento ou o aplicativo chegue ao fim.

   . Para obter mais informações sobre como depurar tarefas em segundo plano, consulte [disparar eventos de suspensão, retomada e segundo plano para a Windows Store](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md).

## <a name="start-an-installed-app-in-the-debugger"></a><a name="BKMK_Start_an_installed_app_in_the_debugger"></a>Iniciar um aplicativo instalado no depurador
 Quando você inicia a depuração usando F5, o Visual Studio compila e implanta o aplicativo, define que ele seja executado no modo de depuração e, em seguida, inicia-o. Para iniciar um aplicativo que já está instalado em um dispositivo, use a caixa de diálogo Depurar Pacote do Aplicativo Instalado. Esse procedimento é útil quando você precisa depurar um aplicativo instalado da Windows Store ou quando você tem os arquivos de origem do aplicativo, mas não tem um projeto do Visual Studio para o aplicativo. Por exemplo, você pode ter um sistema de build personalizado que não use projetos ou soluções do Visual Studio.

 O aplicativo pode ser instalado no dispositivo local ou pode estar localizado em um dispositivo remoto.  É possível iniciar o aplicativo imediatamente ou defini-lo para ser executado no depurador quando for iniciado por outro processo ou método, por exemplo, no menu Iniciar ou por um contrato de ativação. Você também pode definir o aplicativo para ser executado no modo de depuração quando quiser depurar um processo em segundo plano sem iniciar o aplicativo. Para obter mais informações, consulte [disparar eventos de suspensão, retomada e segundo plano para a Windows Store](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md).

 Para definir um aplicativo instalado para ser executado no modo de depuração, faça o seguinte:

> [!NOTE]
> O aplicativo não deve estar em execução quando você iniciar este procedimento.

1. No menu **depurar** , escolha **depurar pacote do aplicativo instalado**

2. Escolha uma destas opções na lista:

   |                    |                                                                                                                                                                                                                                                                                                                                                                                                           |
   |--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | **Computador local**  |                                                                                                                Depura o aplicativo na sessão atual no computador local. Consulte [executar aplicativos da Windows Store no computador local](../debugger/run-windows-store-apps-on-the-local-machine.md).                                                                                                                 |
   |   **Simula**    | Depura o aplicativo no simulador do Visual Studio para aplicativos [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)]. O simulador é uma janela da área de trabalho que permite depurar recursos, como gestos de toque e rotação de dispositivos, que não estão disponíveis no computador local. Consulte [executar aplicativos da Windows Store no simulador](../debugger/run-windows-store-apps-in-the-simulator.md). |
   | **Computador remoto** |                          Depura o aplicativo em um dispositivo conectado ao computador local por uma intranet ou diretamente por meio de um cabo Ethernet. Para depurar remotamente, as Ferramentas Remotas do Visual Studio devem estar instaladas e em execução no dispositivo remoto. Consulte [executar aplicativos da Windows Store em um computador remoto](../debugger/run-windows-store-apps-on-a-remote-machine.md).                           |

3. Escolha o aplicativo na lista **pacotes de aplicativos instalados** .

4. Escolha o mecanismo de depuração a ser usado na lista **depurar este tipo de código** .

5. (Opcional). Escolha **não iniciar, mas depure meu código quando começar** a depurar o aplicativo quando ele for iniciado por algum outro método ou para depurar um processo em segundo plano.

   Quando você clica em **Iniciar**, o aplicativo é iniciado ou definido para ser executado no modo de depuração.

## <a name="attach-the-debugger-to-a-running-app"></a><a name="BKMK_Attach_the_debugger_to_a_running_app_"></a>Anexar o depurador a um aplicativo em execução
 Para anexar o depurador a um aplicativo [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)], você deve usar o Gerenciador de Pacotes Depuráveis para definir a execução do aplicativo no modo de depuração. Esse recurso é instalado com as Ferramentas Remotas do Visual Studio.

 Anexar o depurador a um aplicativo é útil quando você precisa depurar um aplicativo já instalado; por exemplo, um que tenha sido instalado na Windows Store. A anexação é necessária quando você tem os arquivos de origem do aplicativo, mas não tem um projeto do Visual Studio para ele. Por exemplo, você pode ter um sistema de build personalizado que não use projetos ou soluções do Visual Studio.

 Para anexar a um aplicativo:

1. Defina o aplicativo para ser executado no modo de depuração. Isso deve ser feito quando o aplicativo não está em execução.

2. Inicie o aplicativo. Você pode iniciar o aplicativo do menu Iniciar por um contrato de execução ou por outro método.

3. Anexe o depurador ao aplicativo em execução.

### <a name="set-the-app-to-run-in-debug-mode"></a><a name="BKMK_Set_the_app_to_run_in_debug_mode"></a>Definir o aplicativo para ser executado no modo de depuração

1. Instale as Ferramentas Remotas do Visual Studio no dispositivo em que o aplicativo está instalado. Consulte [instalando as ferramentas remotas](https://msdn.microsoft.com/library/windows/apps/hh441469.aspx#BKMK_Installing_the_Remote_Tools).

2. No menu Iniciar, procure por `Debuggable Package Manager` e inicie-o.

     É exibida uma janela do PowerShell corretamente configurada para o cmdlet AppxDebug.

3. Para habilitar a depuração de um aplicativo, é preciso especificar o identificador NomeCompletodoPacote do aplicativo. Para ver uma lista de todos os aplicativos que incluem o NomeCompletodoPacote, digite `Get-AppxPackage` no aviso do PowerShell.

4. No prompt do PowerShell, insira `Enable-AppxDebug` *PackageFullName* , em que *PackageFullName* é o identificador PackageFullName do aplicativo.

### <a name="attach-the-debugger"></a><a name="BKMK_Attach_the_debugger"></a>Anexar o depurador

> [!TIP]
> Os aplicativos JavaScript são executados em uma instância do processo wwahost.exe. Se outros aplicativos JavaScript estiverem em execução quando você anexa ao aplicativo, será necessário saber a ID do processo numérico (PID) do wwahost.exe em que o aplicativo está executando.
>
> A maneira mais fácil de lidar com essa situação é fechar todos os outros aplicativos JavaScript. Do contrário, você pode abrir o Gerenciador de Tarefas do Windows antes de iniciar o aplicativo e observar as IDs dos processos wwahost.exe. Quando você especifica o processo a ser anexado na caixa de diálogo **processos disponíveis** , o wwahost.exe do aplicativo terá uma ID diferente daquelas que você anotou.

 Para anexar o depurador:

1. No menu **Depurar**, escolha **Anexar ao Processo**.

    A caixa de diálogo **Anexar ao Processo** é exibida.

2. Para anexar a um aplicativo em um dispositivo remoto, especifique o dispositivo remoto na caixa **qualificador** . Você pode:

   - Insira o nome na caixa **qualificador** .

   - Escolha a seta para baixo na caixa **qualificador** e escolha o dispositivo em uma lista de dispositivos aos quais você anexou antes.

   - Escolha **Localizar** para escolher o dispositivo em uma lista de dispositivos na sub-rede local.

3. Especifique o tipo de código que você deseja depurar na caixa **anexar a** .

    Escolha **selecionar** e siga um destes procedimentos:

   - Escolha **determinar automaticamente o tipo de código a ser depurado**

   - Escolha **depurar esses tipos de código** e, em seguida, escolha um ou mais tipos na lista.

4. Na lista **processos disponíveis** , escolha o processo de **wwahost.exe** apropriado. Use a coluna **título** para identificar seu aplicativo.

5. Escolha **anexar**.

   O Visual Studio anexa o depurador ao processo. A execução continua até que um ponto de interrupção seja alcançado, você suspenda a execução manualmente, ocorra uma exceção sem tratamento ou o aplicativo chegue ao fim.

## <a name="see-also"></a>Consulte Também
 [Controlar a execução em um início rápido de sessão de depuração (JavaScript)](../debugger/control-execution-of-a-store-app-in-a-visual-studio-debug-session-for-windows-store-apps-javascript.md) [: Depurar HTML e CSS](../debugger/quickstart-debug-html-and-css.md) [disparar eventos de suspensão, retomada e segundo plano para a Windows Store)](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md) [depurar aplicativos no Visual Studio](../debugger/debug-store-apps-in-visual-studio.md)
