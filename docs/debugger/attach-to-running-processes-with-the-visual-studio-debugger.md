---
title: Anexar a processos em execução com o depurador | Microsoft Docs
ms.custom: seodec18
ms.date: 06/12/2020
ms.topic: conceptual
f1_keywords:
- vs.debug.processes.attach
- vs.debug.process
- vs.debug.programs
- vs.debug.detaching
- vs.debug.processes
- vs.debug.error.attach
- vs.debug.remotemachine
dev_langs:
- CSharp
- FSharp
- C++
- VB
helpviewer_keywords:
- remote debugging, attaching to programs
- processes, attaching to running processes
- Attach to Process dialog box
- debugging [Visual Studio], attaching to processes
- debugger, processes
ms.assetid: 27900e58-090c-4211-a309-b3e1496d5824
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5970e7e4408c826058cb27590254b278d4cdb9b7
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281000"
---
# <a name="attach-to-running-processes-with-the-visual-studio-debugger"></a>Anexar a processos em execução com o depurador do Visual Studio

Você pode anexar o depurador do Visual Studio a um processo em execução em um computador local ou remoto. Depois que o processo estiver em execução, selecione **depuração**  >  **anexar ao processo** ou pressione **Ctrl** + **ALT** + **P** no Visual Studio e use a caixa de diálogo **anexar ao processo** para anexar o depurador ao processo.

Você pode usar **anexar ao processo** para depurar a execução de aplicativos em computadores locais ou remotos, depurar vários processos simultaneamente, depurar aplicativos que não foram criados no Visual Studio ou depurar qualquer aplicativo que não tenha sido iniciado no Visual Studio com o depurador anexado. Por exemplo, se você estiver executando um aplicativo sem o depurador e clicar em uma exceção, você poderá anexar o depurador ao processo que executa o aplicativo e iniciar a depuração.

> [!TIP]
> Não tem certeza se deseja usar **anexar ao processo** para seu cenário de depuração? Consulte [cenários comuns de depuração](#BKMK_Scenarios).

## <a name="attach-to-a-running-process-on-your-local-machine"></a><a name="BKMK_Attach_to_a_running_process"></a>Anexar a um processo em execução no computador local

Para reanexar rapidamente a um processo que você anexou anteriormente, consulte [reanexar a um processo](#BKMK_reattach).

**Para anexar a um processo em seu computador local:**

1. No Visual Studio, selecione **depurar**  >  **anexar ao processo** (ou pressione **Ctrl** + **ALT** + **P**) para abrir a caixa de diálogo **anexar ao processo** .

1. Verifique o **tipo de conexão**.

   Na maioria dos cenários, você pode usar o **padrão**. Alguns cenários podem exigir um tipo de conexão diferente. Para obter mais informações, consulte outras seções neste artigo ou [cenários comuns de depuração](#BKMK_Scenarios).

1. Defina o **destino da conexão com** o nome do computador local.

   ![DBG_Basics_Attach_To_Process](../debugger/media/DBG_Basics_Attach_To_Process.png "DBG_Basics_Attach_To_Process")

1. Na lista **processos disponíveis** , localize e selecione o processo ou os processos aos quais você deseja anexar.

   - Para selecionar rapidamente um processo, digite seu nome ou primeira letra na caixa **Filtrar processos** .

   - Se você não souber o nome do processo, navegue pela lista ou veja [cenários comuns de depuração](#BKMK_Scenarios) para alguns nomes de processo comuns.

   >[!TIP]
   >Os processos podem iniciar e parar em segundo plano enquanto a caixa de diálogo **anexar ao processo** está aberta, de modo que a lista de processos em execução nem sempre seja atual. Você pode selecionar **Atualizar** a qualquer momento para ver a lista atual.

1. No campo **anexar a** , verifique se o tipo de código que você planeja Depurar está listado. A configuração **automática** padrão funciona para a maioria dos tipos de aplicativos.

   Se você estiver usando o tipo de conexão **padrão** , poderá selecionar manualmente o tipo de código ao qual deseja anexar. Caso contrário, a opção **selecionar** pode estar desabilitada.

   Para selecionar tipos de código manualmente:
   1. Clique em **Selecionar**.
   1. Na caixa de diálogo **Selecionar tipo de código** , selecione **depurar esses tipos de código**.
      Se ocorrer uma falha ao tentar anexar a um processo na lista, você poderá usar a caixa de diálogo [Selecionar tipo de código](../debugger/select-code-type-dialog-box.md) para ajudar a [solucionar](#BKMK_Troubleshoot_attach_errors) o problema.
   1. Selecione os tipos de código que você deseja depurar.
   1. Selecione **OK**.

1. Selecionar **Anexar**.

>[!NOTE]
>Você pode ser anexado a vários aplicativos para depuração, mas apenas um aplicativo está ativo no depurador por vez. Você pode definir o aplicativo ativo na barra de ferramentas do **local de depuração** do Visual Studio ou na janela **processos** .

## <a name="attach-to-a-process-on-a-remote-computer"></a><a name="BKMK_Attach_to_a_process_on_a_remote_computer"></a> Anexar a um processo em um computador remoto

Você também pode selecionar um computador remoto na caixa de diálogo **anexar ao processo** , exibir uma lista de processos disponíveis em execução no computador e anexar a um ou mais dos processos de depuração. O depurador remoto (*msvsmon.exe*) deve estar em execução no computador remoto. Para obter mais informações, consulte [depuração remota](../debugger/remote-debugging.md).

Para obter instruções mais completas sobre a depuração de aplicativos ASP.NET que foram implantados no IIS, consulte [depuração remota ASP.net em um computador IIS remoto](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md).

**Para anexar a um processo em execução em um computador remoto:**

1. No Visual Studio, selecione **depurar**  >  **anexar ao processo** (ou pressione **Ctrl** + **ALT** + **P**) para abrir a caixa de diálogo **anexar ao processo** .

1. Verifique o **tipo de conexão**.

   Na maioria dos cenários, você pode usar o **padrão**. Alguns cenários, como a depuração do Linux ou um aplicativo em contêiner, exigem um tipo de conexão diferente. Para obter mais informações, consulte outras seções neste artigo ou [cenários comuns de depuração](#BKMK_Scenarios).

1. Na caixa **destino da conexão** , selecione o computador remoto, usando um dos seguintes métodos:

   - Selecione a seta suspensa ao lado de **destino da conexão**e selecione o nome do computador na lista suspensa.
   - Digite o nome do computador na caixa **destino da conexão** e pressione **Enter**.

     Verifique se o Visual Studio adiciona a porta necessária ao nome do computador, que aparece no formato: ** \<remote computer name> :p classificar**

     ::: moniker range=">= vs-2019"

     > [!NOTE]
     > Se você não conseguir se conectar usando o nome do computador remoto, tente usar o endereço IP e a porta (por exemplo, `123.45.678.9:4022` ). 4024 é a porta padrão para o depurador remoto do Visual Studio 2019 x64. Para outras atribuições de porta do depurador remoto, consulte [atribuições de porta do depurador remoto](remote-debugger-port-assignments.md).

     ::: moniker-end
     ::: moniker range="vs-2017"

     > [!NOTE]
     > Se você não conseguir se conectar usando o nome do computador remoto, tente usar o endereço IP e a porta (por exemplo, `123.45.678.9:4022` ). 4022 é a porta padrão para o depurador remoto do Visual Studio 2017 x64. Para outras atribuições de porta do depurador remoto, consulte [atribuições de porta do depurador remoto](remote-debugger-port-assignments.md).

     ::: moniker-end

   - Selecione o botão **Localizar** ao lado da caixa **destino da conexão** para abrir a caixa de diálogo **conexões remotas** . A caixa de diálogo **conexões remotas** lista todos os dispositivos que estão em sua sub-rede local ou conectados diretamente ao seu computador. Talvez seja necessário [abrir a porta UDP 3702](../debugger/remote-debugger-port-assignments.md) no servidor para descobrir dispositivos remotos. Selecione o computador ou dispositivo desejado e clique em **selecionar**.

   > [!NOTE]
   > A configuração de **tipo de conexão** persiste entre sessões de depuração. A configuração de **destino de conexão** persiste entre sessões de depuração somente se uma conexão de depuração bem-sucedida tiver ocorrido com esse destino.

3. Clique em **Atualizar** para preencher a lista de **processos disponíveis** .

    >[!TIP]
    >Os processos podem iniciar e parar em segundo plano enquanto a caixa de diálogo **anexar ao processo** está aberta, de modo que a lista de processos em execução nem sempre seja atual. Você pode selecionar **Atualizar** a qualquer momento para ver a lista atual.

4. Na lista **processos disponíveis** , localize e selecione o processo ou os processos aos quais você deseja anexar.

   - Para selecionar rapidamente um processo, digite seu nome ou primeira letra na caixa **Filtrar processos** .

   - Se você não souber o nome do processo, navegue pela lista ou veja [cenários comuns de depuração](#BKMK_Scenarios) para alguns nomes de processo comuns.

   - Para localizar processos em execução em todas as contas de usuário, marque a caixa de seleção **Mostrar processos de todos os usuários** .

     >[!NOTE]
     >Se você tentar anexar a um processo de propriedade de uma conta de usuário não confiável, aparecerá uma confirmação da caixa de diálogo de aviso de segurança. Para obter mais informações, consulte [aviso de segurança: Anexar a um processo pertencente a um usuário não confiável pode ser perigoso. Se as informações a seguir parecerem suspeitas ou, se você não tiver certeza, não anexe a esse processo](../debugger/security-warning-attaching-to-a-process-owned-by-an-untrusted-user.md).

5. No campo **anexar a** , verifique se o tipo de código que você planeja Depurar está listado. A configuração **automática** padrão funciona para a maioria dos tipos de aplicativos.

   Se você estiver usando o tipo de conexão **padrão** , poderá selecionar manualmente o tipo de código ao qual deseja anexar. Caso contrário, a opção **selecionar** pode estar desabilitada.

   Para selecionar tipos de código manualmente:
   1. Clique em **Selecionar**.
   1. Na caixa de diálogo **Selecionar tipo de código** , selecione **depurar esses tipos de código**.
      Se ocorrer uma falha ao tentar anexar a um processo na lista, você poderá usar a caixa de diálogo [Selecionar tipo de código](../debugger/select-code-type-dialog-box.md) para ajudar a [solucionar](#BKMK_Troubleshoot_attach_errors) o problema.
   1. Selecione **OK**.

6. Selecionar **Anexar**.

>[!NOTE]
>Você pode ser anexado a vários aplicativos para depuração, mas apenas um aplicativo está ativo no depurador por vez. Você pode definir o aplicativo ativo na barra de ferramentas do **local de depuração** do Visual Studio ou na janela **processos** .

Em alguns casos, quando você depura em uma sessão Área de Trabalho Remota (serviços de terminal), a lista de **processos disponíveis** não exibirá todos os processos disponíveis. Se você estiver executando o Visual Studio como um usuário que tem uma conta de usuário limitada, a lista de **processos disponíveis** não mostrará os processos em execução na sessão 0. A sessão 0 é usada para serviços e outros processos de servidor, incluindo *w3wp.exe*. Você pode resolver o problema executando o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] em uma conta de administrador ou executando o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] no console do servidor em vez de uma sessão de Serviços de Terminal.

Se nenhuma dessas soluções alternativas é possível, uma terceira opção é anexar ao processo executando `vsjitdebugger.exe -p <ProcessId>` na linha de comando do Windows. Você pode determinar a ID do processo usando *tlist.exe*. Para obter *tlist.exe*, baixe e instale as ferramentas de depuração para Windows, disponíveis em [downloads do WDK e do WinDbg](/windows-hardware/drivers/download-the-wdk).

::: moniker range=">= vs-2019"

## <a name="attach-to-a-net-core-process-running-on-linux-using-ssh"></a>Anexar a um processo do .NET Core em execução no Linux usando SSH

Para obter mais informações, consulte [depuração remota do .NET Core em execução no Linux usando SSH](../debugger/remote-debugging-dotnet-core-linux-with-ssh.md).

## <a name="attach-to-a-process-running-on-a-linux-docker-container"></a><a name="BKMK_Linux_Docker_Attach"></a>Anexar a um processo em execução em um contêiner do Docker do Linux

Você pode anexar o depurador do Visual Studio a um processo em execução em um contêiner do Docker do Linux .NET Core em seu computador local ou remoto usando a caixa de diálogo **anexar ao processo** .

> [!IMPORTANT]
> Para usar esse recurso, você deve instalar a carga de trabalho de desenvolvimento entre plataformas do .NET Core e ter acesso local ao código-fonte.

**Para anexar a um processo em execução em um contêiner do Docker do Linux:**

1. No Visual Studio, selecione **depurar > anexar ao processo (CTRL + ALT + P)** para abrir a caixa de diálogo **anexar ao processo** .

![Anexar ao menu processar](../debugger/media/attach-process-menu.png "Attach_To_Process_Menu")

2. Defina o **tipo de conexão** como **Docker (contêiner do Linux)**.
3. Selecione **Localizar...** para definir o **destino de conexão** por meio da caixa de diálogo **selecionar contêiner do Docker** .

    Você pode depurar um processo de contêiner do Docker localmente ou remotamente.
    
    **Para depurar um processo de contêiner do Docker localmente:**
    1. Definir **host da CLI do Docker** para o **computador local**.
    1. Selecione um contêiner em execução para anexar na lista e clique em **OK**.
    
    ![Selecionar menu do contêiner do Docker](../debugger/media/select-docker-container.png "Select_Docker_Container_Menu")
 
    **B. para depurar um processo de contêiner do Docker remotamente:**
    
    > [!NOTE] 
    > Há duas opções para se conectar remotamente a um processo em execução em um contêiner do Docker. A primeira opção, para usar SSH, é ideal se você não tiver as ferramentas do Docker instaladas em seu computador local.  Se você tiver as ferramentas do Docker instaladas localmente e tiver um daemon do Docker configurado para aceitar solicitações remotas, tente a segunda opção, usando um daemon do Docker.

    1. ***Para se conectar a um computador remoto via SSH:***
        1. Selecione **Adicionar...** para se conectar a um sistema remoto.<br/>
        ![Conectar-se a um sistema remoto](../debugger/media/connect-remote-system.png "Conectar-se a um sistema remoto")
        1. Selecione um contêiner em execução ao qual anexar depois de se conectar ao SSH ou ao daemon com êxito e pressione **OK**.

    
    1. ***Para definir o destino para um contêiner remoto executando um processo por meio de um [daemon do Docker](https://docs.docker.com/engine/reference/commandline/dockerd/)***
        1. Especifique o endereço do daemon (ou seja, via TCP, IP, etc.) em **host do Docker (opcional)** e clique no link atualizar.
        1. Selecione um contêiner em execução ao qual anexar depois de se conectar ao daemon com êxito e pressione **OK**.

4. Escolha o processo de contêiner correspondente na lista de **processos disponíveis** e selecione **anexar** para iniciar a depuração do processo de contêiner do C# no Visual Studio!

    ![Menu de anexo do Docker concluído](../debugger/media/docker-attach-complete.png "Menu de anexação do Docker do Linux concluído")
    

## <a name="attach-to-a-process-running-on-a-windows-docker-container"></a><a name="BKMK_Windows_Docker_Attach"></a>Anexar a um processo em execução em um contêiner do Docker do Windows

Você pode anexar o depurador do Visual Studio a um processo em execução em um contêiner do Docker do Windows em seu computador local usando a caixa de diálogo **anexar ao processo** .

> [!IMPORTANT]
> Para usar esse recurso com um processo do .NET Core, você deve instalar a carga de trabalho de desenvolvimento entre plataformas do .NET Core e ter acesso local ao código-fonte.

**Para anexar a um processo em execução em um contêiner do Docker do Windows:**

1. No Visual Studio, selecione **depurar > anexar ao processo** (ou **Ctrl + Alt + P**) para abrir a caixa de diálogo **anexar ao processo** .

   ![Anexar ao menu processar](../debugger/media/attach-process-menu-docker-windows.png "Attach_To_Process_Menu")

2. Defina o **tipo de conexão** como **Docker (contêiner do Windows)**.
3. Selecione **Localizar...** para definir o **destino de conexão** usando a caixa de diálogo **selecionar contêiner do Docker** .

    > [!IMPORTANT]
    > O processo de destino deve ter a mesma arquitetura de processador que o contêiner do Windows do Docker em que está sendo executado.
    
   A definição do destino para um contêiner remoto via SSH não está disponível no momento e só pode ser feita usando um daemon do Docker.
    
    ***Para definir o destino para um contêiner remoto executando um processo por meio de um [daemon do Docker](https://docs.docker.com/engine/reference/commandline/dockerd/)***
    1. Especifique o endereço do daemon (ou seja, via TCP, IP, etc.) em **host do Docker (opcional)** e clique no link atualizar. 

    1. Selecione um contêiner em execução ao qual anexar depois de se conectar ao daemon com êxito e escolha OK.
    
4. Escolha o processo de contêiner correspondente na lista de **processos disponíveis** e selecione **anexar** para iniciar a depuração do processo de contêiner do C#.

    ![Menu de anexo do Docker concluído](../debugger/media/docker-attach-complete-windows.png "Menu de anexação do Docker do Windows concluído")
    

5.  Escolha o processo de contêiner correspondente na lista de processos disponíveis e escolha **anexar** para iniciar a depuração do processo de contêiner do C#.


::: moniker-end

## <a name="reattach-to-a-process"></a><a name="BKMK_reattach"></a>Reanexar a um processo

Você pode reanexar rapidamente aos processos aos quais você estava anexado anteriormente, escolhendo **depurar**  >  **reanexar para processar** (**Shift** + **ALT** + **P**). Quando você escolher esse comando, o depurador tentará imediatamente se anexar aos últimos processos anexados pela primeira vez tentando corresponder à ID do processo anterior e, se isso falhar, correspondendo ao nome do processo anterior. Se nenhuma correspondência for encontrada ou se vários processos tiverem o mesmo nome, a caixa de diálogo **anexar ao processo** será aberta para que você possa selecionar o processo correto.

> [!NOTE]
> O comando **reanexar ao processo** está disponível a partir do Visual Studio 2017.

## <a name="common-debugging-scenarios"></a><a name="BKMK_Scenarios"></a>Cenários comuns de depuração

Para ajudá-lo a determinar se deve usar **anexar ao processo** e a qual processo anexar, a tabela a seguir mostra alguns cenários comuns de depuração, com links para mais instruções, quando disponíveis. (A lista não é exaustiva.)

Para alguns tipos de aplicativos, como aplicativos da UWP (Universal Windows app), você não anexa diretamente a um nome de processo, mas usa a opção de menu **depurar pacote de aplicativo instalado** no Visual Studio em vez disso (consulte a tabela).

Para que o depurador se anexe ao código escrito em C++, o código precisa emitir `DebuggableAttribute`. Você pode adicionar isso ao seu código automaticamente vinculando à opção do vinculador [/ASSEMBLYDEBUG](/cpp/build/reference/assemblydebug-add-debuggableattribute).

Para depuração de script do lado do cliente, a depuração de script deve ser habilitada no navegador. Para depurar o script do lado do cliente no Chrome, escolha **JavaScript (Chrome)** ou **JavaScript (Microsoft Edge-Chromium)** como o tipo de código e, dependendo do seu tipo de aplicativo, talvez seja necessário fechar todas as instâncias do Chrome e iniciar o navegador no modo de depuração (tipo `chrome.exe --remote-debugging-port=9222` de uma linha de comando). Em versões anteriores do Visual Studio, o depurador de scripts do Chrome era o **Web kit**.

Para selecionar rapidamente um processo em execução para anexar ao, no Visual Studio, digite **Ctrl** + **ALT** + **P**e digite a primeira letra do nome do processo.

|Cenário|Método de depuração|Nome do processo|Anotações e links|
|-|-|-|-|
|Depuração remota ASP.NET 4 ou 4,5 em um servidor IIS|Usar as ferramentas remotas e **anexar ao processo**|*w3wp.exe*|Consulte [depuração remota ASP.net em um computador IIS remoto](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)|
|ASP.NET Core de depuração remota em um servidor IIS|Usar as ferramentas remotas e **anexar ao processo**|*w3wp.exe* ou *dotnet.exe*|A partir do .NET Core 3, o processo de *w3wp.exe* é usado para o [modelo de hospedagem no aplicativo](/aspnet/core/host-and-deploy/aspnet-core-module?view=aspnetcore-3.1#hosting-models)padrão. Para a implantação de aplicativo, consulte [publicar no IIS](/aspnet/core/host-and-deploy/iis/). Para obter informações mais detalhadas, consulte [depuração remota ASP.NET Core em um computador IIS remoto](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md#BKMK_attach)|
|Depurar script do lado do cliente em um servidor IIS local, para tipos de aplicativos com suporte |Usar **anexar ao processo**|*chrome.exe*, *MicrosoftEdgeCP.exe* ou *iexplore.exe*|A depuração de script deve ser habilitada. Para o Chrome, você também deve executar o Chrome no modo de depuração (tipo `chrome.exe --remote-debugging-port=9222` de uma linha de comando) e selecionar **JavaScript (Chrome)** no campo **anexar a** .|
|Depurar um aplicativo em C#, Visual Basic ou C++ no computador local|Usar a depuração padrão (**F5**) ou **anexar ao processo**|*\<appname>. exe*|Na maioria dos cenários, use a depuração padrão e não **anexe ao processo**.|
|Depuração remota de um aplicativo de área de trabalho do Windows|Ferramentas remotas|N/D| Consulte [depuração remota de um aplicativo C# ou Visual Basic](../debugger/remote-debugging-csharp.md) ou [depuração remota de um aplicativo C++](../debugger/remote-debugging-cpp.md)|
|Depurar o .NET Core no Linux|Usar **anexar ao processo**|*dotnet.exe*|Para usar o SSH, consulte [depuração remota do .NET Core em execução no Linux usando SSH](../debugger/remote-debugging-dotnet-core-linux-with-ssh.md). Para aplicativos em contêineres, consulte as seções anteriores neste artigo.|
|Python de depuração remota no Linux|Usar **anexar ao processo**|*debugpy*|Consulte [anexar remotamente de ferramentas do Python](../python/debugging-python-code-on-remote-linux-machines.md#attach-remotely-from-python-tools)|
|Depurar um aplicativo ASP.NET no computador local depois de iniciar o aplicativo sem o depurador|Usar **anexar ao processo**|*iiexpress.exe*|Isso pode ser útil para fazer com que seu aplicativo seja carregado mais rapidamente, como (por exemplo) durante a criação de perfil. |
|Depurar outros tipos de aplicativos com suporte em um processo de servidor|Se o servidor for remoto, use as ferramentas remotas e **anexe ao processo**|*chrome.exe*, *iexplore.exe*ou outros processos|Se necessário, use Monitor de Recursos para ajudar a identificar o processo. Consulte [depuração remota](../debugger/remote-debugging.md).|
|Depuração remota de um aplicativo universal do Windows (UWP), OneCore, HoloLens ou aplicativo de IoT|Depurar pacote do aplicativo instalado|N/D|Confira [depurar um pacote do aplicativo instalado](debug-installed-app-package.md) em vez de usar **anexar ao processo**|
|Depurar um aplicativo universal do Windows (UWP), OneCore, HoloLens ou aplicativo IoT que você não iniciou no Visual Studio|Depurar pacote do aplicativo instalado|N/D|Confira [depurar um pacote do aplicativo instalado](debug-installed-app-package.md) em vez de usar **anexar ao processo**|

## <a name="use-debugger-features"></a>Usar recursos do depurador

Para usar os recursos completos do depurador do Visual Studio (como atingir pontos de interrupção) ao anexar a um processo, o aplicativo deve corresponder exatamente à fonte local e aos símbolos. Ou seja, o depurador deve ser capaz de carregar os [arquivos de símbolo (. pdb)](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)corretos. Por padrão, isso requer uma compilação de depuração.

Para cenários de depuração remota, você deve ter o código-fonte (ou uma cópia do código-fonte) já aberto no Visual Studio. Os binários de aplicativo compilados no computador remoto devem vir da mesma compilação que no computador local.

Em alguns cenários de depuração local, você pode depurar no Visual Studio sem acesso à origem se os arquivos de símbolo corretos estiverem presentes com o aplicativo. Por padrão, isso requer uma compilação de depuração. Para obter mais informações, consulte [especificar o símbolo e os arquivos de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).

## <a name="troubleshoot-attach-errors"></a><a name="BKMK_Troubleshoot_attach_errors"></a> Solucionar problemas de anexo

Em alguns cenários, o depurador pode precisar de ajuda para identificar corretamente o tipo de código a ser depurado. Se os valores de conexão estiverem definidos corretamente (você pode exibir o processo correto na lista de **processos disponíveis** ), mas o depurador não conseguir se conectar, tente selecionar o tipo de conexão mais apropriado na lista **tipo de conexão** , que pode ser necessária, por exemplo, se você estiver depurando um aplicativo Linux ou Python. Se você estiver usando o tipo de conexão padrão, você pode, como alternativa, selecionar o tipo específico de código ao qual se conectar, conforme descrito mais adiante nesta seção.

Quando o depurador se anexa a um processo em execução, o processo pode conter um ou mais tipos de código. Os tipos de código aos quais o depurador pode se anexar são exibidos e selecionados na caixa de diálogo [Selecionar Tipo de Código](../debugger/select-code-type-dialog-box.md).

Às vezes, o depurador pode ser anexado com êxito a um tipo de código, mas não a outro tipo de código. Normalmente, isso ocorre quando:

- Você tenta anexar a um processo que está sendo executado em um computador remoto. O computador remoto pode ter componentes de depuração remota instalados para alguns tipos de código mas não para outros.
- Você tenta anexar a dois ou mais processos para depuração direta de banco de dados. A depuração de SQL dá suporte à anexação de apenas um único processo.

Se o depurador for capaz de anexar a alguns tipos de código, mas não a todos, você verá uma mensagem identificando quais tipos não puderam ser anexados.

Se o depurador for anexado com êxito a pelo menos um tipo de código, você poderá depurar o processo. Você poderá depurar apenas os tipos de código que foram anexados com êxito. O código não anexado no processo ainda será executado, mas você não poderá definir pontos de interrupção, exibir dados ou executar outras operações de depuração nesse código.

Se você quiser obter informações mais específicas sobre por que o depurador falhou ao anexar a um tipo de código, tente reanexar a esse tipo de código.

**Para obter informações específicas sobre o motivo de um tipo de código ter falhado na anexação:**

1. Desanexe do processo. No menu **depurar** , selecione **desanexar tudo**.

1. Reanexe ao processo, selecionando apenas o tipo de código que falhou ao anexar.

    1. Na caixa de diálogo **Anexar ao Processo**, selecione o processo na lista **Processos Disponíveis**.

    2. Selecione **Selecionar**.

    3. Na caixa de diálogo **Tipo de Código Selecionado**, selecione **Depurar esses tipos de código** e o tipo de código que falhou em ser anexado. Desmarque os outros tipos de código.

    4. Selecione **OK**.

    5. Na caixa de diálogo **anexar ao processo** , selecione **anexar**.

    Desta vez, o anexo falhará completamente e você receberá uma mensagem de erro específica.

## <a name="see-also"></a>Veja também

- [Depurar vários processos](../debugger/debug-multiple-processes.md)
- [Depuração Just-in-time](../debugger/just-in-time-debugging-in-visual-studio.md)
- [Depuração remota](../debugger/remote-debugging.md)
