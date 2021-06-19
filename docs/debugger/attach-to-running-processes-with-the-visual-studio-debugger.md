---
title: Anexar a processos em execução com o depurador
description: Descubra como anexar o Visual Studio depurador a um processo em execução em um computador local ou remoto.
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 5e3836403af80d06a2ecaa7f77cb7f49f0c6f0e8
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389781"
---
# <a name="attach-to-running-processes-with-the-visual-studio-debugger"></a>Anexar a processos em execução com o depurador do Visual Studio

Você pode anexar o Visual Studio depurador a um processo em execução em um computador local ou remoto. Depois que o processo for executado, selecione **Depurar** Anexar ao Processo ou pressione Ctrl Alt p no Visual Studio e use a caixa de diálogo Anexar ao Processo para anexar o  >    +  +  depurador ao processo. 

Você pode  usar Anexar ao Processo para depurar aplicativos em execução em computadores locais ou remotos, depurar vários processos simultaneamente, depurar aplicativos que não foram criados no Visual Studio ou depurar qualquer aplicativo que você não tenha Visual Studio com o depurador anexado. Por exemplo, se você estiver executando um aplicativo sem o depurador e atingir uma exceção, poderá anexar o depurador ao processo que executa o aplicativo e iniciar a depuração.

> [!TIP]
> Não tem certeza se deve usar **Anexar ao Processo para** seu cenário de depuração? Consulte [Cenários comuns de depuração.](#BKMK_Scenarios)

## <a name="attach-to-a-running-process-on-your-local-machine"></a><a name="BKMK_Attach_to_a_running_process"></a> Anexar a um processo em execução no computador local

Para anexar rapidamente a um processo anexado anteriormente, consulte [Reattach a um processo](#BKMK_reattach).

**Para anexar a um processo no computador local:**

1. No Visual Studio, selecione **Depurar**  >  **Anexar** ao Processo (ou pressione **Ctrl** Alt P ) para abrir a caixa de +  +  **diálogo Anexar** ao Processo.

1. Verifique o **Tipo de conexão**.

   Na maioria dos cenários, você pode usar **o Padrão.** Alguns cenários podem exigir um tipo de conexão diferente. Para obter mais informações, consulte outras seções neste artigo ou Cenários comuns [de depuração.](#BKMK_Scenarios)

1. De definir o **Destino da conexão** no nome do computador local.

   ![Captura de tela da caixa de diálogo Anexar ao Processo, com o destino de conexão definido como o nome do computador local.](../debugger/media/DBG_Basics_Attach_To_Process.png)

1. Na lista **Processos disponíveis,** encontre e selecione o processo ou os processos aos que você deseja anexar.

   - Para selecionar rapidamente um processo, digite seu nome ou primeira letra na **caixa Filtrar** processos.

   - Se você não sabe o nome do processo, navegue pela lista ou consulte [Cenários](#BKMK_Scenarios) comuns de depuração para alguns nomes de processo comuns.

   >[!TIP]
   >Os processos podem iniciar e  parar em segundo plano enquanto a caixa de diálogo Anexar ao Processo está aberta, portanto, a lista de processos em execução pode nem sempre ser atual. Você pode selecionar **Atualizar** a qualquer momento para ver a lista atual.

1. No campo **Anexar a** , certifique-se de que o tipo de código que você planeja depurar está listado. A **configuração automática** padrão funciona para a maioria dos tipos de aplicativo.

   Se você estiver usando o **tipo de** conexão Padrão, poderá selecionar manualmente o tipo de código ao qual deseja anexar. Caso contrário, **a opção** Selecionar poderá ser desabilitada.

   Para selecionar tipos de código manualmente:
   1. Clique em **Selecionar**.
   1. Na caixa **de diálogo Selecionar Tipo** de Código, selecione **Depurar esses tipos de código**.
      Se você tiver uma falha ao tentar anexar a um [](../debugger/select-code-type-dialog-box.md) processo na lista, poderá usar a caixa de diálogo Selecionar Tipo de Código para ajudar a [solucionar](#BKMK_Troubleshoot_attach_errors) o problema.
   1. Selecione os tipos de código que você deseja depurar.
   1. Selecione **OK**.

1. Selecionar **Anexar**.

>[!NOTE]
>Você pode ser anexado a vários aplicativos para depuração, mas apenas um aplicativo está ativo no depurador por vez. Você pode definir o aplicativo ativo na barra de ferramentas Visual Studio **Local de Depuração** ou na **janela** Processos.

## <a name="attach-to-a-process-on-a-remote-computer"></a><a name="BKMK_Attach_to_a_process_on_a_remote_computer"></a> Anexar a um processo em um computador remoto

Você também pode selecionar um  computador remoto na caixa de diálogo Anexar ao Processo, exibir uma lista de processos disponíveis em execução no computador e anexar a um ou mais dos processos para depuração. O depurador remoto (*msvsmon.exe*) deve estar em execução no computador remoto. Para obter mais informações, consulte [Depuração remota.](../debugger/remote-debugging.md)

Para obter instruções mais completas para depurar ASP.NET aplicativos que foram implantados no IIS, consulte Depuração remota ASP.NET em um [computador IIS remoto.](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)

**Para anexar a um processo em execução em um computador remoto:**

1. No Visual Studio, selecione **Depurar**  >  **Anexar** ao Processo (ou pressione **Ctrl** Alt P ) para abrir a caixa de +  +  **diálogo Anexar** ao Processo.

1. Verifique o **Tipo de conexão**.

   Na maioria dos cenários, você pode usar **o Padrão.** Alguns cenários, como depuração do Linux ou um aplicativo em contêineres, exigem um tipo de conexão diferente. Para obter mais informações, consulte outras seções neste artigo ou Cenários comuns [de depuração.](#BKMK_Scenarios)

1. Na caixa **Destino da** conexão, selecione o computador remoto usando um dos seguintes métodos:

   - Selecione a seta para baixo ao lado de **Destino da** conexão e selecione o nome do computador na lista lista listada.
   - Digite o nome do computador na **caixa Destino da** conexão e pressione **Enter**.

     Verifique se Visual Studio adiciona a porta necessária ao nome do computador, que aparece no formato: **\<remote computer name> :p out**

     ::: moniker range=">= vs-2019"

     > [!NOTE]
     > Se você não conseguir se conectar usando o nome do computador remoto, tente usar o ENDEREÇO IP e a porta (por exemplo, `123.45.678.9:4022` ). 4024 é a porta padrão para o depurador remoto Visual Studio 2019 x64. Para outras atribuições de porta do depurador remoto, consulte [Atribuições de porta do depurador remoto.](remote-debugger-port-assignments.md)

     ::: moniker-end
     ::: moniker range="vs-2017"

     > [!NOTE]
     > Se você não conseguir se conectar usando o nome do computador remoto, tente usar o ENDEREÇO IP e a porta (por exemplo, `123.45.678.9:4022` ). 4022 é a porta padrão para o depurador remoto Visual Studio 2017 x64. Para outras atribuições de porta do depurador remoto, consulte [Atribuições de porta do depurador remoto.](remote-debugger-port-assignments.md)

     ::: moniker-end

   - Selecione o **botão Encontrar** ao lado da caixa **de destino** Conexão para abrir a caixa de **diálogo Conexões** Remotas. A **caixa de diálogo** Conexões Remotas lista todos os dispositivos que estão em sua sub-rede local ou conectados diretamente ao computador. Talvez seja necessário abrir [a porta UDP 3702](../debugger/remote-debugger-port-assignments.md) no servidor para descobrir dispositivos remotos. Selecione o computador ou dispositivo que você deseja e clique **em Selecionar**.

   > [!NOTE]
   > A **configuração Tipo** de conexão persiste entre as sessões de depuração. A **configuração Destino** de conexão persiste entre as sessões de depuração somente se uma conexão de depuração bem-sucedida tiver ocorrido com esse destino.

3. Clique **em** Atualizar para preencher **a lista Processos disponíveis.**

    >[!TIP]
    >Os processos podem iniciar e  parar em segundo plano enquanto a caixa de diálogo Anexar ao Processo está aberta, portanto, a lista de processos em execução pode nem sempre ser atual. Você pode selecionar **Atualizar** a qualquer momento para ver a lista atual.

4. Na lista **Processos disponíveis,** encontre e selecione o processo ou os processos aos que você deseja anexar.

   - Para selecionar rapidamente um processo, digite seu nome ou primeira letra na **caixa Filtrar** processos.

   - Se você não sabe o nome do processo, navegue pela lista ou consulte [Cenários](#BKMK_Scenarios) comuns de depuração para alguns nomes de processo comuns.

   - Para encontrar processos em execução em todas as contas de usuário, marque a caixa de seleção Mostrar **processos de todos os** usuários.

     >[!NOTE]
     >Se você tentar anexar a um processo de propriedade de uma conta de usuário não confiável, aparecerá uma confirmação da caixa de diálogo de aviso de segurança. Para obter mais informações, consulte [aviso de segurança: Anexar a um processo pertencente a um usuário não confiável pode ser perigoso. Se as informações a seguir parecerem suspeitas ou, se você não tiver certeza, não anexe a esse processo](../debugger/security-warning-attaching-to-a-process-owned-by-an-untrusted-user.md).

5. No campo **Anexar a** , certifique-se de que o tipo de código que você planeja depurar está listado. A **configuração automática** padrão funciona para a maioria dos tipos de aplicativo.

   Se você estiver usando o **tipo de** conexão Padrão, poderá selecionar manualmente o tipo de código ao qual deseja anexar. Caso contrário, **a opção** Selecionar poderá ser desabilitada.

   Para selecionar tipos de código manualmente:
   1. Clique em **Selecionar**.
   1. Na caixa **de diálogo Selecionar Tipo** de Código, selecione **Depurar esses tipos de código**.
      Se você tiver uma falha ao tentar anexar a um [](../debugger/select-code-type-dialog-box.md) processo na lista, poderá usar a caixa de diálogo Selecionar Tipo de Código para ajudar a [solucionar](#BKMK_Troubleshoot_attach_errors) o problema.
   1. Selecione **OK**.

6. Selecionar **Anexar**.

>[!NOTE]
>Você pode ser anexado a vários aplicativos para depuração, mas apenas um aplicativo está ativo no depurador por vez. Você pode definir o aplicativo ativo na barra de ferramentas Visual Studio **Local de Depuração** ou na **janela** Processos.

Em alguns casos, quando você depura em uma sessão  Área de Trabalho Remota (Serviços de Terminal), a lista Processos disponíveis não exibirá todos os processos disponíveis. Se você estiver executando Visual Studio como um usuário que  tem uma conta de usuário limitada, a lista Processos disponíveis não mostrará os processos em execução na Sessão 0. A sessão 0 é usada para serviços e outros processos de servidor, incluindo *w3wp.exe*. Você pode resolver o problema executando o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] em uma conta de administrador ou executando o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] no console do servidor em vez de uma sessão de Serviços de Terminal.

Se nenhuma dessas soluções alternativas é possível, uma terceira opção é anexar ao processo executando `vsjitdebugger.exe -p <ProcessId>` na linha de comando do Windows. Você pode determinar a ID do processo *usandotlist.exe*. Para obter *tlist.exe*, baixe e instale as Ferramentas de Depuração para Windows, disponível em  [WDK e WinDbg baixa](/windows-hardware/drivers/download-the-wdk).

## <a name="attach-to-a-net-core-process-running-on-linux-using-ssh"></a>Anexar a um processo do .NET Core em execução no Linux usando SSH

Para obter mais informações, consulte [Depuração remota do .NET Core em execução no Linux usando SSH](../debugger/remote-debugging-dotnet-core-linux-with-ssh.md).

::: moniker range=">= vs-2019"

## <a name="attach-to-a-process-running-on-a-docker-container"></a><a name="BKMK_Linux_Docker_Attach"></a> Anexar a um processo em execução em um contêiner do Docker

A partir Visual Studio 2019, você pode anexar o Visual Studio depurador a um processo em execução em um contêiner do Docker. Para um contêiner do Docker do .NET Core do Linux, consulte [Anexar a um processo em execução em um contêiner do Docker do Linux.](../debugger/attach-to-process-running-in-docker-container.md#attach-to-a-process-running-on-a-linux-docker-container) Para um contêiner do Docker do Windows, consulte [Anexar a um processo em execução em um contêiner do Docker do Windows.](../debugger/attach-to-process-running-in-docker-container.md#attach-to-a-process-running-on-a-windows-docker-container)

::: moniker-end

## <a name="reattach-to-a-process"></a><a name="BKMK_reattach"></a> Reattar a um processo

Você pode reacopiá-lo rapidamente aos processos aos quais foi anexado anteriormente escolhendo **Depurar**  >  **Rea anexar** ao Processo (**Shift** + **Alt** + **P**). Quando você escolher esse comando, o depurador tentará anexar imediatamente aos últimos processos anexados, primeiro tentando corresponder à ID do processo anterior e, se isso falhar, correspondendo ao nome do processo anterior. Se nenhuma corresponde for encontrada ou se vários  processos têm o mesmo nome, a caixa de diálogo Anexar ao Processo será aberta para que você possa selecionar o processo correto.

> [!NOTE]
> O **comando Reattach to Process** está disponível a partir do Visual Studio 2017.

## <a name="common-debugging-scenarios"></a><a name="BKMK_Scenarios"></a> Cenários comuns de depuração

Para ajudá-lo a  determinar se deve usar Anexar ao Processo e a qual processo anexar, a tabela a seguir mostra alguns cenários comuns de depuração, com links para mais instruções, quando disponíveis. (A lista não é completa.)

Para alguns tipos de aplicativos, como aplicativos UWP (Aplicativo Universal do Windows), você não anexa diretamente a um nome de processo, mas usa a opção de menu **Depurar** Pacote do Aplicativo Instalado no Visual Studio em vez disso (consulte tabela).

Para que o depurador se anexe ao código escrito em C++, o código precisa emitir `DebuggableAttribute`. Você pode adicionar isso ao seu código automaticamente vinculando à opção do vinculador [/ASSEMBLYDEBUG](/cpp/build/reference/assemblydebug-add-debuggableattribute).

Para depuração de script do lado do cliente, a depuração de script deve ser habilitada no navegador. Para depurar o script do lado do cliente no Chrome, escolha **JavaScript (Chrome)** ou **JavaScript (Microsoft Edge – Chromium)** como o tipo de código e, dependendo do tipo de aplicativo, talvez seja necessário fechar todas as instâncias do Chrome e iniciar o navegador no modo de depuração (digite de uma linha de `chrome.exe --remote-debugging-port=9222` comando). Em versões anteriores do Visual Studio, o depurador de script para Chrome era **o Kit web**.

Para selecionar rapidamente um processo em execução ao qual anexar, em Visual Studio, digite **Ctrl** Alt P e digite a primeira +  + letra do nome do processo.

|Cenário|Método de depuração|Nome do processo|Observações e links|
|-|-|-|-|
|Depuração remota ASP.NET 4 ou 4.5 em um servidor IIS|Usar ferramentas remotas e **Anexar ao Processo**|*w3wp.exe*|Confira [Depuração remota ASP.NET em um computador IIS remoto](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)|
|Depuração remota ASP.NET Core em um servidor IIS|Usar ferramentas remotas e **Anexar ao Processo**|*w3wp.exe* ou *dotnet.exe*|A partir do .NET Core 3, *ow3wp.exe* é usado para o modelo de hospedagem padrão [no aplicativo.](/aspnet/core/host-and-deploy/aspnet-core-module?view=aspnetcore-3.1&preserve-view=true#hosting-models) Para implantação de aplicativo, [consulte Publicar no IIS.](/aspnet/core/host-and-deploy/iis/) Para obter informações mais detalhadas, consulte [Depuração remota ASP.NET Core em um computador IIS remoto](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md#BKMK_attach)|
|Depurar script do lado do cliente em um servidor IIS local para tipos de aplicativo com suporte |Usar **Anexar ao Processo**|*chrome.exe*, *MicrosoftEdgeCP.exe* ou *iexplore.exe*|A depuração de script deve ser habilitada. Para o Chrome, você também deve executar o Chrome no modo de depuração (digite de uma linha de comando) e selecione `chrome.exe --remote-debugging-port=9222` **JavaScript (Chrome)** no campo Anexar **a.**|
|Depurar um aplicativo C#, Visual Basic ou C++ no computador local|Usar a depuração padrão (**F5**) ou **Anexar ao Processo**|*\<appname>.exe*|Na maioria dos cenários, use a depuração padrão e não **Anexar ao Processo**.|
|Depurar remotamente um aplicativo da área de trabalho do Windows|Ferramentas remotas|N/D| Confira [Depurar remotamente um aplicativo C# ou Visual Basic ou](../debugger/remote-debugging-csharp.md) [Depurar remotamente um aplicativo C++](../debugger/remote-debugging-cpp.md)|
|Depuração do .NET Core no Linux|Usar **Anexar ao Processo**|*dotnet.exe* ou um nome de processo exclusivo|Para usar o SSH, consulte [Depuração remota do .NET Core em execução no Linux usando SSH](../debugger/remote-debugging-dotnet-core-linux-with-ssh.md). Para aplicativos em contêineres, [consulte Anexar a um processo em execução em um contêiner do Docker](../debugger/attach-to-process-running-in-docker-container.md#attach-to-a-process-running-on-a-linux-docker-container).|
|Depurar um aplicativo em contêineres|Usar **Anexar ao Processo**|*dotnet.exe* ou um nome de processo exclusivo|Confira [Anexar a um processo em execução em um contêiner do Docker](../debugger/attach-to-process-running-in-docker-container.md)|
|Depuração remota do Python no Linux|Usar **Anexar ao Processo**|*debugpy*|Confira [Anexar remotamente das Ferramentas python](../python/debugging-python-code-on-remote-linux-machines.md#attach-remotely-from-python-tools)|
|Depurar um ASP.NET aplicativo no computador local depois de iniciar o aplicativo sem o depurador|Usar **Anexar ao Processo**|*iiexpress.exe*|Isso pode ser útil para tornar o carregamento do aplicativo mais rápido, como (por exemplo) ao criação de perfil. |
|Depurar outros tipos de aplicativo com suporte em um processo de servidor|Se o servidor for remoto, use ferramentas remotas e **Anexar ao Processo**|*chrome.exe*, *iexplore.exe* ou outros processos|Se necessário, use Monitor de Recursos para ajudar a identificar o processo. Consulte [Depuração remota.](../debugger/remote-debugging.md)|
|Depurar remotamente um aplicativo UWP (Universal do Windows), OneCore, HoloLens ou IoT|Depurar pacote do aplicativo instalado|N/D|Consulte [Depurar um pacote de aplicativo instalado em](debug-installed-app-package.md) vez de usar **Anexar ao Processo**|
|Depurar um aplicativo UWP (Universal do Windows), OneCore, HoloLens ou IoT que você não começou do Visual Studio|Depurar pacote do aplicativo instalado|N/D|Consulte [Depurar um pacote de aplicativo instalado em](debug-installed-app-package.md) vez de usar **Anexar ao Processo**|

## <a name="use-debugger-features"></a>Usar recursos do depurador

Para usar os recursos completos do depurador Visual Studio (como atingir pontos de interrupção) ao anexar a um processo, o aplicativo deve corresponder exatamente à origem e aos símbolos locais. Ou seja, o depurador deve ser capaz de carregar os arquivos de símbolo [corretos (.pdb).](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md) Por padrão, isso requer um build de depuração.

Para cenários de depuração remota, você deve ter o código-fonte (ou uma cópia do código-fonte) já aberto Visual Studio. Os binários de aplicativo compilados no computador remoto devem vir do mesmo build que no computador local.

Em alguns cenários de depuração local, você pode depurar no Visual Studio sem acesso à origem se os arquivos de símbolo corretos estão presentes com o aplicativo. Por padrão, isso requer um build de depuração. Para obter mais informações, consulte [Especificar arquivos de símbolo e de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).

## <a name="troubleshoot-attach-errors"></a><a name="BKMK_Troubleshoot_attach_errors"></a> Solucionar problemas de anexo

Em alguns cenários, o depurador pode precisar de ajuda para identificar corretamente o tipo de código a ser depurado. Se os valores de conexão estão definidos corretamente  (você pode exibir o processo correto na lista Processos disponíveis), mas  o depurador não conseguir anexar, tente selecionar o tipo de conexão mais apropriado na lista Tipo de conexão, o que pode ser necessário, por exemplo, se você estiver depurando um aplicativo Linux ou Python. Se você estiver usando o tipo de conexão Padrão, poderá, como alternativa, selecionar o tipo específico de código ao qual se conectar, conforme descrito posteriormente nesta seção.

Quando o depurador se anexa a um processo em execução, o processo pode conter um ou mais tipos de código. Os tipos de código aos quais o depurador pode se anexar são exibidos e selecionados na caixa de diálogo [Selecionar Tipo de Código](../debugger/select-code-type-dialog-box.md).

Às vezes, o depurador pode ser anexado com êxito a um tipo de código, mas não a outro tipo de código. Normalmente, isso ocorre quando:

- Você tenta anexar a um processo que está em execução em um computador remoto. O computador remoto pode ter componentes de depuração remota instalados para alguns tipos de código mas não para outros.
- Você tenta anexar a dois ou mais processos para depuração direta de banco de dados. A depuração de SQL dá suporte à anexação de apenas um único processo.

Se o depurador for capaz de anexar a alguns, mas não a todos os tipos de código, você verá uma mensagem identificando quais tipos não foram anexados.

Se o depurador for anexado com êxito a pelo menos um tipo de código, você poderá depurar o processo. Você poderá depurar apenas os tipos de código que foram anexados com êxito. O código desconectado no processo ainda será executado, mas você não poderá definir pontos de interrupção, exibir dados ou executar outras operações de depuração nesse código.

Se você quiser informações mais específicas sobre por que o depurador não foi anexado a um tipo de código, tente reanexá-lo somente a esse tipo de código.

**Para obter informações específicas sobre o motivo de um tipo de código ter falhado na anexação:**

1. Desanexe do processo. No menu **Depurar,** selecione **Desconectar Tudo.**

1. Reanexe ao processo, selecionando apenas o tipo de código que não foi anexado.

    1. Na caixa de diálogo **Anexar ao Processo**, selecione o processo na lista **Processos Disponíveis**.

    2. Selecione **Selecionar**.

    3. Na caixa de diálogo **Tipo de Código Selecionado**, selecione **Depurar esses tipos de código** e o tipo de código que falhou em ser anexado. Desmarque os outros tipos de código.

    4. Selecione **OK**.

    5. Na caixa de diálogo **anexar ao processo** , selecione **anexar**.

    Desta vez, o anexo falhará completamente e você receberá uma mensagem de erro específica.

## <a name="see-also"></a>Confira também

- [Depurar vários processos](../debugger/debug-multiple-processes.md)
- [Depuração Just-in-time](../debugger/just-in-time-debugging-in-visual-studio.md)
- [Depuração remota](../debugger/remote-debugging.md)
