---
title: Depurar vários processos | Microsoft Docs
ms.date: 11/20/2018
ms.topic: how-to
f1_keywords:
- vs.debug.programs
- vs.debug.processes.attaching
- vs.debug.activeprogram
- vs.debug.attaching
- vs.debug.attachedprocesses
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: bde37134-66af-4273-b02e-05b3370c31ab
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 94a61e0083b17fa095b419a2066a4f8b9c39dfb7
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350596"
---
# <a name="debug-multiple-processes-c-visual-basic-c"></a>Depurar vários processos (C#, Visual Basic, C++)

O Visual Studio pode depurar uma solução que tenha vários processos. Você pode iniciar e alternar entre processos, interromper, continuar e percorrer a origem, parar a depuração e terminar ou desanexar de processos individuais.

## <a name="start-debugging-with-multiple-processes"></a>Iniciar a depuração com vários processos

Quando mais de um projeto em uma solução do Visual Studio puder ser executado de forma independente, você poderá selecionar qual projeto será iniciado pelo depurador. O projeto de inicialização atual aparece em negrito no **Gerenciador de soluções**.

Para alterar o projeto de inicialização, em **Gerenciador de soluções**, clique com o botão direito do mouse em um projeto diferente e selecione **definir como projeto de inicialização**.

Para iniciar a depuração de um projeto do **Gerenciador de soluções** sem torná-lo o projeto de inicialização, clique com o botão direito do mouse no projeto e selecione **depurar**  >  **Iniciar nova instância** ou **entrar em Nova instância**.

**Para definir o projeto de inicialização ou vários projetos de propriedades da solução:**

1. Selecione a solução em **Gerenciador de soluções** e, em seguida, selecione o ícone **Propriedades** na barra de ferramentas ou clique com o botão direito do mouse na solução e selecione **Propriedades**.

1. Na página **Propriedades** , selecione o projeto de inicialização **Propriedades comuns**  >  **Startup Project**.

   ![Alterando o tipo de inicialização de um projeto](../debugger/media/dbg_execution_startmultipleprojects.png "DBG_Execution_StartMultipleProjects")

1. Selecione **seleção atual**, **projeto de inicialização única** e um arquivo de projeto ou **vários projetos de inicialização**.

   Se você selecionar **vários projetos de inicialização**, poderá alterar a ordem de inicialização e a ação a ser tomada para cada projeto: **Iniciar**, **Iniciar sem depuração**ou **nenhum**.

1. Selecione **aplicar**ou **OK** para aplicar e fechar a caixa de diálogo.

### <a name="attach-to-a-process"></a><a name="BKMK_Attach_to_a_process"></a> Anexar a um processo

O depurador também pode ser *anexado* a aplicativos executados em processos fora do Visual Studio, incluindo em dispositivos remotos. Depois de anexar a um aplicativo, você pode usar o depurador do Visual Studio. Os recursos de depuração podem ser limitados. Depende se o aplicativo foi criado com informações de depuração, se você tem acesso ao código-fonte do aplicativo e se o compilador JIT está rastreando informações de depuração.

Para obter mais informações, consulte [anexar a processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md).

**Para anexar a um processo em execução:**

1. Com o aplicativo em execução, selecione **depurar**  >  **anexar ao processo**.

   ![Caixa de diálogo anexar ao processo](../debugger/media/dbg_attachtoprocessdlg.png "Caixa de diálogo Anexar ao Processo")

1. Na caixa de diálogo **anexar ao processo** , selecione o processo na lista **processos disponíveis** e, em seguida, selecione **anexar**.

>[!NOTE]
>O depurador não é anexado automaticamente a um processo filho que é inicializado por um processo depurado, mesmo se o projeto filho estiver na mesma solução. Para depurar um processo filho, anexe-o ao processo filho depois que ele for iniciado ou configure o editor do registro do Windows para iniciar o processo filho em uma nova instância do depurador.

### <a name="use-the-registry-editor-to-automatically-start-a-process-in-the-debugger"></a><a name="BKMK_Automatically_start_an_process_in_the_debugger"></a>Usar o editor do registro para iniciar automaticamente um processo no depurador

Às vezes, talvez seja necessário depurar o código de inicialização para um aplicativo que é iniciado por outro processo. Os exemplos incluem serviços e ações de configuração personalizada. Você pode fazer com que o depurador seja iniciado e anexado automaticamente ao aplicativo.

1. Inicie o editor do registro do Windows executando *regedit.exe*.

1. No editor do registro, navegue até **HKEY_LOCAL_MACHINE \Software\microsoft\windows NT\CurrentVersion\Image opções de execução de arquivo**.

1. Selecione a pasta do aplicativo que você deseja iniciar o depurador.

   Se o aplicativo não estiver listado como uma pasta filho, clique com o botão direito do mouse em **Opções de execução do arquivo de imagem**, selecione **nova**  >  **chave**e digite o nome do aplicativo. Ou clique com o botão direito do mouse na nova chave na árvore, selecione **renomear**e, em seguida, insira o nome do aplicativo.

1. Clique com o botão direito do mouse na nova chave na árvore e selecione **novo**  >  **valor de cadeia de caracteres**.

1. Altere o nome do novo valor de **novo valor #1** para `debugger` .

1. Clique com o botão direito do mouse em **depurador** e selecione **Modificar**.

   ![Caixa de diálogo Editar Cadeia de caracteres](../debugger/media/dbg_execution_automaticstart_editstringdlg.png "Caixa de diálogo Editar Cadeia de caracteres")

1. Na caixa de diálogo **Editar Cadeia de caracteres** , digite `vsjitdebugger.exe` na caixa **dados do valor** e selecione **OK**.

   ![Entrada de início do depurador automático no regedit.exe](../debugger/media/dbg_execution_automaticstart_result.png "Entrada de início do depurador automático no regedit.exe")

## <a name="debug-with-multiple-processes"></a><a name="BKMK_Switch_processes__break_and_continue_execution__step_through_source"></a>Depurar com vários processos
<a name="BKMK_Configure_the_execution_behavior_of_multiple_processes"></a>

Ao depurar um aplicativo com vários processos, os comandos de depuração de interrupção, depuração e continuação afetam todos os processos por padrão. Por exemplo, quando um processo é suspenso em um ponto de interrupção, a execução de todos os outros processos também é suspensa. Você pode alterar esse comportamento padrão para obter mais controle sobre os destinos dos comandos de execução.

**Para alterar se todos os processos são suspensos quando um processo é interrompido:**

- Em **ferramentas** (ou **depurar**) > **Opções**  >  **depuração**  >  **geral**, marque ou desmarque a caixa de seleção **interromper todos os processos quando um processo for interrompido** .

### <a name="break-step-and-continue-commands"></a><a name="BKMK_Break__step__and_continue_commands"></a> Comandos de interromper, depurar e continuar

A tabela a seguir descreve os comportamentos dos comandos de depuração quando a caixa de seleção **interromper todos os processos quando um processo é interrompido** está marcada ou desmarcada:

|**Comando**|Selecionada|Desmarcado|
|-|-|-|
|**Depurar**   >  **Interromper tudo**|Todos os processos são interrompidos.|Todos os processos são interrompidos.|
|**Depurar**  >  **Continuar**|Todos os processos são retomados.|Todos os processos suspensos são retomados.|
|**Depurar**  >  **Intervir**, **intervir**ou **percorrer**|Todos os processos estão em execução durante as etapas de processo atual. <br />Em seguida, todos os processos são interrompidos.|Etapas de processo atual. <br />Retomada de processos suspensos. <br />Executando a continuação dos processos.|
|**Depurar**  >  **Passe para o processo atual**, **Percorra o processo atual**ou **Percorra o processo atual**|N/D|Etapas de processo atual.<br />Outros processos mantém o estado existente (suspenso ou em execução).|
|Ponto de **interrupção** da janela de origem|Todos os processos são interrompidos.|Somente quebras do processo da janela de origem.|
|Execução da janela **de origem até o cursor**<br />A janela de origem deve estar no processo atual.|Todos os processos estão em execução enquanto o processo da janela de origem executa ao cursor e depois interrompe.<br />Em seguida, todos os outros processos não interrompidos.|O processo da janela de origem é executado para o cursor.<br />Outros processos mantém o estado existente (suspenso ou em execução).|
|Janela de **processos** > **processo de interrupção**|N/D|Quebras selecionadas do processo.<br />Outros processos mantém o estado existente (suspenso ou em execução).|
|Janela de **processos** > **continuar o processo**|N/D|O processo selecionado é retomado.<br />Outros processos mantém o estado existente (suspenso ou em execução).|

### <a name="find-the-source-and-symbol-pdb-files"></a><a name="BKMK_Find_the_source_and_symbol___pdb__files"></a> Localize a fonte e os arquivos de símbolo (.pdb)
Para navegar no código-fonte de um processo, o depurador precisa acessar seus arquivos de origem e de símbolo. Para obter mais informações, confira [Especificar arquivos de símbolo (.pdb) e de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).

Se você não puder acessar os arquivos para um processo, poderá navegar usando a janela de **desmontagem** . Para obter mais informações, consulte [como: usar a janela de desmontagem](../debugger/how-to-use-the-disassembly-window.md).

### <a name="switch-between-processes"></a><a name="BKMK_Switch_between_processes"></a> Alternar entre processos

Você pode anexar a vários processos quando estiver Depurando, mas apenas um processo está ativo no depurador em um determinado momento. Você pode definir o processo ativo *atual* ou na barra de ferramentas do **Localização de Depuração** ou na janela **Processos**. Para alternar entre processos, ambos os processos devem estar no modo de interrupção.

**Para definir o processo atual na barra de ferramentas local de depuração:**

1. Para abrir a barra de ferramentas **local de depuração** , selecione **Exibir**  >  **barras de ferramentas**  >  **local de depuração**.

1. Durante a depuração, na barra de ferramentas **local de depuração** , selecione o processo que você deseja definir como o processo atual na lista suspensa **processo** .

   ![Alternar entre processos](../debugger/media/dbg_execution_switchbetweenmodules.png "DBG_Execution_SwitchBetweenModules")

**Para definir o processo atual na janela processos:**

1. Para abrir a janela **processos** , durante a depuração, selecione **depurar**  >  **Windows**  >  **processos**do Windows.

1. Na janela **processos** , o processo atual é marcado por uma seta amarela. Clique duas vezes no processo que você deseja definir como o processo atual.

   ![Janela de processos](../debugger/media/dbg_processeswindow.png "DBG_ProcessesWindow")

Alternar para um processo o define como o processo atual para fins de depuração. As janelas do depurador mostram o estado do processo atual e os comandos de depuração afetam apenas o processo atual.

## <a name="stop-debugging-with-multiple-processes"></a>Parar a depuração com vários processos

Por padrão, quando você seleciona **depurar**  >  **parar depuração**, o depurador termina ou se desconecta de todos os processos.

- Se o processo atual foi iniciado no depurador, o processo é encerrado.

- Se você já anexou o depurador ao processo atual, o depurador será desanexado do processo e o deixará em execução.

Se você iniciar a depuração de um processo de uma solução do Visual Studio, anexe a outro processo que já está em execução e, em seguida, escolha **parar depuração**, a sessão de depuração terminará. O processo que foi iniciado no Visual Studio termina, enquanto o processo que você anexou mantém a execução.

Para controlar a maneira como a **interrupção da depuração** afeta um processo individual, na janela **processos** , clique com o botão direito do mouse em um processo e marque ou desmarque a caixa de seleção **desanexar quando a depuração for interrompida** .

>[!NOTE]
>A opção **interromper todos os processos quando um processo interrompe** o depurador não afeta a interrupção, o encerramento ou a desanexação de processos.

### <a name="stop-terminate-and-detach-commands"></a>Parar, finalizar e desanexar comandos

A tabela a seguir descreve os comportamentos dos comandos parar, encerrar e desanexar do depurador com vários processos:

|**Comando**|**Descrição**|
|-|-|
|**Depurar**  >  **Parar depuração**|A menos que o comportamento seja alterado na janela **processos** , os processos iniciados pelo depurador são encerrados e os processos anexados são desanexados.|
|**Depurar**  >  **Encerrar tudo**|Todos os processos foram encerrados.|
|**Depurar**  >  **Desanexar tudo**|O depurador desanexa todos os processos.|
|Janela de **processos** > **desanexar processo**|O depurador dispara do processo selecionado.<br />Outros processos mantém o estado existente (suspenso ou em execução).|
|Janela de **processos** > **encerrar processo**|O processo selecionado foi encerrado.<br />Outros processos mantém o estado existente (suspenso ou em execução).|
|Janela de **processos** > **desanexar quando a depuração parar**|Se selecionado, **depurar**  >  **parar depuração** desanexará do processo selecionado. <br />Se não for selecionado, **depurar**  >  **parar depuração** finalizará o processo selecionado. |

## <a name="see-also"></a>Veja também

- [Especificar o símbolo (. pdb) e os arquivos de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
- [Anexar a processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [Navegando pelo código com o depurador](../debugger/navigating-through-code-with-the-debugger.md)
- [Depuração Just-in-time](../debugger/just-in-time-debugging-in-visual-studio.md)
- [Depurar aplicativos multissegmentados](../debugger/debug-multithreaded-applications-in-visual-studio.md)