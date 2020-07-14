---
title: Depurar vários processos | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.programs
- vs.debug.processes.attaching
- vs.debug.activeprogram
- vs.debug.attaching
- vs.debug.attachedprocesses
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: bde37134-66af-4273-b02e-05b3370c31ab
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 97d98522e011023cb3a021a69c9a82e8bb34cef3
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85533270"
---
# <a name="debug-multiple-processes"></a>Depurar vários processos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Veja como iniciar processos de depuração, alternar entre processos, interromper e continuar a execução, percorrer o código-fonte, interromper a depuração e terminar ou desanexar dos processos.  
  
## <a name="contents"></a><a name="BKMK_Contents"></a>Índice  
 [Configurar o comportamento de execução de vários processos](#BKMK_Configure_the_execution_behavior_of_multiple_processes)  
  
 [Localizar os arquivos de origem e símbolo (. pdb)](#BKMK_Find_the_source_and_symbol___pdb__files)  
  
 [Iniciar vários processos em uma solução VS, anexar a um processo, iniciar automaticamente um processo no depurador](#BKMK_Start_multiple_processes_in_a_VS_solution__attach_to_a_process__automatically_start_a_process_in_the_debugger)  
  
 [Alternar processos, interromper e continuar a execução, percorrer a origem](#BKMK_Switch_processes__break_and_continue_execution__step_through_source)  
  
 [Parar a depuração, finalizar ou desanexar dos processos](#BKMK_Stop_debugging__terminate_or_detach_from_processes)  
  
## <a name="configure-the-execution-behavior-of-multiple-processes"></a><a name="BKMK_Configure_the_execution_behavior_of_multiple_processes"></a>Configurar o comportamento de execução de vários processos  
 Por padrão, quando vários processos são executados no depurador, os comandos de quebra, avanço e interrupção do depurador geralmente afetam todos os processos. Por exemplo, quando um processo é suspenso em um ponto de interrupção, a execução de todos outros processos é suspendida também. Você pode alterar esse comportamento padrão para obter mais controle sobre os destinos dos comandos de execução.  
  
1. No menu de **Depurar**, escolha **Opções e Configurações**.  
  
2. Na página **depuração**, **geral** , desmarque a caixa de seleção **interromper todos os processos quando um processo for interrompido** .  
  
   ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior  
  
## <a name="find-the-source-and-symbol-pdb-files"></a><a name="BKMK_Find_the_source_and_symbol___pdb__files"></a> Localize a fonte e os arquivos de símbolo (.pdb)  
 Para navegar no código-fonte de um processo, o depurador precisa acessar os arquivos de origem e os arquivos do símbolo do processo. Consulte [especificar símbolo (. pdb) e arquivos de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).  
  
 Se você não conseguir acessar arquivos para um processo, poderá navegar usando a janela de desmontagem. Consulte [como: usar a janela de desmontagem](../debugger/how-to-use-the-disassembly-window.md)  
  
 ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior  
  
## <a name="start-multiple-processes-in-a-vs-solution-attach-to-a-process-automatically-start-a-process-in-the-debugger"></a><a name="BKMK_Start_multiple_processes_in_a_VS_solution__attach_to_a_process__automatically_start_a_process_in_the_debugger"></a>Iniciar vários processos em uma solução VS, anexar a um processo, iniciar automaticamente um processo no depurador  
  
- [Iniciar a depuração de vários processos em uma solução do Visual Studio](#BKMK_Start_debugging_multiple_processes_in_a_Visual_Studio_solution) • [alterar o projeto de inicialização](#BKMK_Change_the_startup_project) • [Iniciar um projeto específico em uma solução](#BKMK_Start_a_specific_project_in_a_solution) • [Iniciar vários projetos em uma solução](#BKMK_Start_multiple_projects_in_a_solution) • [anexar a um processo](#BKMK_Attach_to_a_process) • [iniciar automaticamente um processo no depurador](#BKMK_Automatically_start_an_process_in_the_debugger)  
  
> [!NOTE]
> O depurador não é anexado automaticamente a um processo filho que é inicializado por um processo depurado, mesmo se o projeto filho estiver na mesma solução. Para depurar um processo filho:  
> 
> - Anexar ao processo filho depois que for iniciado.  
> 
>   -ou-  
>   - Configurar o Windows para iniciar automaticamente o processo filho em uma nova instância do depurador.  
  
### <a name="start-debugging-multiple-processes-in-a-visual-studio-solution"></a><a name="BKMK_Start_debugging_multiple_processes_in_a_Visual_Studio_solution"></a>Iniciar a depuração de vários processos em uma solução do Visual Studio  
 Quando você tiver mais de um projeto em uma solução do Visual Studio que pode executar de forma independente (projetos que são executados em processos separados), será possível selecionar quais projetos o depurador inicia.  
  
 ![Alterando o tipo de inicialização de um projeto](../debugger/media/dbg-execution-startmultipleprojects.png "DBG_Execution_StartMultipleProjects")  
  
#### <a name="change-the-startup-project"></a><a name="BKMK_Change_the_startup_project"></a>Alterar o projeto de inicialização  
 Para alterar o projeto de inicialização para uma solução, selecione o projeto em Gerenciador de Soluções e, em seguida, escolha **definir como projeto de inicialização** no menu de contexto.  
  
#### <a name="start-a-specific-project-in-a-solution"></a><a name="BKMK_Start_a_specific_project_in_a_solution"></a>Iniciar um projeto específico em uma solução  
 Para iniciar um projeto para uma solução sem alterar o projeto de inicialização padrão, selecione o projeto em Gerenciador de Soluções e, em seguida, escolha **depurar** no menu de contexto. Você pode escolher **Iniciar nova instância** ou **entrar em Nova instância**.  
  
 ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") início [Iniciar vários processos em uma solução vs, anexar a um processo, iniciar automaticamente um processo no depurador](../debugger/debug-multiple-processes.md#BKMK_Start_multiple_processes_in_a_VS_solution__attach_to_a_process__automatically_start_a_process_in_the_debugger)  
  
 ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior  
  
#### <a name="start-multiple-projects-in-a-solution"></a><a name="BKMK_Start_multiple_projects_in_a_solution"></a>Iniciar vários projetos em uma solução  
  
1. Selecione a solução em Gerenciador de Soluções e, em seguida, escolha **Propriedades** no menu de contexto.  
  
2. Selecione **Propriedades comuns**, **projeto de inicialização** na caixa de diálogo **Propriedades** .  
  
3. Para cada projeto que você deseja alterar, escolha **Iniciar**, **Iniciar sem depuração**ou **nenhum**.  
  
   ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") início [Iniciar vários processos em uma solução vs, anexar a um processo, iniciar automaticamente um processo no depurador](../debugger/debug-multiple-processes.md#BKMK_Start_multiple_processes_in_a_VS_solution__attach_to_a_process__automatically_start_a_process_in_the_debugger)  
  
   ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior  
  
### <a name="attach-to-a-process"></a><a name="BKMK_Attach_to_a_process"></a> Anexar a um processo  
 O depurador também pode *anexar* a programas que estão sendo executados em processos fora do Visual Studio, incluindo programas que estão sendo executados em um dispositivo remoto. Após vincular-se a um programa, você poderá usar comandos de execução do depurador, inspecionar o estado do programa e assim por diante. A capacidade de inspecionar o programa pode ser limitada se o programa foi criado com informações de depuração, se você tem acesso ao código-fonte do programa, e se o compilador just-in-time (JIT) do Common Language Runtime está controlando as informações de depuração.  
  
 Consulte [anexar a processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md) para obter mais informações.  
  
 **Anexar a um processo que está executando em seu computador local**  
  
 Escolha **depurar**, **anexar ao processo**. Na caixa de diálogo **anexar ao processo** , selecione o processo na lista **processos disponíveis** e escolha **anexar**.  
  
 ![Caixa de diálogo anexar ao processo](../debugger/media/dbg-attachtoprocessdlg.png "DBG_AttachToProcessDlg")  
  
 ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior  
  
### <a name="automatically-start-a-process-in-the-debugger"></a><a name="BKMK_Automatically_start_an_process_in_the_debugger"></a>Iniciar automaticamente um processo no depurador  
 Às vezes, pode ser necessário depurar o código de inicialização para um programa que foi iniciado por outro processo. Os exemplos incluem serviços e ações de configuração personalizada. Nesses cenários, você poderá fazer com que o depurador seja iniciado e automaticamente anexado quando seu aplicativo iniciar.  
  
1. Inicie o editor do registro (**regedit.exe**).  
  
2. Navegue até a pasta **HKEY_LOCAL_MACHINE \Software\microsoft\windows NT\CurrentVersion\Image opções de execução de arquivo** .  
  
3. Selecione a pasta do aplicativo que você deseja iniciar o depurador.  
  
    Se o nome do aplicativo não estiver listado como uma pasta filho, selecione **Opções de execução de arquivo de imagem** e, em seguida, escolha **nova**, **chave** no menu de contexto. Selecione a nova chave, escolha **renomear** no menu de atalho e, em seguida, insira o nome do aplicativo.  
  
4. No menu de contexto da pasta do aplicativo, escolha **novo**, **valor da cadeia de caracteres**.  
  
5. Altere o nome do novo valor de **novo valor** para `debugger` .  
  
6. No menu de contexto da entrada do depurador, escolha **Modificar**.  
  
7. Na caixa de diálogo Editar Cadeia de caracteres, digite `vsjitdebugger.exe` a caixa **dados do valor** .  
  
    ![Caixa de diálogo Editar Cadeia de caracteres](../debugger/media/dbg-execution-automaticstart-editstringdlg.png "DBG_Execution_AutomaticStart_EditStringDlg")  
  
   ![Entrada de início do depurador automático no regedit.exe](../debugger/media/dbg-execution-automaticstart-result.png "DBG_Execution_AutomaticStart_Result")  
  
   ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior  
  
## <a name="switch-processes-break-and-continue-execution-step-through-source"></a><a name="BKMK_Switch_processes__break_and_continue_execution__step_through_source"></a>Alternar processos, interromper e continuar a execução, percorrer a origem  
  
- [Alternar entre processos](#BKMK_Switch_between_processes) • [comandos break, Step e continue](#BKMK_Break__step__and_continue_commands)  
  
### <a name="switch-between-processes"></a><a name="BKMK_Switch_between_processes"></a> Alternar entre processos  
 Você pode conectar-se a vários processos quando está depurando, mas somente um processo está ativo no depurador em um determinado momento. Você pode definir o processo ativo ou *atual* na barra de ferramentas local de depuração ou na janela **processos** . Para alternar entre processos, ambos os processos devem estar no modo de interrupção.  
  
 **Para definir o processo atual**  
  
- Na barra de ferramentas local de depuração, escolha **processar** para exibir a caixa de listagem **processo** . Selecione o processo que você deseja designar como o processo atual.  
  
   ![Alternar entre processos](../debugger/media/dbg-execution-switchbetweenmodules.png "DBG_Execution_SwitchBetweenModules")  
  
   Se a barra de ferramentas **local de depuração** não estiver visível, escolha **ferramentas**, **Personalizar**. Na guia **barras de ferramentas** , escolha **local de depuração**.  
  
- Abra a janela **processos** (atalho **Ctrl + Alt + Z**), localize o processo que você deseja definir como o processo atual e clique duas vezes nele.  
  
   ![Janela de processos](../debugger/media/dbg-processeswindow.png "DBG_ProcessesWindow")  
  
   O processo atual é marcado por uma seta amarela.  
  
  Alternar para um projeto o torna o processo atual para fins de depuração. Qualquer janela do depurador que você exibir mostrará o estado do processo atual e todos os comandos das etapas afetarão somente o processo atual.  
  
  ![Voltar aos](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [processos do comutador Top, interromper e continuar a execução, percorrer a origem](../debugger/debug-multiple-processes.md#BKMK_Switch_processes__break_and_continue_execution__step_through_source)  
  
  ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior  
  
### <a name="break-step-and-continue-commands"></a><a name="BKMK_Break__step__and_continue_commands"></a> Comandos de interromper, depurar e continuar  
  
> [!NOTE]
> Por padrão, os comandos interromper, continuar e avançar depurador afetam todos os processos que estão sendo depurados. Para alterar esse comportamento, consulte [Configurar o comportamento de execução de vários processos](#BKMK_Configure_the_execution_behavior_of_multiple_processes)  
  
|**Comando**|**Interromper todos os processos quando um processo for interrompido**<br /><br /> Verificado (Padrão)|**Interromper todos os processos quando um processo for interrompido**<br /><br /> Desmarcada|  
|-|-|-|
|Menu **depurar** :<br /><br /> -   **Interromper tudo**|Todos os processos são interrompidos.|Todos os processos são interrompidos.|  
|Menu **depurar** :<br /><br /> -   **Continua**|Todos os processos são retomados.|Todos os processos suspensos são retomados.|  
|Menu **depurar** :<br /><br /> -   **Intervir**<br />-   **Depurar**<br />-   **Sair**|Todos os processos estão em execução durante as etapas de processo atual.<br /><br /> Em seguida, todos os processos são interrompidos.|Etapas de processo atual.<br /><br /> Retomada de processos suspensos.<br /><br /> Executando a continuação dos processos.|  
|Menu **depurar** :<br /><br /> -   **Entrar no processo atual**<br />-   **Depurar o processo atual**<br />-   **Depurar o processo atual**|N/D|Etapas de processo atual.<br /><br /> Outros processos mantém o estado existente (suspenso ou em execução).|  
|Janela de origem<br /><br /> -   **Breakpoint**|Todos os processos são interrompidos.|Somente quebras do processo da janela de origem.|  
|Menu de contexto da janela de origem:<br /><br /> -   **Executar até o cursor**<br /><br /> A janela de origem deve estar no processo atual.|Todos os processos estão em execução enquanto o processo da janela de origem executa ao cursor e depois interrompe.<br /><br /> Em seguida, todos os outros processos não interrompidos.|O processo da janela de origem é executado para o cursor.<br /><br /> Outros processos mantém o estado existente (suspenso ou em execução).|  
|Menu de contexto da janela **processos** :<br /><br /> -   **Interromper processo**|N/D|Quebras selecionadas do processo.<br /><br /> Outros processos mantém o estado existente (suspenso ou em execução).|  
|Menu de contexto da janela **processos** :<br /><br /> -   **Continuar processo**|N/D|O processo selecionado é retomado.<br /><br /> Outros processos mantém o estado existente (suspenso ou em execução).|  
  
 ![Voltar aos](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [processos do comutador Top, interromper e continuar a execução, percorrer a origem](../debugger/debug-multiple-processes.md#BKMK_Switch_processes__break_and_continue_execution__step_through_source)  
  
 ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior  
  
## <a name="stop-debugging-terminate-or-detach-from-processes"></a><a name="BKMK_Stop_debugging__terminate_or_detach_from_processes"></a>Parar depuração, encerrar ou desanexar de processos  
  
- [Parar, finalizar e desanexar comandos](#BKMK_Stop__terminate__and_detach_commands)  
  
  Por padrão, quando você escolhe **depurar**, **interrompe a depuração** quando vários processos são abertos no depurador, o depurador é encerrado ou desanexado de todos os processos, dependendo de como o processo foi aberto no depurador:  
  
- Se o processo atual foi iniciado no depurador, esse processo é finalizado.  
  
- Se você já anexou o depurador ao processo atual, o depurador será desanexado do processo e o deixará em execução.  
  
  Por exemplo, se você começar a depurar um processo de uma solução do Visual Studio, anexar a outro processo que já está em execução e, em seguida, escolher **parar depuração**, a sessão de depuração terminará, o processo iniciado no Visual Studio será encerrado, enquanto o processo que você anexou será deixado em execução. Você pode usar os seguintes procedimentos para controlar a maneira que você interrompe a depuração.  
  
> [!NOTE]
> A opção **interromper todos os processos quando um processo é interrompido** não afeta a interrupção da depuração ou do encerramento e desanexação de processos.  
  
 **Para alterar como a depuração de parada afeta um processo individual**  
  
- Abra a janela **processos** (atalho **Ctrl + Alt + Z**). Selecione um processo e marque ou desmarque a caixa de seleção **desanexar ao parar de depurar** .  
  
### <a name="stop-terminate-and-detach-commands"></a><a name="BKMK_Stop__terminate__and_detach_commands"></a>Comandos de parar, encerrar e desanexar  
  
|**Comando**|**Descrição**|  
|-|-|  
|Menu **depurar** :<br /><br /> -   **Parar depuração**|A menos que o comportamento seja alterado pela janela de **processos** **desanexar quando a depuração parar** :<br /><br /> 1. os processos iniciados pelo depurador são encerrados.<br />2. os processos anexados são desanexados do depurador.|  
|Menu **depurar** :<br /><br /> -   **Encerrar tudo**|Todos os processos são encerrados.|  
|Menu **depurar** :<br /><br /> -   **Desanexar tudo**|O depurador desanexa todos os processos.|  
|Menu de contexto da janela **processos** :<br /><br /> -   **Desanexar processo**|O depurador dispara do processo selecionado.<br /><br /> Outros processos mantém o estado existente (suspenso ou em execução).|  
|Menu de contexto da janela **processos** :<br /><br /> -   **Encerrar processo**|O processo selecionado é finalizado.<br /><br /> Outros processos mantém o estado existente (suspenso ou em execução).|  
|Menu de contexto da janela **processos** :<br /><br /> -   **Desanexar quando a depuração parar**|Alterna o comportamento da **depuração**, **interrompe a depuração** para o processo selecionado:<br /><br /> -Verificado: o depurador se desconecta do processo.<br />-Limpo: o processo é encerrado.|  
  
 ![Voltar ao início](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [parar depuração, encerrar ou desanexar de processos](../debugger/debug-multiple-processes.md#BKMK_Stop_debugging__terminate_or_detach_from_processes)  
  
 ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior  
  
## <a name="see-also"></a>Consulte Também  
 [Especificar o símbolo (. pdb) e os arquivos de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)   
 [Anexar a processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)   
 [Navegando pelo código com o depurador](../debugger/navigating-through-code-with-the-debugger.md)   
 [Depuração Just-in-time](../debugger/just-in-time-debugging-in-visual-studio.md)   
 [Depurar aplicativos multithread](../debugger/debug-multithreaded-applications-in-visual-studio.md)
